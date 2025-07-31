---
title: Get Currencies
excerpt: >-
  Retrieve the list of supported currencies for payment processing, including
  shopper payment currencies, pricing currencies, and settlement currencies.
api:
  file: v2.json
  operationId: currencies
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
This API provides information about supported currencies used in CoinGate’s merchant integrations for payment processing. It helps you determine:

* In which currencies shoppers can pay (merchant\_pay)
* In which currencies you, as a merchant, can receive settlements (merchant\_receive)
* In which currencies you can set product or service prices (merchant\_price)

### Other Related Endpoints

If you are looking for supported currencies in other services, refer to the following endpoints:

* [Merchant Refund Supported Currencies](https://developer.coingate.com/reference/refund-supported-currencies)
* [Payouts (Send) Supported Currencies](https://developer.coingate.com/reference/supported-payout-currencies-and-crypto-platforms)
* [Deposit Supported Currencies](https://developer.coingate.com/reference/deposit-supported-currencies)

### Common Usage Examples

Currencies in which shoppers can pay:

```curl
curl https://api.coingate.com/api/v2/currencies?merchant_pay=true
curl https://api.coingate.com/v2/currencies?merchant_pay=true&enabled=true
```

Currencies in which merchants can receive settlements:

```curl
curl https://api.coingate.com/v2/currencies?merchant_receive=true
```

#### Notes

* The `disabled` field in the response indicates that the currency is **temporarily unavailable** for use as a payment currency. You may optionally display the disabled\_message (in English) to inform users why the currency is disabled.
* The `native` field indicates whether the currency is natively supported by CoinGate. If native: false, it means the currency is processed via a third-party service.\
  *Currently, all shopper pay currencies are natively supported (native: true).*