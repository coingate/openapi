---
title: Create Conversion
excerpt: ''
api:
  file: v2.json
  operationId: create-conversion
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
### On successful creation

In the response, check the field `actions_required`.

- As operation requires confirmation or cancellation
- Use one of the following actions given in `actions_required` or API endpoints:
  - ✅ [Confirm Conversion](https://developer.coingate.com/reference/confirm-conversion)
  - ❌ [Cancel Conversion](https://developer.coingate.com/reference/cancel-conversion)

Once confirmed, your balance will be updated with the converted currency.