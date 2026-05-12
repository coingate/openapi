---
title: Billing Request Callback
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
A callback will be sent to the merchant's **callback_url** when the billing request is created or the status is changed

> 🚧 API Callback Documentation
>
> Read more about common callback functionalities in the [API Callbacks section](doc:api-callbacks).

CoinGate callback sends the data below:

| Name                    | Type        | Value                                                                             |
| :---------------------- | :---------- | :-------------------------------------------------------------------------------- |
| `id`                    | Integer     | Billing Request ID                                                                |
| `uuid`                  | String      | Generated UUID                                                                    |
| `status`                | String      | Billing Request status                                                            |
| `orded_id`              | Integer     | Order ID of a paid billing request.                                               |
| `title`                 | String      | Custom title of the request                                                       |
| `due_days`              | Integer     | Days after billing request will expired                                           |
| `callback_url`          | String      | Callback URL                                                                      |
| `send_email`            | Boolean     | If CoinGate will send an email to billing contact about request                   |
| `underpaid_cover_pct`   | String      | Underpaid coverage percentage by merchant.                                        |
| `created_at`            | String      | Date of blilling request creation.                                                |
| `billing_contact_id`    | Integer     | ID of [Billing Contact](doc:list-billing-contacts).                               |
| `price_currency`        | Hash        | id, symbol [Currency](doc:currencies). Currency of the invoice amount.            |
| `price_amount`          | String      | Requested amount                                                                  |
| `receive_currency`      | Hash        | id, symbol [Currency](doc:currencies). Currency that will be received on payment. |
| `receive_amount`        | String      | Receive amount                                                                    |
| `pay_currency`          | Hash        | id, symbol [Currency](doc:currencies) . Currency that was paid with.              |
| `pay_amount`            | String      | Paid amount                                                                       |
| `fees`                  | Array[Hash] | Applied fees                                                                      |
| `billing_request_items` | Hash        | [Biling Product ID](doc:list-billing-products), quantity                          |
| `billing_request_url`   | String      | URL of invoice.                                                                   |

An example of pending callback in JSON:

```json
{
  "id": 1,
  "uuid": "6d93326d-f386-4b90-ab35-1eaab2673ba7",
  "status": "pending",
	"order_id": null,
  "title": "Billing Request Example",
  "due_days": 1,
  "callback_url": "https://callback.com/exmaple",
  "send_email": true,
  "underpaid_cover_pct": "0.0",
  "created_at": "2024-10-02T13:16:49Z",
  "billing_contact_id": 1,
  "billing_request_items": [
    {
      "id": 4,
      "billing_product_id": 1,
      "quantity": 2
    },
    {
      "id": 5,
      "billing_product_id": 1,
      "quantity": 1
    }
  ],
  "price_currency": {
    "id": 2,
    "symbol": "EUR"
  },
  "price_amount": "20.0",
  "receive_currency": {},
  "receive_amount": null,
  "pay_currency": {},
  "pay_amount": null,
  "fees": []
  "billing_request_url": ""
}
```

An example of completed callback in JSON

```json json
{
  "id": 3,
  "uuid": "a88d2edc-16be-4b1b-bfdf-bf62f302dca4",
  "status": "completed",
	"order_id": 27365192,
  "title": "20 eur",
  "due_days": 30,
  "callback_url": "https://callback.com/exmaple",
  "send_email": false,
  "underpaid_cover_pct": "0.0",
  "created_at": "2024-02-10T18:22:28.806Z",
  "billing_contact_id": 1,
  "external_contact_id": "1",
  "price_currency": {
    "id": 2,
    "symbol": "EUR"
  },
  "price_amount": "20.0",
  "receive_currency": {
    "id": 2,
    "symbol": "EUR"
  },
  "receive_amount": "19.8",
  "pay_currency": {
    "id": 1,
    "symbol": "BTC"
  },
  "pay_amount": "0.00022086",
  "fees": [
    {
      "type": "processing_fee",
      "amount": "0.2",
      "currency": {
        "id": 2,
        "symbol": "EUR"
      }
    }
  ],
  "billing_request_items": [],
  "billing_request_url": ""
}
```
