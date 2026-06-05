---
title: Payment Channels Overview
deprecated: false
hidden: false
metadata:
  robots: index
---
<Callout icon="🚧" theme="warn">
  This feature is currently under development and available only for selected partners during the early access phase. To join the whitelist and receive updates about Payment Channels availability, visit: <Anchor label="CoinGate Payment Channels" target="_blank" href="https://coingate.com/payment-channels">CoinGate Payment Channels</Anchor>
</Callout>

Payment Channels allow merchants to create dedicated crypto payment addresses for their customers and receive recurring payments without creating a new Order for every transaction.

Unlike traditional crypto payment flows, Payment Channels do not expire after 20 minutes. Customers can send funds to the assigned payment address at any time, making them ideal for recurring deposits, account top-ups, customer wallets, and gaming platforms.

Funds received through a Payment Channel are automatically processed and converted to the merchant’s selected settlement currency (for example, EUR), allowing merchants to receive predictable settlement amounts without managing cryptocurrency exposure.

<Image align="center" src="https://files.readme.io/66765784fe7cd0eb4a05961ee4c728545b1ac5e569735c87b61d3005040a6291-payment-channel-flow.png" />

## Payment Channel Flow

### 1. Create Contact

```curl API
POST /contacts
```

A Contact represents the customer who will use the Payment Channel.

Merchants can optionally upload verification documents (e.g. passport, ID card, proof of address). These documents may help speed up compliance review if additional verification is required in the future.

Documentation: [https://developer.coingate.com/reference/create-contact](https://developer.coingate.com/reference/create-contact)

### 2. Create Payment Channel

```curl API
POST /payment-channels
```

A Payment Channel is a dedicated collection of cryptocurrency payment addresses assigned to a single Contact, allowing merchants to identify customers and receive recurring crypto payments to the same addresses.

It allows merchants to collect recurring payments from the same customer without generating a new payment address for every transaction.

For example, a gaming platform may create a Payment Channel for each player and allow them to top up their account using BTC, XRP, USDC, or other supported cryptocurrencies. The player can continue sending funds to the same addresses at any time.

When a payment is received, CoinGate automatically processes the payment, performs compliance checks, and settles the funds in the merchant’s selected settlement currency (for example, EUR).

Documentation: [https://developer.coingate.com/reference/create-payment-channel](https://developer.coingate.com/reference/create-payment-channel)

### 3. Receive Payment

The shopper sends cryptocurrency to the provided payment address.

CoinGate automatically processes the payment, performs compliance checks, and creates the related payment records.

### 4. Receive Payment Callback

After the payment is successfully processed, CoinGate sends an <Anchor label="API callback" target="_blank" href="https://developer.coingate.com/reference/api-callbacks">API callback</Anchor> to the merchant.

Merchants can use this callback to credit customer balances, fulfill orders, or update their internal systems.

Documentation: [https://developer.coingate.com/reference/payment-channel-order-callback](https://developer.coingate.com/reference/payment-channel-order-callback)