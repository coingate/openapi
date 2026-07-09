---
title: CoinGate Cryptocurrency Payment API
excerpt: Accept, convert, and send cryptocurrency payments with a single API
deprecated: false
hidden: false
metadata:
  title: CoinGate Payment Processing API Overview
  description: ''
  robots: index
next:
  pages:
    - slug: api-overview
      title: API Overview
      type: endpoint
---
CoinGate is a licensed cryptocurrency payment gateway for online businesses. Accept BTC, ETH, USDC, and dozens of other [currencies across major networks](https://coingate.com/supported-currencies) — including TRON, Solana, and Layer 2s like Base and Arbitrum — and settle in crypto or fiat (EUR, USD, GBP).

Integrate directly via the API below, or use our ready-made [ecommerce plugins](https://coingate.com/plugins) for WooCommerce, WHMCS, PrestaShop, and other platforms.

## Make your first request

Create an order and you get back a `payment_url` — a hosted checkout page where your customer picks a currency and pays. That's the whole integration in its simplest form.

> 📘 Test for free in the sandbox
>
> Generate a sandbox API key at [sandbox.coingate.com](https://sandbox.coingate.com) (production keys don't work in sandbox), then run the request below. See [Environments](https://developer.coingate.com/reference/environments) and [API Authentication](https://developer.coingate.com/reference/api-authentication).

```curl
curl -X POST https://api-sandbox.coingate.com/v2/orders \
  -H 'Authorization: Token YOUR_API_TOKEN' \
  -H 'Content-Type: application/json' \
  -d '{
        "order_id": "YOUR-ORDER-123",
        "price_amount": 99.99,
        "price_currency": "EUR",
        "receive_currency": "EUR",
        "title": "Order #123",
        "description": "1 x Apple MacBook Air",
        "callback_url": "https://example.com/payments/callback",
        "success_url": "https://example.com/payments/success",
        "cancel_url": "https://example.com/payments/cancel"
      }'
```
```json Response
{
  "id": 538,
  "status": "new",
  "title": "Order #123",
  "price_currency": "EUR",
  "price_amount": "99.99",
  "receive_currency": "EUR",
  "order_id": "YOUR-ORDER-123",
  "payment_url": "https://pay.coingate.com/invoice/a275c4a1-fc54-45b1-a98a-66652e338fb2",
  "token": "PsPXSa46uohMtMWqfzTrnwy3p3sNmQ",
  "created_at": "2025-12-09T14:02:41+00:00"
}
```

## How it works

1. **Create an order** — call [Create Order](https://developer.coingate.com/reference/create-order) with the amount and currency.
2. **Redirect your customer** to the `payment_url` from the response. They choose a cryptocurrency and complete the payment on the hosted checkout.
3. **Get notified** — CoinGate sends a [payment callback](https://developer.coingate.com/reference/api-callbacks) to your `callback_url` on every status change, and settles the funds in crypto or fiat to your account.

## Accept payments

<Cards columns={2}>
  <Card title="Payments" icon="fa-bolt" href="https://developer.coingate.com/reference/api-overview">
    Create an order, redirect to checkout, get settled — the full payment lifecycle in a few API calls.
  </Card>
  <Card title="Payment Channels" icon="fa-arrows-rotate" href="https://developer.coingate.com/reference/payment-channels-overview">
    Dedicated, non-expiring deposit addresses per customer. Deposits are auto-detected, attributed, compliance-checked, and settled.
  </Card>
  <Card title="Binance Pay" icon="fa-qrcode" href="https://developer.coingate.com/reference/binance-checkout">
    Included with your CoinGate integration: millions of Binance users can pay straight from their Binance account.
  </Card>
  <Card title="Underpaid Cover" icon="fa-shield-halved" href="https://support.coingate.com/hc/en-us/articles/4402498932114">
    Accept invoices underpaid by up to 10%, so near-complete payments don't fail or expire.
  </Card>
</Cards>

## Move & manage funds

<Cards columns={2}>
  <Card title="Payouts" icon="fa-paper-plane" href="https://developer.coingate.com/reference/send-request-overview">
    Send crypto to employees, vendors, or users — one-off, at scale, or as no-code CSV batches.
  </Card>
  <Card title="Convert" icon="fa-arrow-right-arrow-left" href="https://developer.coingate.com/reference/conversion-overview">
    Swap between supported crypto and fiat at real-time rates, credited straight to your CoinGate balance.
  </Card>
  <Card title="Refunds" icon="fa-rotate-left" href="https://developer.coingate.com/reference/create-refund">
    Issue full or partial refunds with transparent status tracking for you and your customer.
  </Card>
  <Card title="Billing" icon="fa-file-invoice" href="https://developer.coingate.com/reference/billing-overview">
    Create one-off or recurring crypto invoices with due dates, and track them via API or dashboard.
  </Card>
</Cards>

## Developer essentials

* [Sandbox environment](https://developer.coingate.com/reference/environments) for safe integration testing
* API keys with [permission controls](https://coingate.com/blog/post/business-user-permissions)
* [Libraries](https://developer.coingate.com/reference/code-libraries) in popular programming languages
* A working [shop example](https://example.coingate.com/) you can try end to end
* Every payment, conversion, payout, and refund is traceable in your [dashboard](https://coingate.com), with exportable reports for accounting

## Licensed & regulated

> 🛡️ MiCA-authorised in the EU
>
> CoinGate (UAB Decentralized) is authorised as a Crypto-Asset Service Provider under the EU Markets in Crypto-Assets Regulation (MiCA) and licensed as a Payment Institution by the Bank of Lithuania.

_UAB Decentralized, a private limited liability company incorporated in Lithuania, is authorised as a Crypto-Asset Service Provider under the EU Markets in Crypto-Assets Regulation (MiCA) by the Bank of Lithuania (Authorization code: LB002323) to provide crypto-asset services. UAB Decentralized is also licensed as a Payment institution by the Bank of Lithuania (Authorization code: LB002324) to provide transfer services for Electronic Money Tokens. Crypto-assets are high-risk investments and may result in partial or total loss of capital._
