---
title: Code Examples
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

* [Ruby Gem](https://rubygems.org/gems/coingate)
* [Coingate PHP](https://github.com/coingate/coingate-php)
* [Omnipay (PHP)](https://github.com/thephpleague/omnipay)
* [Ruby on Rails Shop Example](http://example.coingate.com/) / [Source Code](https://github.com/coingate/rails-shop-example)
* [E-commerce Plugins](https://coingate.com/plugins)

```ruby
# Recommend to use Ruby gem: https://rubygems.org/gems/coingate

require 'openssl'
require 'rest_client'
require 'json'

APP_ID      = 'YOUR_APP_ID'
API_KEY     = 'YOUR_API_KEY'
API_SECRET  = 'YOUR_API_SECRET'

def api_request(url, request_method = :get, params = {})
  nonce     = (Time.now.to_f * 1e6).to_i
  message   = nonce.to_s + APP_ID.to_s + API_KEY
  signature = OpenSSL::HMAC.hexdigest(OpenSSL::Digest.new('sha256'), API_SECRET, message)

  headers = {
    'Access-Nonce'      => nonce,
    'Access-Key'        => API_KEY,
    'Access-Signature'  => signature
  }

  begin
    response = case request_method
    when :get
      RestClient.get(url, headers)
    when :post
      RestClient.post(url, params, headers.merge('Content-Type' => 'application/x-www-form-urlencoded'))
    end
    
    [response.code, response.to_str]
  rescue => e
    [e.http_code, e.response]
  end
end

# GET Example
status_code, response_body = api_request('https://api-sandbox.coingate.com/v1/orders/3')

puts status_code
puts response_body

# POST Example
post_params = {
  order_id:         'ORDER-1412759368',
  price:            1050.99,
  currency:         'USD',
  receive_currency: 'EUR',
  callback_url:     'https://example.com/payments/callback?token=6tCENGUYI62ojkuzDPX7Jg',
  cancel_url:       'https://example.com/cart',
  success_url:      'https://example.com/account/orders',
  description:      'Apple Iphone 6'
}

status_code, response_body = api_request('https://api-sandbox.coingate.com/v1/orders', :post, post_params)

puts status_code
puts response_body
```
```php
<?php
// Recommend to use coingate-php library: https://github.com/coingate/coingate-php

		define('APP_ID', 'YOUR_APP_ID');
    define('API_KEY', 'YOUR_API_KEY');
    define('API_SECRET', 'YOUR_API_SECRET');

    function api_request($url, $method = 'GET', $params = array())
    {
        $nonce      = time();
        $message    = $nonce . APP_ID . API_KEY;
        $signature  = hash_hmac('sha256', $message, API_SECRET);

        $headers = array();
        $headers[] = 'Access-Key: ' . API_KEY;
        $headers[] = 'Access-Nonce: ' . $nonce;
        $headers[] = 'Access-Signature: ' . $signature;

        $curl = curl_init();
        
        $curl_options = array(
            CURLOPT_RETURNTRANSFER  => 1,
            CURLOPT_URL             => $url
        );

        if ($method == 'POST') {
            $headers[] = 'Content-Type: application/x-www-form-urlencoded';

            array_merge($curl_options, array(CURLOPT_POST => 1));
            curl_setopt($curl, CURLOPT_POSTFIELDS, http_build_query($params));
        }

        curl_setopt_array($curl, $curl_options);
        curl_setopt($curl, CURLOPT_HTTPHEADER, $headers);
        curl_setopt($curl, CURLOPT_SSL_VERIFYPEER, FALSE);

        $response       = curl_exec($curl);
        $http_status    = curl_getinfo($curl, CURLINFO_HTTP_CODE);

        curl_close($curl);

        return array('status_code' => $http_status, 'response_body' => $response);
    }

    // GET Example
    $response = api_request('https://api-sandbox.coingate.com/v1/orders/1');

    echo $response['status_code'];
    echo $response['response_body'];

    // POST Example
    $post_params = array(
        'order_id'          => 'ORDER-1412759368',
        'price'             => 1050.99,
        'currency'          => 'USD',
        'receive_currency'  => 'EUR',
        'callback_url'      => 'https://example.com/payments/callback?token=6tCENGUYI62ojkuzDPX7Jg',
        'cancel_url'        => 'https://example.com/cart',
        'success_url'       => 'https://example.com/account/orders',
        'description'       => 'Apple Iphone 6'
    );

    $response = api_request('https://api-sandbox.coingate.com/v1/orders', 'POST', $post_params);

    echo $response['status_code'];
    echo $response['response_body'];

?>
```
```python
import hashlib
import hmac
import time
import urllib
import urllib2

APP_ID      = 'YOUR_APP_ID'
API_KEY     = 'YOUR_API_KEY'
API_SECRET  = 'YOUR_API_SECRET'

def api_request(url, request_method='get', params={}):
  nonce       = str(int(time.time() * 1e6))
  message     = str(nonce) + str(APP_ID) + API_KEY
  signature   = hmac.new(API_SECRET, message, hashlib.sha256).hexdigest()

  headers = {
    'Access-Nonce': nonce,
    'Access-Key': API_KEY,
    'Access-Signature': signature
  }

  if request_method == 'get':
    req = urllib2.Request(url, headers=headers)
  elif request_method == 'post':
    headers['Content-Type'] = 'application/x-www-form-urlencoded'
    req = urllib2.Request(url, data=urllib.urlencode(params), headers=headers)

  try:
    response      = urllib2.urlopen(req)
    status_code   = response.getcode()
    response_body = response.read()
  except urllib2.HTTPError as e:
    status_code   = e.getcode()
    response_body = e.read()

  return status_code, response_body


# GET Example
status_code, response_body = api_request('https://api-sandbox.coingate.com/v1/orders/3')

print status_code, response_body

# POST Example
post_params = {
  'order_id':         'ORDER-1412759368',
  'price':            1050.99,
  'currency':         'USD',
  'receive_currency': 'EUR',
  'callback_url':     'https://example.com/payments/callback?token=6tCENGUYI62ojkuzDPX7Jg',
  'cancel_url':       'https://example.com/cart',
  'success_url':      'https://example.com/account/orders',
  'description':      'Apple Iphone 6'
}

status_code, response_body = api_request('https://api-sandbox.coingate.com/v1/orders', 'post', post_params)

print status_code, response_body
```
