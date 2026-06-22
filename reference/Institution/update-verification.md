---
api:
  file: v2.json
  operationId: update-verification
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
The verification must be in the `edited` status to accept submissions. By default (`upsert: true`) array sections such as business partners and shareholders are merged into the existing records. Set `upsert: false` to replace them instead — only non-empty sections are touched, and records added by CoinGate admins are preserved.
