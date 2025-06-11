---
title: API Overview
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
![CoinGate API Overview](https://files.readme.io/e318931-API_Overview.png)

1. Call [Create Order](./reference/create-order) API method to create an order in the CoinGate system.

2. CoinGate checks if the order is valid.

   2a. If the order is valid, CoinGate responds with 200 HTTP status and returns [order data](./doc/create-order). After receiving 200 HTTP status, you should redirect the shopper to **_payment_url_** address.

   2b. If the order is not valid, CoinGate returns 422 (or another) error HTTP status and an error message (see [Errors](./doc/common-errors)).

3. When the shopper pays for the order, CoinGate sends [Payment Callback/Payment Notification](./doc/payment-callback) to your **_callback_url_**, which is defined when creating the order (see [Create Order](./doc/create-order)). CoinGate also sends Payment Callback when order status is changed to canceled, expired or to any other status (see [Order Statuses](./doc/order-statuses)). Please note that payment notifications are sent using **POST** method.

## Environments

| Environment | URL |
|:------------|:----|
| **Live** | `https://api.coingate.com/v2` |
| **Sandbox** | `https://api-sandbox.coingate.com/v2` |

- If you wish to use **Live** environment, create an account and API credentials on https://coingate.com
- If you wish to use **Sandbox** environment, create an account and API credentials on https://sandbox.coingate.com

## Limits and Quotas

| Type | Limit |
|------|-------|
| Create Order | **500 per hour per business** (contact support to increase)<br/>This default value is the number of orders that can be created per hour. Reaching the limit will prevent further orders to be created before the hourly timer resets. |
| API Requests | **200 requests per minute** |

## API Requests

API Requests are used to query the CoinGate API (examples: [Create Order](./doc/create-order), [Get Order](./doc/get-order)).

To review your API Requests, login to your CoinGate account, then go to API » Requests.

API Request attributes:

- Action - Which API method was queried.
- Response - HTTP status returned by CoinGate.
- Parameters - Parameters used to query the CoinGate API.
- Response - Parameters returned by CoinGate.

![API Requests Interface](https://files.readme.io/B2ELvNVCT2unLKj4ewy8_api-requests.png)

## Payment Callbacks (Payment Notifications)

[Payment Callback](./doc/payment-callback) (Payment Notification) is a response which is sent after the order status changes (see [Order Statuses](./doc/order-statuses)). CoinGate sends the Payment Callback to merchant's **_callback_url_**, which is set during order creation (see [Create Order](./doc/create-order)).

To review your Payment Callbacks, login to your CoinGate account, then go to API » Payment Callbacks.

Payment Callback attributes:

- **Response Status** - HTTP status returned by merchant.
- **Response Data** - Data body returned by merchant.
- **Callback Params** - Parameters sent by CoinGate to merchant's **_callback_url_**.

![Payment Callbacks Interface](https://files.readme.io/cffb98c-callbacks.png)

## POST Request

In every POST method set **Content-Type: application/x-www-form-urlencoded** header.