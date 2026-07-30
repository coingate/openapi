---
api:
  file: v2.json
  operationId: platform-available
hidden: false
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: ''
---
Checks whether a specific payment platform (network) is currently operational. Use it before offering a network to confirm that CoinGate can process payments on that chain right now. The platform is identified by its `id_name`, as returned by the [Platforms](https://developer.coingate.com/reference/platforms) endpoint.
