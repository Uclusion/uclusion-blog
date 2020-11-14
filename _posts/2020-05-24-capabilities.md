---
layout: post
title:  "Capabilities and JWT Security"
author: ben
categories: [ engineering, backend ]
---
Security for products like [Uclusion](https://www.uclusion.com/?utm_source=uclusion&utm_medium=blog&utm_campaign=devcapability), is a tricky beast. You need to provide a robust security model, but you don’t have a lot of wall clock time you can spend validating a request or user experience begins to suffer. This means that whatever scheme you come up has to be fast to verify, and ideally doesn’t require you to make round trips to databases or external resources.

Enter the [Capability](https://en.wikipedia.org/wiki/Capability-based_security). Capabilities don’t follow the normal security model where each recipient authenticates the user, and then checks the request against some permission authority (such as a permissions table stored in a DB) to determine if the request can be granted. Instead the user presents a capability containing a permission to the endpoint, the endpoint checks the syntactic structure of the capability, checks that the capability was granted by an authority it trusts, checks the request against the provided capability, and them, if everything matches, performs the action.

This scheme raises a some important questions however.

1. How do does the user get the capability?

1. How does the the recipient verify the capability was issued by a trusted authority?

1. How do you prevent the user from *forging* a capability granting them a permission that they don’t actually have.

1. How do you revoke access once granted?

1. What happens if a user shares the capability with another user?

Fortunately, the web have some technologies in common use that make answering these fairly easy:

First, for question 1: The user gets the capability from your service. That is, you can provide them via login or other fetch or list calls. You *must* make sure that whatever issues those capabilities takes into account your security model, and that all the checks you’d make in the other model are covered. Also, it generally requires front ends to request and store capabilities before using them, but we have IndexDB and local storage to solve that problem.

Questions 2 and 3 are easily solved via [JSON Web Tokens](https://jwt.io/), because JWTs aren’t valid unless they are cryptographically signed, and your capability issuing authority can keep it’s signing key to itself. JWTs also go a long way to solving question 4, because they also contain an expiration time, after which they must be refreshed. Combine that with signing key rotation, and there’s a very limited (or, if you’re willing to make users refetch the capabilities, zero length) window of opportunity for a revoked capability to be used.

Question 5, sharing of capabilities, is where serious thought arises. If your service has a model where if someone gets an email and clicks a link in that email, or steals a URL out of the users local storage VERY BAD THINGS HAPPEN, then you need to layer on some additional protections. A fairly straightforward thing to do is embed the user’s unique ID in the capability, and check it against the user who’s making the request. This doesn’t 100% protect you, but you’ve reduced the problem to an attacker who can make requests with that users identity, and has access to their email or local browser storage.

## Practical Considerations:

1: Capabilities can encode whatever data you want

With JWT based capabilities you can embed whatever additional information is required to make processing fast. For instance Uclusion embeds lots of information about the user’s relationship to an object (e.g. are they the creator) to prevent looking things up in the database. In some instances we can perform a fully secured and authenticated request without hitting our DynamoDB layer at all.

2: Login is the best time to issue capabilities

Internally, we model the top level of our object hierarchy with it’s own ID, and access to any subsequent resource in a, for example, Workspace requires you to possess the capability for the Workspace. We issue those when you sign into the app, and this allows us to do a simple exchange of JWT tokens based on Cognito’s identity token. High level it looks like:

![Login to Workspace flow for Uclusion](https://cdn-images-1.medium.com/max/2760/1*zbUmx8crF-R6sexSOQQw6g.png)*Login to Workspace flow for Uclusion*

And the code looks like:

    ... the validation context is populated using the capability...
    claims = get_claims(data['id_token'])
    market_id = data.get('market_id', None)
    external_id = claims['sub']
    
    .... figure out the user from the external id, and populate account and role data with db lookups ....

    
    def post_validation_function(event, data, context, validation_context):
        user = validation_context['user']
        account = validation_context['account']
        market_type = validation_context['market_type']
        api_key = None
        if 'api_key' not in account:
            api_key = get_api_key(account)
        is_admin = validation_context.get('is_admin', None)
        login_capability, is_new = create_login_capability(user['id'], market_id, api_key, is_admin, market_type, ...some other stuff...)

                                                                                                             
    return {'uclusion_token': login_capability, 'market_id': market_id, 'user': user, 'is_new_capability': is_new,
                'account': account,
                'user_created': validation_context['user_created']}
