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
[block:callout]
{
  "type": "danger",
  "title": "API v1 is DEPRECATED",
  "body": "API v1 is DEPRECATED and no longer maintained. Please use API v2 http://developer.coingate.com/v2"
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/7507b5a-coingate_api_diagram.jpg",
        "coingate_api_diagram.jpg",
        2162,
        2099,
        "#2eb274"
      ],
      "caption": ""
    }
  ]
}
[/block]
1. Call [Create Order](doc:create-order) API method to create an order in the CoinGate system.
2. CoinGate checks if the order is valid.
2. a) If the order is valid, CoinGate responds with 200 HTTP status and returns [order data](doc:create-order). After receiving 200 HTTP status, you should redirect the buyer to `payment_url` address.
2. b) If the order is not valid, CoinGate returns 422 (or other) [error](doc:common-errors) HTTP status and an error message.
3. When the buyer pays for the order, CoinGate sends [Payment Callback/Payment Notification](doc:payment-callback) to your `callback_url` url. `callback_url` is defined when [creating order](doc:create-order). CoinGate also sends [Payment Callback](doc:payment-callback) when order status is changed to canceled, expired or to any other status [read more about CoinGate order statuses](doc:order-statuses). Please note, that payment notifications are sent using **POST** method.

[block:api-header]
{
  "type": "basic",
  "title": "Environments"
}
[/block]

[block:parameters]
{
  "data": {
    "0-0": "**Live**",
    "0-1": "`https://api.coingate.com/v1`",
    "1-0": "**Sandbox**",
    "1-1": "`https://api-sandbox.coingate.com/v1`"
  },
  "cols": 2,
  "rows": 2
}
[/block]
* If you wish to use **Live** environment, use have to create an account and API credentials on https://coingate.com
* If you wish to use **Sandbox** environment, use have to create an account and API credentials on https://sandbox.coingate.com
[block:api-header]
{
  "type": "basic",
  "title": "Resources"
}
[/block]
* [Ruby Gem](https://rubygems.org/gems/coingate)
* [Coingate PHP](https://github.com/coingate/coingate-php)
* [Omnipay (PHP)](https://github.com/thephpleague/omnipay)
* [Ruby on Rails Shop Example](http://example.coingate.com/) / [Source Code](https://github.com/coingate/rails-shop-example)
* [PHP Laravel Shop Example](http://demo1.coingate.com/) / [Source Code](https://github.com/arnasfomenko/coingate-laravel-php-shop)
* [E-commerce Plugins](https://coingate.com/plugins)
[block:api-header]
{
  "type": "basic",
  "title": "API Requests"
}
[/block]
API Request is used to query CoinGate API (examples: [Create Order](doc:create-order), [Get Order](doc:get-order)).

To review your API Requests, login to your CoinGate account, then go to API » Requests.

API Request attributes:

* Action - Which API method was queried.
* Response - HTTP status returned by CoinGate.
* Parameters - Parameters used to query CoinGate API.
* Response - Parameters returned by CoinGate.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/B2ELvNVCT2unLKj4ewy8_api-requests.png",
        "api-requests.png",
        "999",
        "442",
        "#306694",
        ""
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "type": "basic",
  "title": "API Request Limits"
}
[/block]
1,000 / hour per ip address for all API endpoints.

1 hour API limits per credentials by specific endpoint:
[block:parameters]
{
  "data": {
    "h-0": "Environment",
    "h-1": "Endpoint",
    "0-0": "Live",
    "0-1": "POST /orders",
    "1-0": "Live",
    "1-1": "GET /orders/:id",
    "h-2": "Rate Limit",
    "0-2": "300 / hour",
    "1-2": "500 / hour",
    "3-0": "Sandbox",
    "3-1": "POST /orders",
    "3-2": "300 / hour",
    "4-0": "Sandbox",
    "4-1": "GET /orders/:id",
    "4-2": "500 / hour",
    "2-0": "Live",
    "2-1": "GET /orders",
    "2-2": "500 / hour",
    "5-0": "Sandbox",
    "5-1": "GET /orders",
    "5-2": "500 / hour"
  },
  "cols": 3,
  "rows": 6
}
[/block]
All other endpoints which is not described above the limit is 1,000 / hour per API credentials.

API limits can be manually increased for specific user. If you want change your API limits, please contact to support: [support@coingate.com](mailto:support@coingate.com).

API returns [429 HTTP error](doc:common-errors) if limit is exceeded.
[block:api-header]
{
  "type": "basic",
  "title": "Payment Callbacks (Payment Notifications)"
}
[/block]
[Payment Callback](doc:payment-callback) (Payment Notification) is a response which is sent after order status is changed (see [Order Statuses](doc:order-statuses)). It is sent by CoinGate to merchant's ***callback_url***, which is set during order creation (see [Create Order](doc:create-order)).

To review your Payment Callbacks, login to your CoinGate account, then go to API » Payment Callbacks.

Payment Callback attributes:

* **Response Status** - HTTP status returned by merchant.
* **Response Data** - Data body returned by merchant.
* **Callback Params** - Parameters sent by CoinGate to merchant's ***callback_url***.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/yaUgWXQSzOJ9vj8RgJHg_callbacks.png",
        "callbacks.png",
        "1028",
        "587",
        "#a75742",
        ""
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "type": "basic",
  "title": "POST Request"
}
[/block]
In every POST method set **Content-Type: application/x-www-form-urlencoded** header.