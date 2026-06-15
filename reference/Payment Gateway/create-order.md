---
api:
  file: v2.json
  operationId: create-order
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
The order is placed with the "Create Order" API method. From the user's point of view, at the moment of creating the order, the user is redirected to (*payment\_url*) our payment page (invoice), where shopper can see the payment amount, select the desired payment currency and complete the payment.

Note on the *receive\_currency* parameter - this is your settlement currency. When EUR is selected, all your received payments are immediately settled on exchanges to guarantee a fixed payout for each order. By selecting BTC, ETH, LTC or BCH as your settlement currency, you will automatically be credited with the chosen cryptocurrency (e.g. if BTC is your receive\_currency and your customer pays with ETH, you will be credited BTC according to the real-time market rate locked at the moment the invoice is generated). To keep the coins which your customers pay with, use DO\_NOT\_CONVERT as your receive\_currency (e.g. if a customer pays in BTC, you will be credited BTC, and if the customer pays in ETH, you will be credited with ETH). Please contact our support for further clarification, if needed.

> 📘 Shopper Object
>
> Since 2025, the shopper object has been introduced to enhance the customer experience and simplify Travel Rule compliance by pre-filling the Travel Rule form during checkout. Learn more about the Travel Rule <Anchor label="here" target="_blank" href="https://coingate.com/blog/post/travel-rule-explained">here</Anchor>.
>
> All fields within the shopper object are **optional**. For example, if you only have the shopper’s email, first name, and last name, you may leave all other fields empty. Any provided values will be automatically prefilled on the checkout form, and the remaining fields will be filled on the checkout form by the shopper.