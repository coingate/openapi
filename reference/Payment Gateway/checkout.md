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
<Callout icon="❗️" theme="error">
  The /checkout API endpoint is available only for selected merchants. If you would like to enable this functionality for your account, please contact [CoinGate Support](https://support.coingate.com/hc/en-us/requests/new) for assistance.
</Callout>

# White-label invoices using Checkout method

To utilize the checkout method, please contact our support team to enable this feature for your account. If this step is not completed, the API will return an error with status code 422.

Using Checkout method, invoices can be white-labelled and integrated into your website, without redirecting the customer to CoinGate.

This is achieved by pre-selecting BTC, LTC, etc as the payment currency, and retrieving the `pay_amount` and `payment_address` parameters. These are sufficient for a customer to complete the payment, as well as to generate a QR code which a customer can scan with a mobile wallet.