---
title: Types of Refund Status
excerpt: >-
  The merchant refund system uses three statuses to keep both merchants and
  shoppers in the loop about the refund process. Each status provides a clear
  snapshot of where the refund is at any given moment.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
| Status     | Description                                                                                                                                                                                                                 |
| :--------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Pending    | This is the initial status assigned when a merchant initiates a refund.                                                                                                                                                     |
| Processing | Payment is being processed for the merchant refund. This status is optional depending on the internal CoinGate's workflows.                                                                                                 |
| Rejected   | The refund has been halted and will not proceed further. This happens either in compliance with internal policies and laws, or because the shopper has not approved the return address for the funds. This is final status. |
| Completed  | This status indicates that the refund process has been successfully executed. The funds have been sent to the shopper's designated crypto wallet address. This is final status.                                             |