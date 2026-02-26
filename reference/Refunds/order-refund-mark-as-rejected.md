---
title: Mark as Rejected
api:
  file: v2.json
  operationId: patch_orders-order-id-refunds-refund-id-mark-as-rejected
deprecated: false
hidden: false
link:
  new_tab: false
metadata:
  robots: index
---
Marks a pending refund as rejected, triggering the same business logic as the "Mark as Rejected" action in the Account Dashboard — including updating the order refund status and sending notification emails and API callbacks to the merchant and shopper. **Available in sandbox environment only**.