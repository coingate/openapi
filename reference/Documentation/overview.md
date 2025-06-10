---
title: Overview
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: ''
---
> ❗️ API v1 is DEPRECATED
>
> API v1 is DEPRECATED and no longer maintained. Please use API v2 [http://developer.coingate.com/v2](http://developer.coingate.com/v2)

![2162](https://files.readme.io/7507b5a-coingate_api_diagram.jpg "coingate_api_diagram.jpg")

1. Call [Create Order](doc:create-order) API method to create an order in the CoinGate system.
2. CoinGate checks if the order is valid.
3. a) If the order is valid, CoinGate responds with 200 HTTP status and returns [order data](doc:create-order). After receiving 200 HTTP status, you should redirect the buyer to `payment_url` address.
4. b) If the order is not valid, CoinGate returns 422 (or other) [error](doc:common-errors) HTTP status and an error message.
5. When the buyer pays for the order, CoinGate sends [Payment Callback/Payment Notification](doc:payment-callback) to your `callback_url` url. `callback_url` is defined when [creating order](doc:create-order). CoinGate also sends [Payment Callback](doc:payment-callback) when order status is changed to canceled, expired or to any other status [read more about CoinGate order statuses](doc:order-statuses). Please note, that payment notifications are sent using **POST** method.

## Environments

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>

      </th>

      <th>

      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        **Live**
      </td>

      <td>
        `https://api.coingate.com/v1`
      </td>
    </tr>

    <tr>
      <td>
        **Sandbox**
      </td>

      <td>
        `https://api-sandbox.coingate.com/v1`
      </td>
    </tr>
  </tbody>
</Table>

* If you wish to use **Live** environment, use have to create an account and API credentials on [https://coingate.com](https://coingate.com)
* If you wish to use **Sandbox** environment, use have to create an account and API credentials on [https://sandbox.coingate.com](https://sandbox.coingate.com)

## Resources

* [Ruby Gem](https://rubygems.org/gems/coingate)
* [Coingate PHP](https://github.com/coingate/coingate-php)
* [Omnipay (PHP)](https://github.com/thephpleague/omnipay)
* [Ruby on Rails Shop Example](http://example.coingate.com/) / [Source Code](https://github.com/coingate/rails-shop-example)
* [PHP Laravel Shop Example](http://demo1.coingate.com/) / [Source Code](https://github.com/arnasfomenko/coingate-laravel-php-shop)
* [E-commerce Plugins](https://coingate.com/plugins)

## API Requests

API Request is used to query CoinGate API (examples: [Create Order](doc:create-order), [Get Order](doc:get-order)).

To review your API Requests, login to your CoinGate account, then go to API » Requests.

API Request attributes:

* Action - Which API method was queried.
* Response - HTTP status returned by CoinGate.
* Parameters - Parameters used to query CoinGate API.
* Response - Parameters returned by CoinGate.

![999](https://files.readme.io/B2ELvNVCT2unLKj4ewy8_api-requests.png "api-requests.png")

## API Request Limits

1,000 / hour per ip address for all API endpoints.

1 hour API limits per credentials by specific endpoint:

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Environment
      </th>

      <th>
        Endpoint
      </th>

      <th>
        Rate Limit
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Live
      </td>

      <td>
        POST /orders
      </td>

      <td>
        300 / hour
      </td>
    </tr>

    <tr>
      <td>
        Live
      </td>

      <td>
        GET /orders/:id
      </td>

      <td>
        500 / hour
      </td>
    </tr>

    <tr>
      <td>
        Live
      </td>

      <td>
        GET /orders
      </td>

      <td>
        500 / hour
      </td>
    </tr>

    <tr>
      <td>
        Sandbox
      </td>

      <td>
        POST /orders
      </td>

      <td>
        300 / hour
      </td>
    </tr>

    <tr>
      <td>
        Sandbox
      </td>

      <td>
        GET /orders/:id
      </td>

      <td>
        500 / hour
      </td>
    </tr>

    <tr>
      <td>
        Sandbox
      </td>

      <td>
        GET /orders
      </td>

      <td>
        500 / hour
      </td>
    </tr>
  </tbody>
</Table>

All other endpoints which is not described above the limit is 1,000 / hour per API credentials.

API limits can be manually increased for specific user. If you want change your API limits, please contact to support: [support@coingate.com](mailto:support@coingate.com).

API returns [429 HTTP error](doc:common-errors) if limit is exceeded.

## Payment Callbacks (Payment Notifications)

[Payment Callback](doc:payment-callback) (Payment Notification) is a response which is sent after order status is changed (see [Order Statuses](doc:order-statuses)). It is sent by CoinGate to merchant's ***callback\_url***, which is set during order creation (see [Create Order](doc:create-order)).

To review your Payment Callbacks, login to your CoinGate account, then go to API » Payment Callbacks.

Payment Callback attributes:

* **Response Status** - HTTP status returned by merchant.
* **Response Data** - Data body returned by merchant.
* **Callback Params** - Parameters sent by CoinGate to merchant's ***callback\_url***.

![1028](https://files.readme.io/yaUgWXQSzOJ9vj8RgJHg_callbacks.png "callbacks.png")

## POST Request

In every POST method set **Content-Type: application/x-www-form-urlencoded** header.
