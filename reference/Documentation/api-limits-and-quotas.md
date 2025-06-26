---
title: API Limits and Quotas
deprecated: false
hidden: false
metadata:
  robots: index
---
## API Requests

Rate limits apply to both public and private API endpoints. The default limit is **200 requests per minute**.

If this limit is exceeded, the following response will be returned:

```json
{
  "message": "API request limit is exceeded",
  "reason": "RateLimitExceeded"
}
```

## Merchant Order Creation

The default limit is **500 orders per hour per business**.

This includes orders created via the API or through the dashboard. Once the limit is reached, further order creation will be blocked until the hourly window resets.

To create an order via API, use the following endpoint:\
[Create Order – API Reference](https://developer.coingate.com/reference/create-order)

> Need a higher limit? [Contact our support team](https://support.coingate.com/hc/en-us/requests/new) to request an increase.