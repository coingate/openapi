---
title: Environments
deprecated: false
hidden: false
metadata:
  robots: index
---
CoinGate provides two separate environments: **Live** and **Sandbox**.

| Environment | URL                                   |
| :---------- | :------------------------------------ |
| **Live**    | `https://api.coingate.com/v2`         |
| **Sandbox** | `https://api-sandbox.coingate.com/v2` |

### Live Environment

The Live environment is the production environment where all operations are real and executed on the mainnet blockchain.

To use this environment, you must complete merchant verification:\
👉 <Anchor label="How to verify your merchant account" target="_blank" href="https://coingate.com/blog/post/verify-merchant-account-faq">How to verify your merchant account</Anchor>

### Sandbox Environment

The Sandbox environment is intended for **testing purposes only**.\
In this environment, you can use any API or dashboard functionality without verification. All operations are executed on the **testnet blockchain**.
You can simply create an account and start testing via the dashboard or integrate the API:
👉 <Anchor label="CoinGate Sandbox" target="_blank" href="https://sandbox.coingate.com">CoinGate Sandbox</Anchor>

### Key Differences

* **Separate Systems**:\
  Live and Sandbox are entirely separate environments. This means you need to create separate accounts for each.
* **Separate API Credentials**:\
  If you’re working in “Test” (Sandbox) mode, you must generate API credentials on <Anchor label="sandbox.coingate.com" target="_blank" href="https://sandbox.coingate.com">sandbox.coingate.com</Anchor>.
* **Different Currencies and Platforms**:\
  The list of supported currencies (<Anchor label="reference" target="_blank" href="https://developer.coingate.com/reference/currencies">reference</Anchor>) and platforms ([reference](https://developer.coingate.com/reference/platforms)) differs between Live and Sandbox.
  The Sandbox environment supports fewer currencies and platforms, and the id values for currencies and platforms are different between environments.

> Always ensure you’re using the correct credentials and references based on the environment you’re working in.