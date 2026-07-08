---
api:
  file: v2.json
  operationId: get_payment-channels-supported-currencies
hidden: false
link:
  new_tab: false
metadata:
  robots: index
---
<br />

<Callout icon="📘" theme="info">
  Payment Channels are ready to use. Access is granted on request — to request access, contact our sales team via <Anchor label="CoinGate Payment Channels" target="_blank" href="https://coingate.com/payment-channels">CoinGate Payment Channels</Anchor>.
</Callout>

Returns the list of crypto currencies (and their platforms) a Payment Channel can accept deposits in. Use this endpoint to populate the asset selector when creating a payment channel — each returned `{ id, platforms[].id }` pair maps to a `{ currency_id, platform_id }` entry in the `assets` array of the create-payment-channel request, and a deposit address will be generated for each selected pair.

<br />