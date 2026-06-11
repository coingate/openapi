---
api:
  file: v2.json
  operationId: send-request-exchange-cancel
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
This request cancels the exchange and send request. It is required only if the send request involves an exchange (i.e., when the sending\_currency and the balance\_debit\_currency differ).

Note: If cancellation is possible, a generated cancellation link will be present in the actions\_required response of the send request.