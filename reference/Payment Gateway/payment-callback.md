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
Payment callback (Payment notification) will be sent to merchant's ***callback\_url*** when [order status](https://developer.coingate.com/reference/order-statuses) is changed to *pending* *confirming*, *paid*, *invalid*, *canceled*, *refunded* or *expired*.

> 📘 API Callback Documentation
>
> About common callback functionality please read in [API Callbacks section](https://developer.coingate.com/reference/api-callbacks).

CoinGate callback sends data below:

| Name               | Value                                                                                                                                                                                                                                                                                                                                                                         |
| :----------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`               | CoinGate order (invoice) ID.                                                                                                                                                                                                                                                                                                                                                  |
| `order_id`         | Custom order ID of the merchant. Should be used to identify order or invoice number.                                                                                                                                                                                                                                                                                          |
| `status`           | CoinGate [payment status](https://developer.coingate.com/reference/order-statuses).                                                                                                                                                                                                                                                                                           |
| `price_amount`     | The price set by the merchant; for example, *499.95*.                                                                                                                                                                                                                                                                                                                         |
| `price_currency`   | The currency code which defines the currency in which the merchant's goods/services are priced; for example, *USD*, *CHF*, *BTC* (see [supported currencies](https://coingate.com/supported-currencies)).                                                                                                                                                                     |
| `receive_currency` | The currency code which defines the currency in which the merchant's settlements will be paid. Currency conversions are done by CoinGate automatically. For example: *EUR*, *USD*, *BTC*, *USDT*, etc.                                                                                                                                                                        |
| `receive_amount`   | The amount which will be credited to the merchant when the invoice is paid. It is calculated by taking the `price` amount (converted to currency units set in `receive_currency`) and subtracting CoinGate processing fee from it.                                                                                                                                            |
| `pay_amount`       | The amount of cryptocurrency (defined by `pay_currency`) paid by the shopper.                                                                                                                                                                                                                                                                                                 |
| `pay_currency`     | The cryptocurrency in which the payment was made; for example, *BTC*, *LTC*, *ETH*.                                                                                                                                                                                                                                                                                           |
| `underpaid_amount` | The amount of cryptocurrency (defined by `pay_currency`) underpaid by the shopper; for example, if `pay_amount => 0.123`, `pay_currency => BTC`, and the shopper paid 0.12 BTC, then `underpaid_amount => 0.003`. Changes in `underpaid_amount` will not trigger additional callbacks, but when order information is retrieved using GET or LIST, latest value will be shown. |
| `overpaid_amount`  | The amount of cryptocurrency (defined by `pay_currency`) overpaid by the shopper; for example, if `pay_amount => 0.123`, `pay_currency => BTC`, and the shopper paid 0.15 BTC, then `overpaid_amount => 0.027`. Changes in `overpaid_amount` will not trigger additional callbacks, but when order information is retrieved using GET or LIST, latest value will be shown.    |
| `is_refundable`    | Possible values: *true*, *false*. Indicates whether or not the shopper can request a refund on the invoice. Changes in `is_refundable` will not trigger additional callbacks, but when order information is retrieved using GET or LIST, latest value will be shown.                                                                                                          |
| `created_at`       | Invoice creation time.                                                                                                                                                                                                                                                                                                                                                        |
| `token`            | Your custom token (or generated by CoinGate) to validate payment callback.                                                                                                                                                                                                                                                                                                    |
| `fees`             | Array of fees for *Paid*/*Refunded*/*Partially refunded* order                                                                                                                                                                                                                                                                                                                |
| `paid_at`          | Time when the invoice was fully paid. Only included when the status is paid, refunded, or partially\_refunded.                                                                                                                                                                                                                                                                |

Fields `pay_currency, pay_amount, expire_at, payment_address` are **only sent** when the customer chooses the currency with which he is going to pay for the invoice.

**Content-Type: application/x-www-form-urlencoded** 

```php
// print_r($_POST)

Array
(
    [id] => 343
    [order_id] => 14037
    [status] => paid
    [price_amount] => 1050.99
    [price_currency] => USD
    [receive_amount] => 926.73
    [receive_currency] => EUR
    [pay_amount] => 4.81849315
    [pay_currency] => BTC
    [created_at] => 2014-11-03T13:07:28+00:00
		[token] => ff7a7343-93bf-42b7-b82c-b38687081a4e
		[fees] => Array // only applies to paid/refunded/partially refunded order, otherwise empty Fee array
        (
            [0] => Array
                (
                    [type] => processing_fee
                    [amount] => 1.0
                    [currency] => Array
                        (
                            [id] => 2
                            [symbol] => EUR
                        )
                )
        )
)
```
