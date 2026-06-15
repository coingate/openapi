---
api:
  file: v2.json
  operationId: refund-supported-currencies
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
This endpoint returns the list of supported currencies and platforms available for processing merchant refunds.

It is required by the [Create Order Refund](https://developer.coingate.com/reference/create-refund) endpoint, where you must specify both the _currency_id_ and _platform_id_ when initiating a refund.

For a detailed overview of the merchant refund feature, <Anchor label="read this article" target="_blank" href="https://coingate.com/blog/post/merchant-refund">read this article</Anchor>.