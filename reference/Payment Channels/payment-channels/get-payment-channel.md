---
api:
  file: v2.json
  operationId: get_payment-channels-id
hidden: true
link:
  new_tab: false
metadata:
  robots: index
---
<Callout icon="🚧" theme="warn">
  This feature is currently under development and available only for selected partners during the early access phase. To join the whitelist and receive updates about Payment Channels availability, visit: <Anchor label="CoinGate Payment Channels" target="_blank" href="https://coingate.com/payment-channels">CoinGate Payment Channels</Anchor>
</Callout>

Retrieve a single payment channel by its ID, including its configuration (receive currency, payment purpose, callback URL) and the full list of generated deposit addresses with their current status. Use this to check a channel's state — for example to confirm an `enqueued` address has become `active` and its `address` has been populated.