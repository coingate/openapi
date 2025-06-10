---
title: Send Request Overview
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
Our powerful Send Request API lets you send cryptocurrency to third-party beneficiaries in a fast, secure, and compliant way—right from your dashboard or backend. Whether you’re sending in the same currency or converting on the fly. Get started today and streamline your crypto payouts!

## Use Cases

1. Sending the same currency with no conversion
   1. The beneficiary has a payout setting in **USDC**.
   2. Your ledger account balance is also in **USDC**.
   3. You want to send **100 USDC** to the beneficiary.
   4. **Result:** **100 USDC** is deducted from your ledger account without any conversion.
2. Sending a different input currency, but the beneficiary receives USDC
   1. The beneficiary has a payout setting in **USDC**.
   2. Your ledger account balance is in **USDC**.
   3. You want to send **100 EUR** to the beneficiary.
   4. **Result:** **100 EUR** is converted to **USDC**, and the equivalent **USDC** amount is sent to the beneficiary. The corresponding **USDC** amount is deducted from your ledger account.
3. Sending a different input currency, with both conversion and ledger deduction in a different currency
   1. The beneficiary has a payout setting in **BTC**.
   2. Your ledger account balance is in **USDC**.
   3. You want to send **100 EUR** to the beneficiary.
   4. **Result:** **100 EUR** is converted to **BTC** for the beneficiary. Then, the equivalent **BTC** amount is converted to **USDC**, and the corresponding **USDC** amount is deducted from your ledger account.

<br />

### User Journey: Sending 100 EUR to a BTC Beneficiary (From USDC Balance)

1. **Start with Your Ledger Balance**

You have a balance in USDC and want to send 100 EUR worth of BTC to a third-party beneficiary whose payout currency is BTC.

2. **Create a Send Request**

Use the [Create Send Request API](https://developer.coingate.com/reference/create-send) to initiate the transfer.

Specify:

- The ledger account (in USDC).
- The beneficiary (with BTC payout settings).
- The input amount: 100
- The input currency: EUR

➡️ This step triggers conversion from EUR → BTC and calculates the required deduction in your USDC balance.

3. **Review API Response for Action Requirements**

In the response, check the field [actions_required](https://developer.coingate.com/reference/send-request-callback).

- If this field is present, the operation requires additional confirmation due to currency exchange.
- Use one of the following API endpoints:
  - ✅ [Confirm the send request](https://developer.coingate.com/reference/send-request-exchange-confirm)
  - ❌ [Cancel the send request](https://developer.coingate.com/reference/send-request-exchange-cancel)

4. **Check for 2FA Confirmation Requirement**

Also, check the [requires_2fa_confirmation](https://developer.coingate.com/reference/send-request-callback) field in the response.

- If true, you must manually confirm the operation in your account dashboard using two-factor authentication (2FA).
- If needed, 2FA confirmation can be disabled in the [dashboard settings](https://developer.coingate.com/reference/create-send).