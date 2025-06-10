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
[block:callout]
{
  "type": "danger",
  "title": "API v1 is DEPRECATED",
  "body": "API v1 is DEPRECATED and no longer maintained. Please use API v2 http://developer.coingate.com/v2"
}
[/block]
* [Ruby Gem](https://rubygems.org/gems/coingate)
* [Coingate PHP](https://github.com/coingate/coingate-php)
* [Omnipay (PHP)](https://github.com/thephpleague/omnipay)
* [Ruby on Rails Shop Example](http://example.coingate.com/) / [Source Code](https://github.com/coingate/rails-shop-example)
* [E-commerce Plugins](https://coingate.com/plugins)
[block:code]
{
  "codes": [
    {
      "code": "# Recommend to use Ruby gem: https://rubygems.org/gems/coingate\n\nrequire 'openssl'\nrequire 'rest_client'\nrequire 'json'\n\nAPP_ID      = 'YOUR_APP_ID'\nAPI_KEY     = 'YOUR_API_KEY'\nAPI_SECRET  = 'YOUR_API_SECRET'\n\ndef api_request(url, request_method = :get, params = {})\n  nonce     = (Time.now.to_f * 1e6).to_i\n  message   = nonce.to_s + APP_ID.to_s + API_KEY\n  signature = OpenSSL::HMAC.hexdigest(OpenSSL::Digest.new('sha256'), API_SECRET, message)\n\n  headers = {\n    'Access-Nonce'      => nonce,\n    'Access-Key'        => API_KEY,\n    'Access-Signature'  => signature\n  }\n\n  begin\n    response = case request_method\n    when :get\n      RestClient.get(url, headers)\n    when :post\n      RestClient.post(url, params, headers.merge('Content-Type' => 'application/x-www-form-urlencoded'))\n    end\n    \n    [response.code, response.to_str]\n  rescue => e\n    [e.http_code, e.response]\n  end\nend\n\n# GET Example\nstatus_code, response_body = api_request('https://api-sandbox.coingate.com/v1/orders/3')\n\nputs status_code\nputs response_body\n\n# POST Example\npost_params = {\n  order_id:         'ORDER-1412759368',\n  price:            1050.99,\n  currency:         'USD',\n  receive_currency: 'EUR',\n  callback_url:     'https://example.com/payments/callback?token=6tCENGUYI62ojkuzDPX7Jg',\n  cancel_url:       'https://example.com/cart',\n  success_url:      'https://example.com/account/orders',\n  description:      'Apple Iphone 6'\n}\n\nstatus_code, response_body = api_request('https://api-sandbox.coingate.com/v1/orders', :post, post_params)\n\nputs status_code\nputs response_body",
      "language": "ruby"
    },
    {
      "code": "<?php\n// Recommend to use coingate-php library: https://github.com/coingate/coingate-php\n\n\t\tdefine('APP_ID', 'YOUR_APP_ID');\n    define('API_KEY', 'YOUR_API_KEY');\n    define('API_SECRET', 'YOUR_API_SECRET');\n\n    function api_request($url, $method = 'GET', $params = array())\n    {\n        $nonce      = time();\n        $message    = $nonce . APP_ID . API_KEY;\n        $signature  = hash_hmac('sha256', $message, API_SECRET);\n\n        $headers = array();\n        $headers[] = 'Access-Key: ' . API_KEY;\n        $headers[] = 'Access-Nonce: ' . $nonce;\n        $headers[] = 'Access-Signature: ' . $signature;\n\n        $curl = curl_init();\n        \n        $curl_options = array(\n            CURLOPT_RETURNTRANSFER  => 1,\n            CURLOPT_URL             => $url\n        );\n\n        if ($method == 'POST') {\n            $headers[] = 'Content-Type: application/x-www-form-urlencoded';\n\n            array_merge($curl_options, array(CURLOPT_POST => 1));\n            curl_setopt($curl, CURLOPT_POSTFIELDS, http_build_query($params));\n        }\n\n        curl_setopt_array($curl, $curl_options);\n        curl_setopt($curl, CURLOPT_HTTPHEADER, $headers);\n        curl_setopt($curl, CURLOPT_SSL_VERIFYPEER, FALSE);\n\n        $response       = curl_exec($curl);\n        $http_status    = curl_getinfo($curl, CURLINFO_HTTP_CODE);\n\n        curl_close($curl);\n\n        return array('status_code' => $http_status, 'response_body' => $response);\n    }\n\n    // GET Example\n    $response = api_request('https://api-sandbox.coingate.com/v1/orders/1');\n\n    echo $response['status_code'];\n    echo $response['response_body'];\n\n    // POST Example\n    $post_params = array(\n        'order_id'          => 'ORDER-1412759368',\n        'price'             => 1050.99,\n        'currency'          => 'USD',\n        'receive_currency'  => 'EUR',\n        'callback_url'      => 'https://example.com/payments/callback?token=6tCENGUYI62ojkuzDPX7Jg',\n        'cancel_url'        => 'https://example.com/cart',\n        'success_url'       => 'https://example.com/account/orders',\n        'description'       => 'Apple Iphone 6'\n    );\n\n    $response = api_request('https://api-sandbox.coingate.com/v1/orders', 'POST', $post_params);\n\n    echo $response['status_code'];\n    echo $response['response_body'];\n\n?>",
      "language": "php"
    },
    {
      "code": "import hashlib\nimport hmac\nimport time\nimport urllib\nimport urllib2\n\nAPP_ID      = 'YOUR_APP_ID'\nAPI_KEY     = 'YOUR_API_KEY'\nAPI_SECRET  = 'YOUR_API_SECRET'\n\ndef api_request(url, request_method='get', params={}):\n  nonce       = str(int(time.time() * 1e6))\n  message     = str(nonce) + str(APP_ID) + API_KEY\n  signature   = hmac.new(API_SECRET, message, hashlib.sha256).hexdigest()\n\n  headers = {\n    'Access-Nonce': nonce,\n    'Access-Key': API_KEY,\n    'Access-Signature': signature\n  }\n\n  if request_method == 'get':\n    req = urllib2.Request(url, headers=headers)\n  elif request_method == 'post':\n    headers['Content-Type'] = 'application/x-www-form-urlencoded'\n    req = urllib2.Request(url, data=urllib.urlencode(params), headers=headers)\n\n  try:\n    response      = urllib2.urlopen(req)\n    status_code   = response.getcode()\n    response_body = response.read()\n  except urllib2.HTTPError as e:\n    status_code   = e.getcode()\n    response_body = e.read()\n\n  return status_code, response_body\n\n\n# GET Example\nstatus_code, response_body = api_request('https://api-sandbox.coingate.com/v1/orders/3')\n\nprint status_code, response_body\n\n# POST Example\npost_params = {\n  'order_id':         'ORDER-1412759368',\n  'price':            1050.99,\n  'currency':         'USD',\n  'receive_currency': 'EUR',\n  'callback_url':     'https://example.com/payments/callback?token=6tCENGUYI62ojkuzDPX7Jg',\n  'cancel_url':       'https://example.com/cart',\n  'success_url':      'https://example.com/account/orders',\n  'description':      'Apple Iphone 6'\n}\n\nstatus_code, response_body = api_request('https://api-sandbox.coingate.com/v1/orders', 'post', post_params)\n\nprint status_code, response_body",
      "language": "python"
    }
  ]
}
[/block]