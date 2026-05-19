---
title: Order Callback
deprecated: false
hidden: true
metadata:
  robots: index
---
When an order received through a Payment Channel changes status, CoinGate sends a structured callback to the URL configured on that Payment Channel (`callback_url`). The payload follows a versioned envelope (`event`, `object`, `data`) and includes everything a merchant needs for reconciliation: contact details, external identifiers, the payment address, blockchain transactions, fees, and the exchange rate.

A callback is sent every time the order transitions to one of these statuses:

| event                           | When it fires                                                     |
| :------------------------------ | :---------------------------------------------------------------- |
| order.status.confirming         | Incoming transaction detected, waiting for confirmations          |
| order.status.paid               | Order is fully paid (transactions sufficient and AML-cleared)     |
| order.status.invalid            | Order rejected (AML failure, payment failed, manual invalidation) |
| order.status.refunded           | Order fully refunded                                              |
| order.status.partially_refunded | Order partially refunded                                          |

**Request**

Envelope

| Field name | Type   | Description                                                            |
| :--------- | :----- | :--------------------------------------------------------------------- |
| event      | string | The transition that triggered this callback — `order.status.<status>`. |
| object     | string | Always "order".                                                        |
| data       | object | The order payload (see below).                                         |

`data`

<br />
