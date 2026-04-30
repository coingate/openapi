---
title: Payment Callback
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
Payment callback (Payment notification) will be sent to merchant's _**callback_url**_ when [order status](https://developer.coingate.com/reference/order-statuses) is changed to _pending_ _confirming_, _paid_, _invalid_, _canceled_, _refunded_ or _expired_.

> 📘 API Callback Documentation
>
> About common callback functionality please read in [API Callbacks section](https://developer.coingate.com/reference/api-callbacks).
>
> **Recommended**: use JSON callbacks. JSON is easier to parse, preserves nested structures (like `fees[]`) without bracket-notation quirks, and matches the format of every other CoinGate API response. You can switch your API App's callback format from Form Encoding to JSON at any time — see [API Callbacks](https://developer.coingate.com/reference/api-callbacks) for instructions. The format is configured per API App, not per order.

CoinGate callback sends data below:

| Name               | Type     | Value                                                                                                                                                                                                                                                                                                                                                                         |
| :----------------- | :------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`               | integer  | CoinGate order ID.                                                                                                                                                                                                                                                                                                                                                            |
| `order_id`         | string   | Merchant-supplied order identifier.                                                                                                                                                                                                                                                                                                                                           |
| `status`           | string   | CoinGate [payment status](https://developer.coingate.com/reference/order-statuses).                                                                                                                                                                                                                                                                                           |
| `price_amount`     | string   | The price set by the merchant; for example, _499.95_.                                                                                                                                                                                                                                                                                                                         |
| `price_currency`   | string   | The currency code which defines the currency in which the merchant's goods/services are priced; for example, _USD_, _CHF_, _BTC_ (see [supported currencies](https://coingate.com/supported-currencies)).                                                                                                                                                                     |
| `receive_currency` | string   | The currency code which defines the currency in which the merchant's settlements will be paid. Currency conversions are done by CoinGate automatically. For example: _EUR_, _USD_, _BTC_, _USDT_, etc.                                                                                                                                                                        |
| `receive_amount`   | string   | The amount which will be credited to the merchant when the invoice is paid. It is calculated by taking the `price` amount (converted to currency units set in `receive_currency`) and subtracting CoinGate processing fee from it.                                                                                                                                            |
| `pay_amount`       | string   | The amount of cryptocurrency (defined by `pay_currency`) paid by the shopper.                                                                                                                                                                                                                                                                                                 |
| `pay_currency`     | string   | The cryptocurrency in which the payment was made; for example, _BTC_, _LTC_, _ETH_.                                                                                                                                                                                                                                                                                           |
| `underpaid_amount` | string   | The amount of cryptocurrency (defined by `pay_currency`) underpaid by the shopper; for example, if `pay_amount => 0.123`, `pay_currency => BTC`, and the shopper paid 0.12 BTC, then `underpaid_amount => 0.003`. Changes in `underpaid_amount` will not trigger additional callbacks, but when order information is retrieved using GET or LIST, latest value will be shown. |
| `overpaid_amount`  | string   | The amount of cryptocurrency (defined by `pay_currency`) overpaid by the shopper; for example, if `pay_amount => 0.123`, `pay_currency => BTC`, and the shopper paid 0.15 BTC, then `overpaid_amount => 0.027`. Changes in `overpaid_amount` will not trigger additional callbacks, but when order information is retrieved using GET or LIST, latest value will be shown.    |
| `is_refundable`    | boolean  | Possible values: _true_, _false_. Indicates whether or not the shopper can request a refund on the invoice. Changes in `is_refundable` will not trigger additional callbacks, but when order information is retrieved using GET or LIST, latest value will be shown.                                                                                                          |
| `created_at`       | ISO 8601 | Invoice creation time.                                                                                                                                                                                                                                                                                                                                                        |
| `token`            | string   | The same callback token returned when the order was created — use it to verify the request is genuine.                                                                                                                                                                                                                                                                        |
| `fees`             | array    | Array of fees for _Paid_/_Refunded_/_Partially refunded_ order                                                                                                                                                                                                                                                                                                                |
| `paid_at`          | ISO 8601 | Time when the invoice was fully paid. Only included when the status is paid, refunded, or partially_refunded.                                                                                                                                                                                                                                                                 |

Fields `pay_currency, pay_amount, expire_at, payment_address` are **only sent** when the customer chooses the currency with which he is going to pay for the invoice.

```php Format 1 — JSON (recommended)
{
  "id": 390104,
  "order_id": "test-json-1777557839",
  "status": "paid",
  "price_amount": "10.0",
  "price_currency": "EUR",
  "pay_amount": "0.00016069",
  "pay_currency": "BTC",
  "receive_amount": "0.000152",
  "receive_currency": "BTC",
  "underpaid_amount": "0.00016069",
  "overpaid_amount": "0",
  "is_refundable": false,
  "created_at": "2026-04-30T14:03:59+00:00",
  "paid_at": "2026-04-30T14:04:32+00:00",
  "token": "R3avx2xNb-7onqeCDLa9-S5Dszt8bw",
  "fees": [
    {
      "type": "processing_fee",
      "amount": "0.000002",
      "currency": { "id": 1, "symbol": "BTC" }
    }
  ]
}
```
```Text Format 2 — Form-encoded (legacy)
id=390087
&order_id=test-1777557082
&status=paid
&pay_amount=0.00016055
&pay_currency=BTC
&price_amount=10.0
&price_currency=EUR
&receive_currency=BTC
&receive_amount=0.000152
&created_at=2026-04-30T13%3A51%3A23%2B00%3A00
&paid_at=2026-04-30T13%3A52%3A33%2B00%3A00
&token=knPmMCmFPgWasTQfqGkUoFDZgm3ZLw
&underpaid_amount=0.00016055
&overpaid_amount=0
&is_refundable=false
&fees[][type]=processing_fee
&fees[][amount]=0.000002
&fees[][currency][id]=1
&fees[][currency][symbol]=BTC
```

<br />
