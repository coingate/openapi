---
title: Create Order
excerpt: Create order at CoinGate and redirect shopper to invoice (payment_url).
api:
  file: v2.json
  operationId: create-order
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
> 📘 API authentication is required
>
> To create requests within the CoinGate system, the user must have an authentication token. To obtain one, follow the instructions provided [here](https://developer.coingate.com/reference/api-authentication).

The order is placed with the "Create Order" API method. From the user's point of view, at the moment of creating the order, the user is redirected to (*payment\_url*) our payment page (invoice), where shopper can see the payment amount, select the desired payment currency and complete the payment.

Note on the *receive\_currency* parameter - this is your settlement currency. When EUR is selected, all your received payments are immediately settled on exchanges to guarantee a fixed payout for each order. By selecting BTC, ETH, LTC or BCH as your settlement currency, you will automatically be credited with the chosen cryptocurrency (e.g. if BTC is your receive\_currency and your customer pays with ETH, you will be credited BTC according to the real-time market rate locked at the moment the invoice is generated). To keep the coins which your customers pay with, use DO\_NOT\_CONVERT as your receive\_currency (e.g. if a customer pays in BTC, you will be credited BTC, and if the customer pays in ETH, you will be credited with ETH). Please contact our support for further clarification, if needed.
