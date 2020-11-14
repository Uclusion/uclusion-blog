---
layout: post
title:  "Authenticated S3 Downloads Without Passing Through Lambdas"
author: ben
categories: [ engineering, backend ]
---
In my [previous story](https://medium.com/uclusion/uploading-user-files-to-s3-without-passing-through-your-lambdas-90cdd26240d5) I covered how [Uclusion](https://www.uclusion.com/?utm_source=devto&utm_medium=blog&utm_campaign=devs3download) lets users securely upload files to S3 without having to route the upload data through our Lambdas. In this installment, I’ll explain how to do the same when users download files.

Step 1: Block public access from your bucket.

S3 bucket permissions should be as restrictive as possible, and later in the article I’ll cover how your users will get files without needing direct access to the bucket. Therefore, block it all. Here’s what Uclusion’s public access policy looks like from the console:

![](https://cdn-images-1.medium.com/max/3412/1*YIwb_WTvb6CrHnZEABt-bQ.png)

Step 2. Set up a bucket CORS policy

Since the users are directly uploading via Presigned Post (or PUT if you don’t need fine control), and will be downloading through a CloudFront distribution, the bucket needs a CORS access policy that browsers won’t balk at. Here’s Uclusion’s:

    <?xml version=”1.0" encoding=”UTF-8"?>
    <CORSConfiguration xmlns=”[http://s3.amazonaws.com/doc/2006-03-01/](http://s3.amazonaws.com/doc/2006-03-01/)">
    <CORSRule>
     <AllowedOrigin>*</AllowedOrigin>
     <AllowedMethod>GET</AllowedMethod>
     <AllowedMethod>PUT</AllowedMethod>
     <AllowedMethod>POST</AllowedMethod>
     <AllowedMethod>HEAD</AllowedMethod>
     <MaxAgeSeconds>3000</MaxAgeSeconds>
     <AllowedHeader>*</AllowedHeader>
    </CORSRule>
    </CORSConfiguration>

Step 3: Create a CloudFront distribution for the bucket

As we’ve blocked public access to the bucket we need a way for users to download files. To provide this, we will create a [CloudFront CDN](https://aws.amazon.com/cloudfront/) distribution for the bucket. This has the added benefit of allowing you to cache frequently accessed files near the users, and reduce their latency. There is one HUGE gotcha however, in that all CloudFront distributions must be in US-EAST-1 if you want them to be globally distributed.

Uclusion uses the [Serverless Framework](https://www.serverless.com/) to specify our CloudFormation templates, and here’s the block that sets up the distribution. Also, the configuration below sets up the Origin Access Identity and IAM policy the distribution will need to read from the bucket.

    Resources:
      FilesBucketPolicy:
        Type: AWS::S3::BucketPolicy
        Properties:
          Bucket: ${your_bucket_name}
          PolicyDocument:
            Statement:
              - Sid: CloudFrontRead
                Effect: Allow
                Principal:
                  CanonicalUser:
                    Fn::GetAtt: [ S3FilesCloudfrontOriginAccessIdentity, S3CanonicalUserId ]
                Action:
                  - s3:GetObject
                Resource: arn:aws:s3:::${your_bucket_name}/*
      S3FilesDistribution:
        Type: AWS::CloudFront::Distribution
        Properties:
          DistributionConfig:
            Origins:
              - DomainName: ${your_bucket_name}.s3.us-west-2.amazonaws.com *#all buckets in Uclusion are us-west-2
                *Id: S3FilesOrigin
                S3OriginConfig:
                  OriginAccessIdentity:
                    Fn::Join:
                      - ''
                      - - 'origin-access-identity/cloudfront/'
                        - Ref: S3FilesCloudfrontOriginAccessIdentity
    
            Enabled: 'true'
            Comment: S3 file distribution
            DefaultCacheBehavior:
              ForwardedValues:
                QueryString: 'false'
                Cookies:
                  Forward: none
                Headers:
                  - Origin
                  - Access-Control-Allow-Origin
                  - Access-Control-Request-Origin
                  - Access-Control-Request-Methods
                  - Access-Control-Allow-Methods
                  - Access-Control-Request-Method
                  - Access-Control-Request-Headers
              AllowedMethods:
                - GET
                - HEAD
                - OPTIONS
              TargetOriginId: S3FilesOrigin
              CachedMethods: [GET, HEAD, OPTIONS]
              ViewerProtocolPolicy: redirect-to-https
            PriceClass: PriceClass_200
            ViewerCertificate:
              CloudFrontDefaultCertificate: 'true'
      S3FilesCloudfrontOriginAccessIdentity:
        Type: AWS::CloudFront::CloudFrontOriginAccessIdentity
        Properties:
          CloudFrontOriginAccessIdentityConfig:
            Comment: "user-files-access-identity"

Step 4: Create an [authorizer](https://aws.amazon.com/lambda/edge) for the CloudFront distribution

Cloudfront, unlike S3, allows you to set up a Lambda as an access request authorizer via [Lambda Edge](https://aws.amazon.com/lambda/edge). This allows you to authenticate your users when they want to download a file. Here’s the basic picture (shamelessly stolen from a related [Amazon Blog](https://aws.amazon.com/blogs/networking-and-content-delivery/authorizationedge-how-to-use-lambdaedge-and-json-web-tokens-to-enhance-web-application-security/)):

![](https://cdn-images-1.medium.com/max/2000/1*ZitRPstFKx3016JsykcjXA.png)

Note: at this time Lambda Edge does not support [Provisioned Concurrency](https://aws.amazon.com/blogs/aws/new-provisioned-concurrency-for-lambda-functions/), which means you might need the [warmup plugin for Serverless Framework](https://www.serverless.com/plugins/serverless-plugin-warmup/) when launching it.

In our case we use uploads for Images, and we didn’t want to modify the normal fetching of images too much. Hence, modify the request on the way out of the browser to embed the token as a request param of the GET call if we recongize it as our file.

Here’s the Serverless Framework definition for the authorizer function, and most of it’s code

    s3FilesAuthorizer:
      name: 'S3FilesAccessAuthorizer'
      handler: authorizers/s3_files_authorizer.lambda_handler
      runtime: python3.7
      memorySize: 128
      timeout: 5
      region: us-east-1
      lambdaAtEdge:
        distribution: 'S3FilesDistribution'
        eventType: 'viewer-request'
      retain: true

    import jwt
    from authorizers.key_data import get_key
    from urllib.parse import parse_qs
    
    def lambda_handler(event, context):
        *# get the request object
        *print(event)
        request = event['Records'][0]['cf']['request']
        method = request['method']
        if method == 'OPTIONS':
            return authorized(request)
        request_path = request['uri']
        print('Request Path: ' + request_path)
        query_string = request['querystring']
        print(query_string)
        parsed_query_string = parse_qs(query_string)
        token = parsed_query_string.get('authorization')[0]
        *# no token? unauthorized
        *if not token:
            return unauthorized()
        if not valid_token(token): # an exercise for the reader
            return unauthorized()
        return authorized

    def authorized(request):
        headers = request['headers']
        *# add the origin header because otherwise s3 won't do cors things
        *print('Authorizing request')
        origin = headers.get('origin')
        if origin is None:
            request['headers']['origin'] = [{'key': 'Origin', 'value': 'http://www.uclusion.com'}]
        return request

    def unauthorized():
        return {
            'status': '403',
            'statusDescription': 'Unauthorized'
        }

Step 5: Extra credit, a service worker

Uclusion uses an authorization request param, but we didn’t want to worry about token expiration in links users may embed in their content. Therefore we need to intercept the request for the image on the way out, and add the param if needed. Fortunately [Service Workers](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) allow us to do just that.

Below is the code for Uclusion’s image service worker. It firsts looks for a specific pattern in the URL that matches our CloudFront image paths, and then fetches the token out of token storage and adds the authorization request param with that token (You may notice if it fails to get a token, it tries the user’s account key, as some files are accessible to the users’ account).

    const OUR_FILE_PATTERN = /https\:\/\/\w+.cloudfront.net\/(\w{8}(-\w{4}){3}-\w{12})\/\w{8}(-\w{4}){3}-\w{12}.*/i;
    self.*importScripts*('localforage.min.js');
    self.addEventListener('fetch', (event) => {
      const { request } = event;
      const { method, url } = request;
      if (method === 'GET') {
        const match = url.match(OUR_FILE_PATTERN);
        if (match) {
          const promise = self.localforage.createInstance({ storeName: 'TOKEN_STORAGE_MANAGER' }).getItem(fileKey)
            .then((token) => {
              if (token) {
                return token;
              } else {
                return self.localforage.createInstance({ storeName: 'TOKEN_STORAGE_MANAGER' }).getItem(homeAccountKey);
              }
            }).then((token) => {
              const newUrl = new URL(url);
              newUrl.searchParams.set('authorization', token);
              return *fetch*(newUrl);
            });
          event.respondWith(promise);
        }
      }
    });

See source on Github for this service worker [here](https://github.com/Uclusion/uclusion_web_ui/blob/master/public/image-url-rewriter-service-worker.js).