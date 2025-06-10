---
title: Payment Callback
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
Payment callback (Payment notification) will be sent to merchant's ***callback_url*** when [order status](doc:order-statuses) is changed to *confirming*, *paid*, *invalid*, *canceled*, *refunded* or *expired*.
[block:callout]
{
  "type": "warning",
  "body": "Callback data is sent in **POST** method."
}
[/block]
CoinGate callback sends data below:
[block:parameters]
{
  "data": {
    "h-0": "Name",
    "h-1": "Value",
    "0-0": "`id`",
    "0-1": "CoinGate order (invoice) ID.",
    "1-0": "`order_id`",
    "1-1": "Merchant's custom order ID. You should identify your order or invoice or shopping cart by this value.",
    "2-0": "`status`",
    "2-1": "CoinGate [payment status](doc:order-statuses).",
    "3-0": "`price`",
    "3-1": "The price set by the merchant.",
    "4-0": "`currency`",
    "4-1": "The currency code which defines the currency in which you wish to price your merchandise; used to define price parameter.",
    "5-0": "`receive_currency`",
    "5-1": "The currency code which defines the currency in which you wish to receive your payments. Currency conversions are done at CoinGate. Possible values: EUR, USD, BTC. Please note, that you will not be able to withdraw EUR and USD until you pass level 2 (Merchant) verification. To withdraw BTC no verification is needed.",
    "6-0": "`receive_amount`",
    "7-0": "`btc_amount`",
    "8-0": "`created_at`",
    "8-1": "Invoice creation time.",
    "6-1": "The amount which you will receive when the invoice is paid. It is calculated by taking the `price` amount (converted to currency units set in `receive_currency`) and subtracting CoinGate processing fee from it.",
    "7-1": "The amount of bitcoins which the buyer has to pay. It is calculated by taking the `price` amount and converting it to bitcoins."
  },
  "cols": 2,
  "rows": 9
}
[/block]
**Content-Type: application/x-www-form-urlencoded** 
[block:code]
{
  "codes": [
    {
      "code": "// print_r($_POST)\n\nArray\n(\n    [id] => 343\n    [order_id] => 14037\n    [status] => paid\n    [price] => 1050.99\n    [currency] => USD\n    [receive_currency] => EUR\n    [receive_amount] => 926.73\n    [btc_amount] => 4.81849315\n    [created_at] => 2014-11-03T13:07:28+00:00\n)",
      "language": "php"
    }
  ]
}
[/block]
See the code below how to accept callback.
[block:api-header]
{
  "type": "basic",
  "title": "Callback Retry Time"
}
[/block]

[block:callout]
{
  "type": "info",
  "body": "CoinGate sends payment notification while your application returns response **200 (OK) HTTP** status code."
}
[/block]
* Sends every 1 minute if retry count is <= 5
* Sends every 5 minutes if retry count is > 5 and <= 10
* Sends every 10 minutes if retry count is > 10 and <= 15
* Sends every 20 minutes if retry count is > 15 and <= 20
* Sends every 30 minutes if retry count is > 20 and <= 25
* Sends every 1 hour if retry count is > 25 and <= 30
* Sends every 5 hours if retry count is > 30 and <= 35
* Sends every 1 day if try count is > 35 and <= 40
* Callback will be canceled if retry count is >= 41

After sending payment notification, we wait for response for 20 seconds.

Payment notification will be canceled and terminated if one of these scenarios happen:

* Payment notification is sent 40 times.
* If after sending payment notification we receive 301, 302 (redirect) status response. This commonly happens if you use "http" in your URL and it gets redirected to "https".
* If after sending payment notification we receive 401 (Unauthorized). This commonly happens when your website is protected by password (Basic access authentication). Make your website publicly accessible.
* When payment notification is sent to TOR network.
* When payment notification is sent to private network (for example: localhost).
[block:api-header]
{
  "title": "IP Addresses"
}
[/block]
Payment Callback is sending from servers which is described in API endpoint. This API endpoint is public, authentication is not required.
Live: https://api.coingate.com/v1/ips-v4
Sandbox: https://api-sandbox.coingate.com/v1/ips-v4

Each IP is separated by new line. Please ensure, that your server and third-party security services (cloudflare, incapsula, etc.) is not blocking these IP addresses.

Recommend regularly update your IP whitelist from this API endpoint.
[block:api-header]
{
  "type": "basic",
  "title": "Private Nework & Localhost"
}
[/block]
CoinGate payment callback does not send notification to private network (for example: localhost).
In localhost you can send test payment notification with [cURL library](https://curl.haxx.se/):
[block:code]
{
  "codes": [
    {
      "code": "curl -X POST -d \"id=343&order_id=ORDER-1415020039&status=paid&price=1050.99&currency=USD&receive_currency=EUR&receive_amount=926.73&btc_amount=4.81849315&created_at=2014-11-03T13:07:28%2B00:00\" http://localhost/coingate-payment-callback",
      "language": "curl"
    }
  ]
}
[/block]

[block:api-header]
{
  "type": "basic",
  "title": "Payment Callback Logs"
}
[/block]
You can review payment callbacks and your server response to callback in your account panel: login to your account » API » Payment Callbacks.
[block:api-header]
{
  "type": "basic",
  "title": "Accepting Payment Callback"
}
[/block]
For example: save code below as `accept-coingate-callback.php` and execute cURL command in your command line tool:

```
curl -X POST -d "id=343&order_id=14037&status=paid&price=1050.99&currency=USD&receive_currency=EUR&receive_amount=926.73&btc_amount=4.81849315&created_at=2014-11-03T13:07:28%2B00:00" http://localhost/accept-coingate-callback.php?token=5d02161be9bfb6192a33
```
[block:code]
{
  "codes": [
    {
      "code": "<?php\n\n// Your custom order_id is defined when you creating new order: https://developer.coingate.com/docs/create-order\n// Also don't forget to prevent SQL injection\n$result = mysql_query(\"SELECT * FROM orders WHERE id = \" . $_POST['order_id']);\n$order = mysql_fetch_assoc($result);\n\n// token is your random secure string (for example: 5d02161be9bfb6192a33) for each order\nif ($_POST['token'] == $order['token']) {\n  // Handle CoinGate order status: https://developer.coingate.com/docs/order-statuses\n  $status = NULL;\n  if ($_POST['status'] == 'paid') {\n    if ($_POST['price'] >= $order['amount']) {\n      $status = 'paid';\n    }\n  }\n  else {\n    $status = $_POST['status'];\n  }\n\n  if (!is_null($status)) {\n      mysql_query(\"UPDATE orders SET status = '\".$status.\"' WHERE id = \".$_POST['order_id']);\n  }\n}",
      "language": "php"
    },
    {
      "code": "class CoingateCallbackController < ApplicationController\n  skip_before_action :verify_authenticity_token, only: :create\n\n  def create\n    order = Order.find_by(id: params[:order_id])\n\n    if order.present?\n      if params[:token].present? && order.token == params[:token]\n        status = nil\n\n        if params[:status] == 'paid'\n          if params[:price].to_d >= order.amount # in addition you can check currency (params[:currency] == order.currency)\n            status = 'paid'\n          end\n        else\n          status = params[:status]\n        end\n\n        if status.present?\n          order.update_attribute(:status, status)\n        end\n      end\n    end\n  end\nend",
      "language": "ruby",
      "name": "Ruby on Rails"
    }
  ]
}
[/block]