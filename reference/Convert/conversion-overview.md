---
title: Conversion Overview
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Our flexible Conversions API allows you to seamlessly convert between currencies—right from your dashboard or backend. Instantly exchange balances across supported currencies with real-time rates, all while staying secure and compliant. Whether you're preparing for a payout or managing treasury operations, our API makes currency conversion fast, accurate, and reliable. Get started today and simplify your multi-currency workflows!

### User Journey: Converting 100 EUR to a BTC

1. **Start with Your Ledger Balance**

You have a balance in EUR and want to convert 100 EUR to BTC.

2. **Create a Conversion**

Use the [Create Conversion API](https://developer.coingate.com/reference/create-conversion) to initiate the conversion.

Specify:

* The `ledger_account_id`  balance you want convert from. (In this case [EUR](https://developer.coingate.com/reference/ledger-accounts)).
* The `quote_currency_id`  currency you want convert to. (In this case [BTC](https://developer.coingate.com/reference/currencies)).
* The `base_amount` amount of ledger\_account balance want to convert. (In this case 100)

➡️ This step triggers conversion from EUR → BTC and calculates the required deduction in your balance.

3. **Review API Response for Action Requirements**

In the response, check the field `actions_required`.

* As operation requires confirmation or cancellation
* Use one of the following actions given in `actions_required` or API endpoints:
  * ✅ [Confirm Conversion](https://developer.coingate.com/reference/confirm-conversion)
  * ❌ [Cancel Conversion](https://developer.coingate.com/reference/cancel-conversion)

Once confirmed, your balance will be updated with the converted currency.
