---
layout: post
title:  "Example production Serverless files"
author: david
categories: [ engineering, backend ]
---
Update: Well turns out the new provisioned concurrency feature is mostly unusable. [The hidden cost of Lambda provisioned concurrency pricing](https://www.trek10.com/blog/provisioned-lambda-concurrency) explains why but unfortunately the cost is not at all hidden. Uclusion was billed $3,347.63 for 803,424,893.570 Lambda-GB-Second on Lambdas that were not costing anything under the “warmup” [way](https://www.serverless.com/plugins/serverless-plugin-warmup). We are disputing the charge but will have to revert to trying to solve cold starts with the synthetic traffic plugin.

[Uclusion](https://www.uclusion.com/?utm_source=uclusion&utm_medium=blog&utm_campaign=devexampleserverlessfiles) uses [Serverless](https://www.serverless.com/open-source) to deploy Lambdas in AWS. There are many aspects to our configuration so this post just walks you through a basic abbreviated file. You can use [Serverless documentation](https://www.serverless.com/framework/docs/providers/aws/guide/serverless.yml) to understand the key words.

    service: uclusion-market-api
    
    plugins:
      - serverless-plugin-aws-alerts
    custom:
      alerts:
        topics:
          alarm:
            topic: uclusion-market-api-${opt:stage, self:provider.stage}-alerts-alarm
            notifications:
              - protocol: email
                endpoint: [an email address]
        alarms:
          - functionErrors
          - functionThrottles*
    
    *provider:
      name: aws
      runtime: python3.7
      region: us-west-2
      versionFunctions: false
      usagePlan:
        quota:
          limit: ${ssm:/usageplan/limit}
          period: DAY
        throttle:
          burstLimit: 400
          rateLimit: 100
      apiGateway:
        apiKeySourceType: AUTHORIZER
      environment:
        usersServicePrefix: uclusion-users-dev-
        marketsServicePrefix: uclusion-markets-dev-
        USER_POOL_ID: us-west-2_${ssm:/userpool/id}
        COGNITO_CLIENT_ID: ${ssm:/cognito/client/id~true}
        GLOBAL_CAPABILITY_SECRET_KEY: ${ssm:/capability/secret/key~true}
        CAPABILITY_SIGNING_ALGORITHM: HS256
        myRegion: us-west-2
    
    package:
      exclude:
        - node_modules/**
        - .idea/**
        - env/**
        - tests/**
        - README.md
        - setup.cfg
        - package.json
        - package-lock.json
    
    functions:
      authorizerFunc:
        provisionedConcurrency: 5
        handler: authorizers/long_capability_auth.lambda_handler
        role: arn:aws:iam::${ssm:/account/id}:role/requests/generalapi/policy/GeneralAPIRoleShared
        layers: ${file(layers.yml):${opt:stage, self:provider.stage}}
      update_investment:
        provisionedConcurrency: ${ssm:/account/provisioned}
        role: arn:aws:iam::${ssm:/account/id}:role/requests/generalapi/policy/GeneralAPIRoleShared
        handler: handlers/investment_update.update
        layers: ${file(layers.yml):${opt:stage, self:provider.stage}}
        timeout: 20
        events:
          - http:
              path: invest
              method: post
              private: true
              cors: true
              authorizer: ${file(authorizer.yml):${opt:stage, self:provider.stage}}
      remove_investment:
        provisionedConcurrency: ${ssm:/account/provisioned}
        role: arn:aws:iam::${ssm:/account/id}:role/requests/generalapi/policy/GeneralAPIRoleShared
        handler: handlers/investment_remove.delete
        layers: ${file(layers.yml):${opt:stage, self:provider.stage}}
        timeout: 20
        events:
          - http:
              path: invest/{investible_id}
              method: delete
              private: true
              cors: true
              authorizer: ${file(authorizer.yml):${opt:stage, self:provider.stage}}
      get_market:
        provisionedConcurrency: ${ssm:/account/provisioned}
        role: arn:aws:iam::${ssm:/account/id}:role/requests/generalapi/policy/GeneralAPIRoleShared
        handler: handlers/get_market.get
        layers: ${file(layers.yml):${opt:stage, self:provider.stage}}
        events:
          - http:
              path: get
              method: get
              private: true
              cors: true
              authorizer: ${file(authorizer.yml):${opt:stage, self:provider.stage}}
      update_market:
        provisionedConcurrency: ${ssm:/account/provisioned}
        role: arn:aws:iam::${ssm:/account/id}:role/requests/generalapi/policy/GeneralAPIRoleShared
        handler: handlers/market_update.update
        layers: ${file(layers.yml):${opt:stage, self:provider.stage}}
        events:
          - http:
              path: update
              method: patch
              private: true
              cors: true
              authorizer: ${file(authorizer.yml):${opt:stage, self:provider.stage}}
    resources:
      Resources:
        GatewayResponseDefault4XX: *# See https://serverless.com/blog/cors-api-gateway-survival-guide
          *Type: 'AWS::ApiGateway::GatewayResponse'
          Properties:
            ResponseParameters:
              gatewayresponse.header.Access-Control-Allow-Origin: "'*'"
              gatewayresponse.header.Access-Control-Allow-Headers: "'*'"
            ResponseType: DEFAULT_4XX
            RestApiId:
              Ref: 'ApiGatewayRestApi'

Here the authorizer.yml is

    dev:
      name: authorizerFunc
      authorizer_type: TOKEN
      identitySource: method.request.header.Authorization

and the layers.yml is

    dev:
      - ${cf:udcommon-layer-dev.UdcommonLayerExport}
      - ${cf:ucommon-layer-dev.UcommonLayerExport}
      - ${cf:ubcommon-layer-dev.UbcommonLayerExport}

and you use the environment section in your Lambda Python code like so

    os.environ['usersServicePrefix']

One of the more confusing points when you initially setup using AWS Lambdas is the API Gateway [stage feature](https://docs.aws.amazon.com/apigateway/latest/developerguide/set-up-stages.html). So far Uclusion has not found a way to make use of that feature at all. We created an [organization](https://aws.amazon.com/organizations) with three accounts — dev, stage and production and use the same Serverless yml to deploy to each of them (using CircleCI). So each environment has only one API Gateway stage.

In theory you could canary test a new version of the API in production by having a second stage but in practice the new stage shares [SSM](https://docs.aws.amazon.com/systems-manager/latest/userguide/what-is-systems-manager.html) configuration (see ssm: usage above), DynamoDB, DynamoDB streams, etc. and so if the canary dies the whole site might die as well.

Another confusing aspect is the provisionedConcurrency. Any call you make to an outside static resource like os.environ[‘usersServicePrefix’] must be globally declared in your Python file — not inside a method. Otherwise instead of the call being made once when the Lambda is provisioned it will be made every time the method is called.

Also confusing with provisionedConcurrency you will see in your logs something like

    Init Duration: 2285.65 ms

when you run a Lambda. Even more confusing is that if you run that Lambda twice in a row the init duration won’t be there on the second call. I can’t say for certain what is happening but it was the same with the old warm-up plugin running every 5 minutes.

Finally make sure to thoroughly read the API Gateway [limits](https://docs.aws.amazon.com/apigateway/latest/developerguide/limits.html) ahead of time; I promise that will be time well spent!

