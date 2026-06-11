---
api:
  file: v2.json
  operationId: void-request
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Initiate a refund for a [void transaction](https://support.coingate.com/hc/en-us/articles/4902938327964), typically when:

* An order was overpaid,
* A transaction was received for a canceled or expired order, and
* The refundable amount exceeds the minimum threshold specified in the [Platforms API](https://developer.coingate.com/reference/platforms).