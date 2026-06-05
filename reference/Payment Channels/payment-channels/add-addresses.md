---
api:
  file: v2.json
  operationId: post_payment-channels-id-addresses
hidden: false
link:
  new_tab: false
metadata:
  robots: index
---
Generate additional deposit addresses on an existing payment channel. Use this when you want to accept a new asset (currency / network pair) on a channel that's already in use, without creating a second channel.

The endpoint is idempotent at the asset-pair level — submitting an asset that already has a generated address on this channel is silently skipped (no error, just no new address). Only fresh `{ currency_id, platform_id }` pairs produce a new address.