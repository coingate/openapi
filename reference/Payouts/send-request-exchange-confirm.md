---
title: Send Request Exchange Confirm
excerpt: ''
api:
  file: v2.json
  operationId: send-request-exchange-confirm
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
This request confirms the exchange of a send request. It is required only if the send request involves an exchange (i.e., when the sending_currency and the balance_debit_currency differ).

Note: If confirmation is needed, a generated confirmation link will be present in the actions_required response of the send request.