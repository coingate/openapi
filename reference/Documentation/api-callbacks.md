---
title: API Callbacks
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
A payment callback (payment notification) will be sent to the merchant’s **callback_url** whenever the order status, refund status, or billing status changes due to a request. The _callback_url_ parameter is defined when creating the object.

- [Create Merchant Order](doc:create-order)
- [Create Order Refund](doc:create-refund)
- [Create Send Request](ref:create-send)

> 📘 Testing
> 
> For payment callback handling you can use [requestcatcher.com](https://requestcatcher.com/) tool.

## Callback Format

> 🚧 
> 
> Callback data is sent in **POST** method.

By [creating new API App](https://support.coingate.com/hc/en-us/articles/4402498918546) you can choose in which format you want to receive callbacks:

- Form Encoding (application/x-www-form-urlencoded)
- JSON (application/json)

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/6cd04730eca248cbffe8b5264bbf4466ef0e61f9ab99efc373da8b59eba1e03b-Screenshot_2025-02-26_at_15.48.10.png",
        null,
        ""
      ],
      "align": "center",
      "border": true
    }
  ]
}
[/block]


Change callback format for existing API App go to Merchant » API » Apps » Edit.

## Callback Retry Schedule

> 📘 
> 
> CoinGate sends payment notification while your application returns response **200 (OK) HTTP** or **204 (No Content)** status code.

### Retry Policy for Payment Notifications

Payment notifications are sent according to the following schedule based on the retry count:

- **Every 1 minute** if the retry count is **≤ 5**
- **Every 5 minutes** if the retry count is **> 5 and ≤ 10**
- **Every 10 minutes** if the retry count is **> 10 and ≤ 15**
- **Every 20 minutes** if the retry count is **> 15 and ≤ 20**
- **Every 30 minutes** if the retry count is **> 20 and ≤ 25**
- **Every 1 hour** if the retry count is **> 25 and ≤ 30**
- **Every 5 hours** if the retry count is **> 30 and ≤ 35**
- **Every 1 day** if the retry count is **> 35 and ≤ 40**
- **Callback will be canceled** if the retry count is **≥ 41**

### Notification Response Timeout

After sending a payment notification, CoinGate waits for a response for **20 seconds**.

### Conditions for Canceling and Terminating Payment Notifications

A payment notification will be canceled and terminated under the following conditions:

- The retry limit of 40 attempts is reached.
- A 301 or 302 (Redirect) status is received. This typically occurs when an “http” URL is redirected to “https”. Ensure the URL used is correct.
- A 401 (Unauthorized) status is received. This commonly happens when the website is password-protected (Basic access authentication). Ensure the website is publicly accessible.
- The payment notification is sent to the TOR network.
- The payment notification is sent to a private network, such as localhost.

## IP Addresses

Payment Callbacks are sent from the servers listed in the following public API endpoints:

- Live: <https://api.coingate.com/v2/ips-v4>
- Sandbox: <https://api-sandbox.coingate.com/v2/ips-v4>

These endpoints are public and do not require authentication. Each IP address is listed on a new line.

Ensure that your server and any third-party security services (e.g., Cloudflare, Incapsula) allow traffic from these IP addresses. Blocking them may prevent successful callback delivery.

We recommend updating your IP whitelist regularly using the information provided by these endpoints.

## Private Nework & Localhost

CoinGate payment callback will not send notifications to private networks (for example: localhost).  
In localhost, you can send test payment notification with [cURL library](https://curl.haxx.se/):

```shell HTTPie
# https://httpie.io/

http POST "https://coingate.requestcatcher.com/payment" \
    id==343 \
    order_id=="ORDER-1415020039" \
    status=="paid" \
    price_amount==1050.99 \
    price_currency=="USD" \
    receive_currency=="EUR" \
    receive_amount==926.73 \
    pay_amount==4.81849315 \
    pay_currency=="BTC" \
    created_at=="2014-11-03T13:07:28+00:00"
```
```curl
curl --request POST \
     --data-urlencode "id=343" \
     --data-urlencode "order_id=ORDER-1415020039" \
     --data-urlencode "status=paid" \
     --data-urlencode "price_amount=1050.99" \
     --data-urlencode "price_currency=USD" \
     --data-urlencode "receive_currency=EUR" \
     --data-urlencode "receive_amount=926.73" \
     --data-urlencode "pay_amount=4.81849315" \
     --data-urlencode "pay_currency=BTC" \
     --data-urlencode "created_at=2014-11-03T13:07:28+00:00" \
     "https://coingate.requestcatcher.com/payment"
```

## Payment Callback Logs

You can review payment callbacks and your server response to callback in your account panel. Login to your account and locate API » Payment Callbacks.

- Live: <https://account.coingate.com/merchant-tools/api-integrations?tab=callbacks>
- Sandbox: <https://dashboard-sandbox.coingate.com/account/apps/api-payment-callbacks>

## Accepting Payment Callback

Example: save the code below as `accept-coingate-callback.php` and execute cURL command in your command line tool:

```shell HTTPie
# https://httpie.io/

http POST "http://localhost/accept-coingate-callback.php?token=5d02161be9bfb6192a33" \
    id==343 \
    order_id=="ORDER-1415020039" \
    status=="paid" \
    price_amount==1050.99 \
    price_currency=="USD" \
    receive_currency=="EUR" \
    receive_amount==926.73 \
    pay_amount==4.81849315 \
    pay_currency=="BTC" \
    created_at=="2014-11-03T13:07:28+00:00"
```
```curl cURL
curl --request POST \
     --data-urlencode "id=343" \
     --data-urlencode "order_id=ORDER-1415020039" \
     --data-urlencode "status=paid" \
     --data-urlencode "price_amount=1050.99" \
     --data-urlencode "price_currency=USD" \
     --data-urlencode "receive_currency=EUR" \
     --data-urlencode "receive_amount=926.73" \
     --data-urlencode "pay_amount=4.81849315" \
     --data-urlencode "pay_currency=BTC" \
     --data-urlencode "created_at=2014-11-03T13:07:28+00:00" \
     "http://localhost/accept-coingate-callback.php?token=5d02161be9bfb6192a33"
```

```php
<?php

// Database connection
$mysqli = new mysqli('hostname', 'username', 'password', 'database');

// Check connection
if ($mysqli->connect_error) {
    die("Connection failed: " . $mysqli->connect_error);
}

// Prepare and bind to securely fetch the order
$order_id = $_POST['order_id'];
$stmt = $mysqli->prepare("SELECT * FROM orders WHERE id = ?");
$stmt->bind_param("i", $order_id);
$stmt->execute();
$result = $stmt->get_result();
$order = $result->fetch_assoc();
$stmt->close();

// Securely compare the tokens
$received_token = $_POST['token'];
$stored_hashed_token = $order['token'];

if (hash_equals($stored_hashed_token, hash_hmac('sha256', $received_token, 'your_secret_key'))) {
    // Handle CoinGate order status: https://developer.coingate.com/docs/order-statuses
    $status = NULL;

    // Verify payment status
    if ($_POST['status'] === 'paid') {
        if ($_POST['price_amount'] == $order['amount']) {
            $status = 'paid';
        }
    } else {
        $status = $_POST['status'];
    }

    // Update order status if necessary
    if (!is_null($status)) {
        $stmt = $mysqli->prepare("UPDATE orders SET status = ? WHERE id = ?");
        $stmt->bind_param("si", $status, $order_id);
        $stmt->execute();
        $stmt->close();
    }
}

// Close the database connection
$mysqli->close();
?>
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