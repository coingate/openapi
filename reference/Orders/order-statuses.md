---
title: Order Statuses
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
  "body": "API v1 is DEPRECATED and no longer maintained. Please use API v2 http://developer.coingate.com/v2",
  "title": "API v1 is DEPRECATED"
}
[/block]

[block:parameters]
{
  "data": {
    "h-0": "Status",
    "h-1": "Description",
    "0-0": "pending",
    "0-1": "Awaiting payment from the buyer.",
    "1-0": "confirming",
    "1-1": "Buyer sent a payment for the invoice. Waiting for confirmation from the Bitcoin network. \nIt can take up to:\n* ~10 sec if price < 300 EUR\n*  [~10 min](https://blockchain.info/charts/avg-confirmation-time) if price >= 300 EUR",
    "2-0": "paid",
    "2-1": "Payment confirmed by the Bitcoin network and merchant order is \"ready to be shipped\".",
    "3-0": "invalid",
    "3-1": "Payment rejected by the Bitcoin network.",
    "4-0": "expired",
    "4-1": "Buyer did not pay within 20 minutes and the invoice expired.",
    "5-0": "canceled",
    "5-1": "Buyer canceled the invoice.",
    "6-0": "refunded",
    "6-1": "Payment refunded to buyer or merchant."
  },
  "cols": 2,
  "rows": 7
}
[/block]
**Statuses by priority:**
1. pending
2. confirming
3. paid OR invalid OR expired OR canceled
4. refunded
[block:api-header]
{
  "type": "basic",
  "title": "Statuses and Merchant App Behavior"
}
[/block]

[block:parameters]
{
  "data": {
    "h-0": "Status",
    "h-1": "Behavior",
    "h-2": "Sends Callback",
    "0-0": "pending",
    "0-1": "Mark order status as *unpaid* in database.\nDisplay \"Unpaid\" order status for buyer.",
    "0-2": "No",
    "1-0": "confirming",
    "2-0": "paid",
    "1-1": "Mark order status as *pending* or *confirming* or *processing* in database. \nDisplay \"Waiting payment from CoinGate\" status for buyer.",
    "1-2": "Yes*",
    "2-1": "Mark order as *paid* in database.\nDisplay \"Paid\" order status for buyer.",
    "3-0": "invalid",
    "3-1": "Mark order as *invalid* or *rejected* in database.\nDisplay \"Invalid\" or \"Rejected\" order status for buyer.",
    "4-0": "expired",
    "4-1": "Mark order as *expired* or *unpaid* in database. \nDisplay \"Expired\" or \"Unpaid\" order status for buyer.",
    "5-0": "canceled",
    "5-1": "Mark order as *canceled* or *unpaid* in database.\nDisplay \"Canceled\" or \"Unpaid\" order status for buyer.",
    "2-2": "Yes",
    "3-2": "Yes",
    "4-2": "Yes",
    "5-2": "Yes",
    "6-0": "refunded",
    "6-1": "Mark order as *refunded* in database.\nDisplay \"Refunded\" or \"Unpaid\" order status for buyer.",
    "6-2": "Yes"
  },
  "cols": 3,
  "rows": 7
}
[/block]
*The "confirming" status is sometimes skipped and "paid" or "invalid" status is sent instead.