---
title: Payout Link Statuses
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
| Status     | Description                                                                                                                                                        |
| :--------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| draft      | Created while payout approvals are enabled on your account, waiting to be approved in the dashboard. Links created through the API need two different approvers.    |
| pending    | Live and waiting for the recipient to claim it. The amount is already reserved from your ledger account.                                                            |
| processing | The recipient claimed the link and the payout is on its way. `claimed_at` is set at this point.                                                                     |
| completed  | The payout reached the recipient.                                                                                                                                  |
| expired    | Nobody claimed the link before `expires_at`. The reserved amount was returned to your ledger account.                                                               |
| failed     | The payout could not be completed.                                                                                                                                 |
| canceled   | You canceled the link before it was claimed. The reserved amount was returned to your ledger account.                                                               |

Only `draft` and `pending` links can be canceled — see [Cancel Payout Link](https://developer.coingate.com/reference/cancel-payout-link).
