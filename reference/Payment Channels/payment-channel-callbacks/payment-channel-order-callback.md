---
title: Order Callback
deprecated: false
hidden: false
metadata:
  robots: index
---
<br />

<Callout icon="📘" theme="info">
  Payment Channels are ready to use. Access is granted on request — to request access, contact our sales team via <Anchor label="CoinGate Payment Channels" target="_blank" href="https://coingate.com/payment-channels">CoinGate Payment Channels</Anchor>.
</Callout>

When an order received through a Payment Channel changes status, CoinGate sends a structured callback to the URL configured on that Payment Channel (`callback_url`). The payload follows a versioned envelope (`event`, `object`, `data`) and includes everything a merchant needs for reconciliation: contact details, external identifiers, the payment address, blockchain transactions, fees, and the exchange rate.

> 📘 API Callback Documentation
>
> The callback is delivered as a `POST` request with a `application/json` body. For shared callback behavior — retry policy, IP allowlist, manual resend — see the <Anchor label="API Callbacks " target="_blank" href="https://developer.coingate.com/reference/api-callbacks">API Callbacks </Anchor>reference.

A callback is sent every time the order transitions to one of these statuses:

| event                           | When it fires                                                     |
| :------------------------------ | :---------------------------------------------------------------- |
| order.status.confirming         | Incoming transaction detected, waiting for confirmations          |
| order.status.paid               | Order is fully paid (transactions sufficient and AML-cleared)     |
| order.status.invalid            | Order rejected (AML failure, payment failed, manual invalidation) |
| order.status.refunded           | Order fully refunded                                              |
| order.status.partially_refunded | Order partially refunded                                          |

**Request**

| Property     | Value                                     |
| :----------- | :---------------------------------------- |
| Method       | `POST`                                    |
| URL          | The Payment Channel's `callback_url`      |
| Content-Type | `application/json`                        |
| User-Agent   | `CoinGate Payment Channel Order Callback` |
| Body         | JSON object — see Payload below           |

**Payload**

```json
{
  "event": "order.status.paid",
  "object": "order",
  "data": {
    "id": 390104,
    "status": "paid",
    "address": "bc1qexample...",
    "contact": {
      "id": 123,
      "type": "business",
      "company_name": "Acme Corp",
      "external_contact_id": "shop_user_123"
    },
    "price": {
      "amount": "10.00",
      "currency": { "id": 2, "title": "Euro", "symbol": "EUR" }
    },
    "pay": {
      "amount": "0.00016069",
      "currency": {
        "id": 1,
        "title": "Bitcoin",
        "symbol": "BTC",
        "platform": { "id": 6, "title": "Bitcoin" }
      },
      "exchange_rate": {
        "to_currency": { "id": 2, "title": "Euro", "symbol": "EUR" },
        "value": "62000.00"
      }
    },
    "receive": {
      "amount": "9.00",
      "currency": { "id": 2, "title": "Euro", "symbol": "EUR" },
      "exchange_rate": {
        "to_currency": { "id": 2, "title": "Euro", "symbol": "EUR" },
        "value": "1.0"
      }
    },
    "payment_channel": {
      "id": 456,
      "purpose": "merchant_payment"
    },
    "blockchain_transactions": [
      {
        "id": 123,
        "txid": "5c1a0a92-9a3d-4107-9a00-8d6a2a4b6620",
        "amount": "0.00001234",
        "status": "confirmed",
        "network_confirmations": 6,
        "currency": {
          "id": 1,
          "title": "Bitcoin",
          "symbol": "BTC",
          "platform": { "id": 6, "title": "Bitcoin" }
        }
      }
    ],
    "fees": [
      {
        "type": "processing_fee",
        "amount": "0.000002",
        "currency": { "id": 1, "symbol": "BTC" }
      }
    ],
    "paid_at": "2026-04-30T14:04:32+00:00"
  }
}
```

> 📘 Exchange rate
>
> `exchange_rate.value` is the rate to convert into `exchange_rate.to_currency` (the order's price currency). The `exchange_rate` object is omitted entirely when no rate applies to that side. `pay.currency.platform` identifies the blockchain the paid asset settled on.

<br />
