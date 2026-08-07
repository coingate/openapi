---
api:
  file: v2.json
  operationId: checkout
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# Displaying payment details on your own site

Calls from accounts without access to the checkout method return status code 422.

The checkout method returns the payment details of an order so you can display them on your own page instead of redirecting the shopper to CoinGate.

This is achieved by pre-selecting BTC, LTC, etc as the payment currency, and retrieving the `pay_amount` and `payment_address` parameters. These are sufficient for a customer to complete the payment, as well as to generate a QR code which a customer can scan with a mobile wallet.

## What you give up with this endpoint

The response gives you `payment_address` and `pay_amount` and nothing else. Everything the CoinGate invoice does today becomes yours to build and maintain.

- **Refunds are on you.** [Create Order Refund](https://developer.coingate.com/reference/create-refund) needs the shopper's address and email, which the hosted invoice collects and confirms for you.
- **No Binance Pay.** It has a separate integration, [Binance Checkout](https://developer.coingate.com/reference/binance-checkout).
- **No WalletConnect.** Shoppers copy the address or scan a QR code you render.
- **You supply shopper data.** We never see the shopper, so Travel Rule and risk data must come from you in the [shopper object](https://developer.coingate.com/reference/create-order).
- **You build the payment page.** QR code, amount display, expiry countdown, paid and expired states, underpayments.
- **New payment methods do not reach you.** What we add to the hosted invoice is free for `payment_url` merchants and needs code changes here.