---
api:
  file: v2.json
  operationId: list-payout-links
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Returns the payout links that belong to the authenticated account, newest first, wrapped in a pagination envelope (`current_page`, `per_page`, `total_records`, `total_pages`).

Each entry has the same shape as [Get Payout Link](https://developer.coingate.com/reference/get-payout-link).
