---
title: Errors
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
Most common API error responses described below. Error response must be identified by **HTTP status** and **reason** attribute in your application.
Please note, that specific API methods, for example [Create Order](doc:create-order) has their own errors (422 Unprocessable Entity - when order is not valid).
[block:parameters]
{
  "data": {
    "h-0": "HTTP Status",
    "h-1": "Reason",
    "h-2": "Description",
    "0-0": "401 (Unauthorized)",
    "0-1": "BadCredentials",
    "0-2": "API credentials is not valid",
    "1-0": "404 (Not Found)",
    "1-1": "PageNotFound",
    "1-2": "Page, action or record not found",
    "2-0": "404 (Not Found)",
    "2-1": "RecordNotFound",
    "2-2": "Record not found",
    "3-0": "500 (Internal Server Error)",
    "3-1": "InternalServerError",
    "3-2": "Something wrong in CoinGate",
    "4-0": "429 (Too Many Requests)",
    "4-1": "RateLimitException",
    "4-2": "API request limit is exceeded"
  },
  "cols": 3,
  "rows": 5
}
[/block]
Response example:
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"message\": \"Not found App by Access-Key\",\n  \"reason\": \"BadCredentials\"\n}",
      "language": "json"
    }
  ]
}
[/block]