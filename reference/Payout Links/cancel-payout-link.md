---
api:
  file: v2.json
  operationId: cancel-payout-link
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Cancels a payout link that has not been collected yet and returns the reserved amount to the ledger account it came from.

Only `draft` and `pending` links can be canceled. Anything else returns `422` with `reason: PayoutLinkIsNotValid` and leaves the status untouched — a link that has already been collected cannot be recalled.

An uncollected link that reaches `expires_at` is refunded the same way without you calling anything.
