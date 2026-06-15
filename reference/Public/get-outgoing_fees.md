---
api:
  file: v2.json
  operationId: get-outgoing_fees
hidden: true
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: ''
---
## Request examples:

| Query                                                             | Response                                                                              |
| :---------------------------------------------------------------- | :------------------------------------------------------------------------------------ |
| `api/v2/outgoing_fees`                                            | Array of all **enabled** outgoing fees                                                |
| `api/v2/outgoing_fees?currency_id=1`                              | Array of all **enabled** outgoing fee by currency. Or empty array.                    |
| `api/v2/outgoing_fees?crypto_platform_id=1`                       | Array of all **enabled** outgoing fee by crypto platform. Or empty array.             |
| `api/v2/outgoing_fees?currency_id=1&crypto_platform_id=1`         | Hash of **enabled** outgoing fee. Or empty hash                                       |
| `api/v2/outgoing_fees?applied_for=void_transaction&currency_id=1` | Array of all **enabled** outgoing fee by  currency and payment\_kind. Or empty array. |

> 📘 Filtering by `currency_id` and `crypto_platform_id`
>
> When filtering by the query parameters `currency_id` and `crypto_platform_id` in conjunction, the response will yield a singular Outgoing Fee record hash. For further details, please refer to the provided response example.