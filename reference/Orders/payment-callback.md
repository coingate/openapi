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
> ❗️ API v1 is DEPRECATED
>
> API v1 is DEPRECATED and no longer maintained. Please use API v2 [http://developer.coingate.com/v2](http://developer.coingate.com/v2)

Payment callback (Payment notification) will be sent to merchant's ***callback\_url*** when [order status](doc:order-statuses) is changed to *confirming*, *paid*, *invalid*, *canceled*, *refunded* or *expired*.

> 🚧 Callback data is sent in **POST** method.

CoinGate callback sends data below:

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Name
      </th>

      <th>
        Value
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        `id`
      </td>

      <td>
        CoinGate order (invoice) ID.
      </td>
    </tr>

    <tr>
      <td>
        `order_id`
      </td>

      <td>
        Merchant's custom order ID. You should identify your order or invoice or shopping cart by this value.
      </td>
    </tr>

    <tr>
      <td>
        `status`
      </td>

      <td>
        CoinGate [payment status](doc:order-statuses).
      </td>
    </tr>

    <tr>
      <td>
        `price`
      </td>

      <td>
        The price set by the merchant.
      </td>
    </tr>

    <tr>
      <td>
        `currency`
      </td>

      <td>
        The currency code which defines the currency in which you wish to price your merchandise; used to define price parameter.
      </td>
    </tr>

    <tr>
      <td>
        `receive_currency`
      </td>

      <td>
        The currency code which defines the currency in which you wish to receive your payments. Currency conversions are done at CoinGate. Possible values: EUR, USD, BTC. Please note, that you will not be able to withdraw EUR and USD until you pass level 2 (Merchant) verification. To withdraw BTC no verification is needed.
      </td>
    </tr>

    <tr>
      <td>
        `receive_amount`
      </td>

      <td>
        The amount which you will receive when the invoice is paid. It is calculated by taking the `price` amount (converted to currency units set in `receive_currency`) and subtracting CoinGate processing fee from it.
      </td>
    </tr>

    <tr>
      <td>
        `btc_amount`
      </td>

      <td>
        The amount of bitcoins which the buyer has to pay. It is calculated by taking the `price` amount and converting it to bitcoins.
      </td>
    </tr>

    <tr>
      <td>
        `created_at`
      </td>

      <td>
        Invoice creation time.
      </td>
    </tr>
  </tbody>
</Table>

**Content-Type: application/x-www-form-urlencoded** 

```php
// print_r($_POST)

Array
(
    [id] => 343
    [order_id] => 14037
    [status] => paid
    [price] => 1050.99
    [currency] => USD
    [receive_currency] => EUR
    [receive_amount] => 926.73
    [btc_amount] => 4.81849315
    [created_at] => 2014-11-03T13:07:28+00:00
)
```

See the code below how to accept callback.

## Callback Retry Time

> 📘 CoinGate sends payment notification while your application returns response **200 (OK) HTTP** status code.

* Sends every 1 minute if retry count is \<= 5
* Sends every 5 minutes if retry count is > 5 and \<= 10
* Sends every 10 minutes if retry count is > 10 and \<= 15
* Sends every 20 minutes if retry count is > 15 and \<= 20
* Sends every 30 minutes if retry count is > 20 and \<= 25
* Sends every 1 hour if retry count is > 25 and \<= 30
* Sends every 5 hours if retry count is > 30 and \<= 35
* Sends every 1 day if try count is > 35 and \<= 40
* Callback will be canceled if retry count is >= 41

After sending payment notification, we wait for response for 20 seconds.

Payment notification will be canceled and terminated if one of these scenarios happen:

* Payment notification is sent 40 times.
* If after sending payment notification we receive 301, 302 (redirect) status response. This commonly happens if you use "http" in your URL and it gets redirected to "https".
* If after sending payment notification we receive 401 (Unauthorized). This commonly happens when your website is protected by password (Basic access authentication). Make your website publicly accessible.
* When payment notification is sent to TOR network.
* When payment notification is sent to private network (for example: localhost).

## IP Addresses

Payment Callback is sending from servers which is described in API endpoint. This API endpoint is public, authentication is not required.\
Live: [https://api.coingate.com/v1/ips-v4](https://api.coingate.com/v1/ips-v4)\
Sandbox: [https://api-sandbox.coingate.com/v1/ips-v4](https://api-sandbox.coingate.com/v1/ips-v4)

Each IP is separated by new line. Please ensure, that your server and third-party security services (cloudflare, incapsula, etc.) is not blocking these IP addresses.

Recommend regularly update your IP whitelist from this API endpoint.

## Private Nework & Localhost

CoinGate payment callback does not send notification to private network (for example: localhost).\
In localhost you can send test payment notification with [cURL library](https://curl.haxx.se/):

```curl
curl -X POST -d "id=343&order_id=ORDER-1415020039&status=paid&price=1050.99&currency=USD&receive_currency=EUR&receive_amount=926.73&btc_amount=4.81849315&created_at=2014-11-03T13:07:28%2B00:00" http://localhost/coingate-payment-callback
```

## Payment Callback Logs

You can review payment callbacks and your server response to callback in your account panel: login to your account » API » Payment Callbacks.

## Accepting Payment Callback

For example: save code below as `accept-coingate-callback.php` and execute cURL command in your command line tool:

```
curl -X POST -d "id=343&order_id=14037&status=paid&price=1050.99&currency=USD&receive_currency=EUR&receive_amount=926.73&btc_amount=4.81849315&created_at=2014-11-03T13:07:28%2B00:00" http://localhost/accept-coingate-callback.php?token=5d02161be9bfb6192a33
```

```php
<?php

// Your custom order_id is defined when you creating new order: https://developer.coingate.com/docs/create-order
// Also don't forget to prevent SQL injection
$result = mysql_query("SELECT * FROM orders WHERE id = " . $_POST['order_id']);
$order = mysql_fetch_assoc($result);

// token is your random secure string (for example: 5d02161be9bfb6192a33) for each order
if ($_POST['token'] == $order['token']) {
  // Handle CoinGate order status: https://developer.coingate.com/docs/order-statuses
  $status = NULL;
  if ($_POST['status'] == 'paid') {
    if ($_POST['price'] >= $order['amount']) {
      $status = 'paid';
    }
  }
  else {
    $status = $_POST['status'];
  }

  if (!is_null($status)) {
      mysql_query("UPDATE orders SET status = '".$status."' WHERE id = ".$_POST['order_id']);
  }
}
```
```ruby Ruby on Rails
class CoingateCallbackController < ApplicationController
  skip_before_action :verify_authenticity_token, only: :create

  def create
    order = Order.find_by(id: params[:order_id])

    if order.present?
      if params[:token].present? && order.token == params[:token]
        status = nil

        if params[:status] == 'paid'
          if params[:price].to_d >= order.amount # in addition you can check currency (params[:currency] == order.currency)
            status = 'paid'
          end
        else
          status = params[:status]
        end

        if status.present?
          order.update_attribute(:status, status)
        end
      end
    end
  end
end
```
