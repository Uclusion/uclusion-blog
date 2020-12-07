---
layout: post
title:  "Working with Stripe Promotion Codes"
author: ben
categories: [ engineering ]
image: assets/images/20_percent_off.jpg
featured: false
---

Uclusion uses Stripe for it's subscription service, and August Stripe added
[promotion code support to recurring subscriptions](https://support.stripe.com/questions/promotion-codes).

Unfortunately Stripe's support is fairlyy limited, and there's several "gotchas" to watch out for:

1. While you can set overall redemption limits you can't set a redemption limit per customer.
1. Promotions do not play well with trial period. If you create a promotion good for three months,
then the promotion ends exactly three months after the customer applies the promotion.
1. A customer can only have one promotion active at a time, and adding a new one overwrites the current.
1. Stripe does not track the history of codes the customer has used.

Taken together, this means about all Stripe is going to do for you is provide a nice UI for creating
codes, and discount your invoices appropriately for the active code. In order to ensure customer
friendly behavior you'll have to write your own promotion redemption and application system. You'll also
need that integrate that system with  Stripe's Webhooks to know when to apply the next code.

### How Uclusion does it ###
Uclusion tracks codes by augmenting the customer's `Account` object with a promo code list which is
added to via a redemption button on their account management page.

Each promo code looks like this in PynamoDB:
```
    code = UnicodeAttribute(null=False)
    duration = UnicodeAttribute(null=False)
    months = NumberAttribute(null=False)
    percent_off = NumberAttribute(null=False)
    consumed = BooleanAttribute(default=False)
    application_date = UTCDateTimeAttribute(null=True)
```
We then listen for the following [Webhook Events](https://stripe.com/docs/api/events) from stripe to apply or remove codes
```
    invoice.payment_succeeded
    invoice.upcoming
    customer.subscription.trial_will_end
    customer.subscription.deleted
    customer.subscription.updated
    customer.subscription.created
```
The operations themselves are fairly simple. When we receive an event, say `customer.subscription.deleted`
we check the state of the subscription block for any active discount, and if it's ending soon, look through the account's
promo code list for a new promotion we can apply. If we find it, we first check if it's still valid, and then apply it to Stripe and
update our DB to mark it's been consumed.
```
  # promotions_changed tells us if we need to bother making a actual call to the db
  promotions_changed = False
  for promotion in account.billing_promotions :
        if not promotion.consumed:
            promotion.consumed = True
            promo = lookup_promo_code(stripe, promotion.code)
            if promo is None:
                # just consume it since it's no longer usable
                promotion.consumed = True
                # set promotions changed because we consumed
                promotions_changed = True
            else:
                stripe.Subscription.modify(subscription_id, promotion_code=promo['id'])
                promotion.consumed = True
                promotion.application_date = datetime.now(timezone.utc)
                return True  # we can early stop here since we found one
  return promotions_changed
```
As always, if you have any questions of this code feel free to drop us a line.
