---
title: Refund Binance Order
excerpt: ''
api:
  file: v2.json
  operationId: create-binance-order-refund
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# Refund orders paid via Binance Pay

Please note that this endpoint is only available for orders processed by Binance, please refer to the `payment_gateway` attribute on the order. This is similar to [POST Create Order Refund endpoint](https://developer.coingate.com/reference/create-refund) except you do not need to submit address, crypto platform and related payment information.

Ledger account ID can be found by making a [GET List Accounts ](https://developer.coingate.com/reference/accounts)request and finding the ledger account ID associated with the currency in which the refund will be issued.

❗To create requests within the CoinGate system the user should have an authentication token. To get it, please follow the instructions here.
