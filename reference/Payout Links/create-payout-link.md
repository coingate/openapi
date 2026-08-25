---
api:
  file: v2.json
  operationId: create-payout-link
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Reserves the amount from the ledger account you name and returns a collect URL in `payout_link_url`. The recipient chooses their currency and payout method when they open it, so nothing about the payout destination is sent here.

Amounts are converted at creation time and the rate is fixed from then on. See [Payout Links Overview](https://developer.coingate.com/reference/payout-link-overview) for how `balance_debit_amount` and `fees.service_fee.amount` add up to what leaves your ledger account.

> 📘 The link is created in `draft`, not `pending`, when payout approvals are enabled on your account
>
> It has to be approved in the dashboard before the recipient can collect it, and links created through the API need two different approvers. See [Payout Link Statuses](https://developer.coingate.com/reference/payout-link-statuses).

Set `send_email: true` to have CoinGate email the link to `recipient_email`. Otherwise deliver `payout_link_url` yourself — only that email address can collect it either way.

The recipient also confirms the payout from `recipient_email` before it is sent, so it has to be a real, working mailbox. A temporary, disposable or mistyped address leaves the recipient unable to approve the payout, and the link stays uncollected until it expires.
