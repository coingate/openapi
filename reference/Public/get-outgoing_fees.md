---
title: Get Outgoing Fees
excerpt: >-
  <b>Get Outgoing Fees</b>. Outgoing fees apply to all outgoing transactions,
  such as withdrawals, trader orders, and both refund requests and merchant
  refunds. CoinGate API provides various ways to retrieve these fees based on
  currency, crypto platform, or specific types of payments. You can use
  endpoints like <b>api/v2/outgoing_fees</b> to get an array of all enabled fees
  or filter it further with other parameters to get more specific information.
api:
  file: v2.json
  operationId: get-outgoing_fees
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: ''
---
## Request examples:

| Query                                                             | Response                                                                             |
| :---------------------------------------------------------------- | :----------------------------------------------------------------------------------- |
| `api/v2/outgoing_fees`                                            | Array of all **enabled** outgoing fees                                               |
| `api/v2/outgoing_fees?currency_id=1`                              | Array of all **enabled** outgoing fee by currency. Or empty array.                   |
| `api/v2/outgoing_fees?crypto_platform_id=1`                       | Array of all **enabled** outgoing fee by crypto platform. Or empty array.            |
| `api/v2/outgoing_fees?currency_id=1&crypto_platform_id=1`         | Hash of **enabled** outgoing fee. Or empty hash                                      |
| `api/v2/outgoing_fees?applied_for=void_transaction&currency_id=1` | Array of all **enabled** outgoing fee by  currency and payment_kind. Or empty array. |

> 📘 Filtering by `currency_id` and `crypto_platform_id`
> 
> When filtering by the query parameters `currency_id` and `crypto_platform_id` in conjunction, the response will yield a singular Outgoing Fee record hash. For further details, please refer to the provided response example.