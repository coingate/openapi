---
title: Refund Callback
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
A refund callback will be sent to the merchant's **callback_url** when the merchant refund is created or the status is changed to processing, rejected or completed.

> 🚧 API Callback Documentation
>
> Read more about common callback functionalities in the [API Callbacks section](doc:api-callbacks).

CoinGate callback sends the data below:

| Name                                          | Type    | Value                                                                                                                                                                                                                             |
| :-------------------------------------------- | :------ | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`                                          | Integer | CoinGate merchant refund ID                                                                                                                                                                                                       |
| `order_id`                                    | Integer | CoinGate order ID assigned to the merchant refund                                                                                                                                                                                 |
| `status`                                      | String  | CoinGate merchant refund status                                                                                                                                                                                                   |
| `request_amount`                              | String  | Amount requested to refund                                                                                                                                                                                                        |
| `request_currency`                            | Hash    | [Currency](doc:currencies) id and symbol                                                                                                                                                                                          |
| `address`                                     | String  | Customer’s wallet address where the refund will be sent                                                                                                                                                                           |
| `additional_address_field`                    | String  | Address memo or destination tag                                                                                                                                                                                                   |
| `refund_amount`                               | String  | Amount to refund a customer                                                                                                                                                                                                       |
| `refund_currency`                             | Hash    | [Currency](doc:currencies) id, symbol, [platform](doc:platforms) id, and title                                                                                                                                                    |
| `email`                                       | String  | Customer’s email address                                                                                                                                                                                                          |
| `reason`                                      | String  | Reason for refund                                                                                                                                                                                                                 |
| `ledger_account`                              | Hash    | [Ledger](doc:ledger-accounts) id, [currency](doc:currencies) id, and symbol                                                                                                                                                       |
| **(Deprecated)**`compliance_rejection_reason` | String  | Reason for compliance rejection. Only included when the refund status is `rejected`. **Deprecated in favor of rejection_type and rejection_reason.**                                                                              |
| `rejection_type`                              | String  | This field is included when the refund status is `rejected` and a reason is provided. Type of rejection. Possible values: `compliance`, `merchant`, `shopper`. Will be added then refund status is rejected and reason is present |
| `rejection_reason`                            | String  | This field is included when the refund status is rejected and a reason is provided.  Reason why the refund was rejected.                                                                                                          |

An example of callback in JSON:

```json Completed
{
  "id": 123,
  "order_id": 124,
  "status": "completed",
  "request_amount": "123.0",
  "request_currency": {
    "id": 2,
    "symbol": "EUR"
  },
  "address": "mvKFTr6M8NtKrD659qBCpT9hfM1LTwnQV3",
  "additional_address_field": null,
  "refund_amount": "0.00012345",
  "refund_currency": {
    "id": 1,
    "symbol": "BTC",
    "platform": {
      "id": 6,
      "title": "Bitcoin"
    }
  },
  "email": "test@example.com",
  "reason": "Callbacks Testing Reason",
  "ledger_account": {
    "id": "01HBDE32A9FKNJT5S8MYFFYY6JJ",
    "currency": {
      "id": 1,
      "symbol": "BTC"
    }
  }
}

```
```json Rejected
{
  "id": 123,
  "order_id": 124,
  "status": "rejected",
  "request_amount": "123.0",
  "request_currency": {
    "id": 2,
    "symbol": "EUR"
  },
  "address": "mvKFTr6M8NtKrD659qBCpT9hfM1LTwnQV3",
  "additional_address_field": null,
  "refund_amount": "0.00012345",
  "refund_currency": {
    "id": 1,
    "symbol": "BTC",
    "platform": {
      "id": 6,
      "title": "Bitcoin"
    }
  },
  "email": "test@example.com",
  "reason": "Callbacks Testing Reason",
  "ledger_account": {
    "id": "01HBDE32A9FKNJT5S8MYFFYY6JJ",
    "currency": {
      "id": 1,
      "symbol": "BTC"
    }
  },
  "rejection_type": "compliance",
  "rejection_reason": "Rejected by Compliance due to regulatory or risk concerns."
}

```
