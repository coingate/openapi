---
api:
  file: v2.json
  operationId: get_payment-channels-supported-currencies
deprecated: false
hidden: false
link:
  new_tab: false
metadata:
  robots: index
---
<br />

<Callout icon="🚧" theme="warn">
  This feature is currently under development and available only for selected partners during the early access phase. To join the whitelist and receive updates about Payment Channels availability, visit: <Anchor label="CoinGate Payment Channels" target="_blank" href="https://coingate.com/payment-channels">CoinGate Payment Channels</Anchor>
</Callout>

Returns the list of crypto currencies (and their platforms) a Payment Channel can accept deposits in. Use this endpoint to populate the asset selector when creating a payment channel — each returned `{ id, platforms[].id }` pair maps to a `{ currency_id, platform_id }` entry in the `assets` array of the create-payment-channel request, and a deposit address will be generated for each selected pair.

<br />
