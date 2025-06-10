---
title: Create Mass Payout with quote currency
excerpt: ''
api:
  file: v2.json
  operationId: create-mass-payout-exchange
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
This endpoint is used to create a ***Mass Payout*** with currency exchange, e.g. providing quoting amounts in EUR and paying out in BTC. Once Mass Payout is created, the status is set to ***draft*** and HTTP callback is sent. No matter of the callback status, in order to proceed with ***confirmation***, you must check the latest Mass Payout information at [get Mass Payout endpoint](https://developer.coingate.com/reference/get-mass-payout). In case of agreement, Mass Payout must be confirmed at [confirm Mass Payout endpoint](https://developer.coingate.com/reference/confirm-mass-payout).
