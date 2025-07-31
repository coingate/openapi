---
title: API Overview
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: CoinGate Payment Processing API Overview
  description: ''
  robots: index
next:
  pages:
    - slug: environments
      title: Environments
      type: endpoint
---
<Image align="center" src="https://files.readme.io/8c280ba41fd11925348badbe72e65998d4cacb8720de4a4953f1b2d6b6b42814-API_-_Create_Order1.png" />

The CoinGate Payment Processing API allows you to seamlessly accept cryptocurrency payments and settle them in fiat currencies (EUR, USD, GBP) or crypto. The integration is designed to be lightweight, cost-efficient, and developer-friendly—helping merchants expand their global reach by accepting payments in Bitcoin, Ethereum, and other digital assets.

With CoinGate, your customers can pay in crypto, while you receive payouts in fiat or crypto with automatic conversion.

## 📌 How It Works – Example Flow

1. A customer selects crypto as the payment method for a €100 order.
2. Based on real-time rates, they’re shown the amount to pay in their chosen cryptocurrency.
3. After payment confirmation, you receive \~€99 (minus fees) in your CoinGate account.
4. You can withdraw funds to your bank in EUR, USD, or GBP—or hold them in crypto.

## 🔧 Integration Setup

Follow these steps to integrate CoinGate into your checkout flow:

1. **Create an Order**\
   Use the [Create Order API](https://developer.coingate.com/reference/create-order)  to initiate a new payment.
2. **Validate Order Response**

   2.1 If the order is valid, CoinGate will respond with `HTTP 200 OK` and return the order data, including the `payment_url`.

   ➤ Redirect the customer to this `payment_url` so they can complete the payment.

   2.2 If the order is invalid, you’ll receive an error (`422 Unprocessable Entity`) along with a message explaining why the order could not be created.
3. **Customer Makes a Payment**\
   The shopper selects their preferred currency and blockchain platform (if applicable) and proceeds with the crypto payment.
4. **Receive Payment Status via Callback**\
   CoinGate will notify your system of payment status changes using the [Payment Callback API](https://developer.coingate.com/reference/payment-callback) .
   ➤ Handle these callbacks in your backend to update the order status accordingly in your e-commerce system.