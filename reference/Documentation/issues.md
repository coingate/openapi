---
title: Issues
excerpt: The common issues why your ecommerce or API integration possible not working.
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

[block:api-header]
{
  "title": "Unable to create order or unable to send a request to CoinGate API"
}
[/block]
**Possible reasons:** 
  * API credentials used in the wrong environment. Please create separate users and separate API credentials for Sandbox (sandbox.coingate.com) or Live (coingate.com) environments.
  * Wrong API credentials. Please check if you have entered them correctly. Make sure that there are no spaces before or after the text.
  * Wrong API credentials signature, invalid order, etc. You can see more details by logging in to your CoinGate account and going to API » Requests.
  * You have whitelisted IP address(es) when creating API credentials, but requests are coming from a different IP. You can check the whitelisted IPs by logging in to your CoinGate account, going to API » Apps and clicking Edit next to your API credentials.
  * cURL or other library used to communicate with CoinGate API is outdated or is working incorrectly. Please check library version.
  * Your server can not reach coingate.com. Please check if coingate.com is available and if your server can reach it.

You can check all API request logs by logging in to your CoinGate account and going to API » Requests.
[block:api-header]
{
  "title": "The order status is not updated after payment in e-commerce CMS or CoinGate does not send Payment Callback (Payment Notification)"
}
[/block]
**Possible reasons:**

  * Your server is on a private network, for example localhost. Please make sure that your application is publicly accessible.
  * Your website is disabled (in maintenance mode).
  * Your server firewall, third-party security service (cloudflare, incapsula, etc.) or your application is blocking CoinGate IP address.
  
You can check the specific reason why payment callback was not sent by logging in to your CoinGate account and going to API » Payment Callbacks.