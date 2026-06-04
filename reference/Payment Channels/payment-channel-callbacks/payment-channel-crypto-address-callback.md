---
title: Crypto Address Callback
deprecated: false
hidden: false
metadata:
  robots: index
---
Sent when a deposit address attached to your payment channel changes status — for example, from `enqueued` to `active` once the crypto daemon finishes generating it.

CoinGate sends a structured callback to the URL configured on the parent Payment Channel (`callback_url`). The payload follows a versioned envelope (`event`, `object`, `data`) and includes everything you need to track the address lifecycle: the address, its currency and platform, memo, expiry, status, and the parent payment channel ID.

**Request**

| Property     | Value                                       |
| :----------- | :------------------------------------------ |
| Method       | `POST`                                      |
| URL          | The Payment Channel's `callback_url`        |
| Content-Type | `application/json`                          |
| User-Agent   | `CoinGate Payment Channel Address Callback` |
| Body         | JSON object — see Payload below             |

**Payload**

```json
{
  "event": "payment_channel_address.status.active",
  "object": "payment_channel_address",
  "data": {
    "currency_id": 1,
    "platform_id": 4,
    "address": "bc1qexampledepositaddress00000000000000000",
    "memo": "",
    "expires_at": null,
    "status": "active",
    "payment_channel_id": 61
  }
}
```

**When the callback fires**

| Status   | Meaning                                                                                                                                                                 |
| :------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| enqueued | Generation requested. address is `null`. No funds can land here yet.                                                                                                    |
| active   | Generation complete. `address` is populated. Ready to receive deposits.                                                                                                 |
| expired  | Address was rotated and is no longer accepting deposits. Request a fresh address from the payment channel before showing the next deposit instructions to the customer. |

You will not receive an address callback for funds movement on the address — that's the [Order callback's](https://developer.coingate.com/reference/payment-channel-order-callback) job.
