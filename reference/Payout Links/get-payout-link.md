---
api:
  file: v2.json
  operationId: get-payout-link
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Returns a single payout link by its `id`, with its current status, the amount reserved from your ledger account, the service fee, and the collect URL.

The same object is delivered to your `callback_url` on every status change — see [Payout Link Callback](https://developer.coingate.com/reference/payout-link-callback).
