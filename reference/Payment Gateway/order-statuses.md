---
title: Order Status
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
  pages:
    - type: link
      title: What’s a merchant refund feature & how to use it?
      url: https://coingate.com/blog/post/merchant-refund
    - type: link
      title: ' My customer overpaid for his order. How do I issue refunds? '
      url: https://support.coingate.com/hc/en-us/articles/4402499190418
    - type: link
      title: ' Is it possible to complete an order after it has been canceled or expired? '
      url: https://support.coingate.com/hc/en-us/articles/10420045425948
---
[block:parameters]
{
  "data": {
    "h-0": "Status",
    "h-1": "Description",
    "0-0": "new",
    "0-1": "Newly created invoice. The shopper has not yet selected a [payment currency](https://developer.coingate.com/reference/currencies) or [crypto platform](https://developer.coingate.com/reference/platforms). If the shopper does not make a selection, the order status will eventually change to Expired 2 hours after the order creation time.",
    "1-0": "pending",
    "1-1": "The shopper has selected a payment currency and crypto platform. Awaiting payment. If the shopper does not complete the payment within 20 minutes, the order status will change to Expired.",
    "2-0": "confirming",
    "2-1": "Shopper transferred the payment for the invoice. Awaiting blockchain network confirmation.",
    "3-0": "paid",
    "3-1": "Payment is confirmed by the network, and has been credited to the merchant. Purchased goods/services can be safely delivered to the shopper.",
    "4-0": "invalid",
    "4-1": "The payment was either not confirmed by the blockchain network or was marked as invalid due to AML/CTF compliance reasons.",
    "5-0": "expired",
    "5-1": "An order will expire in the following cases:  \n  \n- For a new order: the shopper does not select a payment currency and crypto platform within 2 hours.\n- For a pending order: the shopper does not complete the payment within 20 minutes.",
    "6-0": "canceled",
    "6-1": "Shopper canceled the invoice.",
    "7-0": "refunded",
    "7-1": "Payment was refunded to the shopper. [Read more about refunds](https://coingate.com/blog/post/merchant-refund)",
    "8-0": "partially_refunded",
    "8-1": "Payment was partially refunded to the shopper. [Read more about refunds](https://coingate.com/blog/post/merchant-refund)"
  },
  "cols": 2,
  "rows": 9,
  "align": [
    "left",
    "left"
  ]
}
[/block]


## Order Status Changing Flow

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/28732a5-Order_Status_Changing_Flow4.png",
        "",
        "CoinGate Paymnet Statuses flow"
      ],
      "align": "center"
    }
  ]
}
[/block]