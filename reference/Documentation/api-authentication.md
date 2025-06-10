---
title: API Authentication
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
> 📘 Create API Key
> 
> <https://support.coingate.com/hc/en-us/articles/4402498918546>

Please note, that for "Test" (sandbox) mode you must generate separate API credentials on <https://sandbox.coingate.com.> API credentials generated on <https://coingate.com> will not work for "Test" (sandbox) mode.

Provide generated Token to **HTTP Authorization Header**.

```curl
curl "https://api-sandbox.coingate.com/v2/auth/test" \
     -H 'Authorization: Token YOUR_API_TOKEN'
```
```php
<?php

$auth_token = 'YOUR_API_AUTH_TOKEN';

$headers   = array();
$headers[] = 'Authorization: Token ' . $auth_token;
$curl      = curl_init();

curl_setopt($curl, CURLOPT_HTTPHEADER, $headers);
```