---
title: Checkout
excerpt: ''
api:
  file: v2.json
  operationId: binance-checkout
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: ''
---
# White-label invoices using Binance Checkout method

Using Binance Checkout method, invoices can be white-labelled and integrated into your website, without redirecting the customer to CoinGate and receiving payments through Binance Pay.

This is achieved by using one of the available Binance Pay attributes: `qr_code_link`, `qr_content`, `checkout_url`, `deep_link` or `universal_url`. Binance recommends using `universal_url`. 

Please be aware that order should be created in advance through [create order endpoint](https://developer.coingate.com/reference/create-order) with `order_id`, `success` and `cancel` urls provided. You may experience some webhook callbacks delay, so we **highly** **recommend** using [get order endpoint](https://developer.coingate.com/reference/get-order) to retrieve latest updates once user lands on `success` or `cancel` url. 

In case of cancelation, Binance only redirects the user to provided url without cancelling the order, so to fully cancel the order, please use [cancel Binance order endpoint](https://developer.coingate.com/reference/binance-cancel).
