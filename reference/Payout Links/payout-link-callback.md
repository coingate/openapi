---
title: Payout Link Callback
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
When you set `callback_url` on a payout link, CoinGate sends a `POST` to that URL when the link is created and again on every status change. The `callback_url` must be a direct URL without redirects.

> 📘 API Callback Documentation
>
> Read more about common callback functionality, including retries, in the [API Callbacks section](doc:api-callbacks).

The request carries the `CoinGate Payout Link Callback` user agent and, by default, a JSON body. If your API app is configured to send callbacks as form data, the same fields arrive URL-encoded instead.

## Payload

The body is the same payout link object that [Get Payout Link](https://developer.coingate.com/reference/get-payout-link) returns, so every field is documented there. `status` is the field to act on — see [Payout Link Statuses](https://developer.coingate.com/reference/payout-link-statuses).

```json
{
  "id": 11,
  "uuid": "0f9d3f0e-6d2f-4a1c-9c7e-5f4b2c1d8e30",
  "status": "completed",
  "ledger_account_id": "01JNQWKKJ6WXN8BZT1Y66B6G9H",
  "purpose": "Invoice 42",
  "external_id": "ext-1",
  "recipient_email": "recipient@example.com",
  "send_email": true,
  "payout_link_url": "https://payout.coingate.com/0f9d3f0e-6d2f-4a1c-9c7e-5f4b2c1d8e30",
  "callback_url": "https://example.com/callback_url",
  "expires_at": "2026-08-31T23:59:59.999Z",
  "claimed_at": "2026-08-26T09:02:41.115Z",
  "created_at": "2026-08-24T10:15:00.000Z",
  "input_amount": "20.0",
  "input_currency": {
    "id": 34,
    "title": "Tether USD",
    "kind": "crypto",
    "symbol": "USDT",
    "enabled": true,
    "disabled_message": null
  },
  "balance_debit_amount": "20.0",
  "balance_debit_currency": {
    "id": 34,
    "title": "Tether USD",
    "kind": "crypto",
    "symbol": "USDT",
    "enabled": true,
    "disabled_message": null
  },
  "fees": {
    "service_fee": {
      "amount": "0.2",
      "currency": {
        "id": 34,
        "title": "Tether USD",
        "kind": "crypto",
        "symbol": "USDT",
        "enabled": true,
        "disabled_message": null
      }
    }
  }
}
```

Use `external_id` to match the callback against your own record, and treat repeated deliveries of the same status as duplicates.
