---
title: Send Request Callback
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
A callback will be sent to the merchant's **callback_url** when the send request is created or the status is changed

> 📘 API Callback Documentation
> 
> Read more about common callback functionalities in the [API Callbacks section](doc:api-callbacks).

CoinGate callback sends the data below:

[block:parameters]
{
  "data": {
    "h-0": "Name",
    "h-1": "Type",
    "h-2": "Value",
    "0-0": "`id`",
    "0-1": "Integer",
    "0-2": "Unique identifier for the send request.",
    "1-0": "`status`",
    "1-1": "String",
    "1-2": "The current status of the send request (e.g., pending, completed, failed). [Available Statuses](doc:send-request-statuses)",
    "2-0": "`purpose`",
    "2-1": "String",
    "2-2": "Description of the purpose of the Send Request.",
    "3-0": "`callback_url`",
    "3-1": "String",
    "3-2": "URL that will receive status change callbacks for this request.",
    "4-0": "`created_at`",
    "4-1": "String",
    "4-2": "Timestamp indicating when the send request was created.",
    "5-0": "`external_id`",
    "5-1": "String",
    "5-2": "A unique identifier provided by the merchant during record creation. (optional, string, max length: 50, uniq)",
    "6-0": "`ledger_account`",
    "6-1": "Hash",
    "6-2": "Ledger account used for deducting the sending amount.",
    "7-0": "`input_amount`",
    "7-1": "Float",
    "7-2": "The amount you intend to send in the specified `input_currency`.",
    "8-0": "`input_currency`",
    "8-1": "Hash",
    "8-2": "The currency in which the amount is provided. This will be converted into the `sending_currency` before sending. For example, if you want to send 100 EUR but the beneficiary’s currency is ETH, the amount will be converted accordingly.",
    "9-0": "`sending_amount`",
    "9-1": "Float",
    "9-2": "The actual amount that will be sent to the beneficiary after conversion.",
    "10-0": "`sending_currency`",
    "10-1": "Hash",
    "10-2": "The currency in which the beneficiary will receive the funds.",
    "11-0": "`input_to_sending_rate`",
    "11-1": "String",
    "11-2": "The exchange rate used to convert `input_amount` from `input_currency` to `sending_amount` in `sending_currency`. For example, if sending 100 EUR (`input_currency`) to ETH (`sending_currency`), this rate determines how much ETH the beneficiary receives.",
    "12-0": "`sending_to_balance_debit_rate`",
    "12-1": "String",
    "12-2": "The exchange rate between `sending_currency` and `balance_debit_currency`, used to determine the deducted amount from the ledger.",
    "13-0": "`balance_debit_amount`",
    "13-1": "Float",
    "13-2": "The amount deducted from the [ledger account](https://developer.coingate.com/reference/get-ledger-account). If the sending currency and ledger account currency differ, the amount will be converted before deduction. For example, if you send 0.1 ETH, but your ledger balance is in USDC, then the equivalent USDC amount will be deducted.",
    "14-0": "`balance_debit_currency`",
    "14-1": "Hash",
    "14-2": "The currency of the [ledger account](https://developer.coingate.com/reference/get-ledger-account) used for deduction.",
    "15-0": "`beneficiary_payout_setting`",
    "15-1": "Hash",
    "15-2": "The payout settings associated with the [beneficiary](https://developer.coingate.com/reference/create-beneficiary). The beneficiary currency is the same as `sending_currency`.",
    "16-0": "`fees`",
    "16-1": "Hash",
    "16-2": "The fees applied to the transaction. Possible fee types include:  \n  \n- `service_fee`: A fee for processing the transaction.\n- `conversion_fee`: A fee applied when converting between `sending_currency`and `balance_debit_currency`.",
    "17-0": "`blockchain_transactions`",
    "17-1": "Array",
    "17-2": "An array containing details of blockchain transactions related to this request. Each transaction includes:  \n  \n- `txid`: The blockchain transaction ID.\n- `amount`: The amount transferred in the transaction.\n- `status`: The current status of the transaction.\n- `network_confirmations`: The number of confirmations received on the blockchain.",
    "18-0": "`actions_required`",
    "18-1": "Hash",
    "18-2": "The `actions_required` field is present only when an exchange is needed (i.e., when `sending_currency` and `balance_debit_currency` are different). If currency conversion is not required, user confirmation is not needed. Note that the conversion is based on `sending_currency` and `balance_debit_currency`, not `input_currency`, even if the currencies differ. Possible actions: `PATCH(cancel)` or `PATCH(confirm)`.",
    "19-0": "`requires_2fa_confirmation`",
    "19-1": "Boolean",
    "19-2": "Indicates whether the operation requires additional manual confirmation in the account dashboard using two-factor authentication (2FA)."
  },
  "cols": 3,
  "rows": 20,
  "align": [
    null,
    null,
    null
  ]
}
[/block]


An example of callback in JSON:

```json
{
  "id": 11,
  "status": "draft",
  "purpose": "Sending 100 EUR Value",
  "callback_url": "https://example.com/callback_url",
  "created_at": "2025-03-13T00:45:17.250Z",
  "external_id": "1",
  "ledger_account": {
    "id": "01JNQWKKJ6WXN8BZT1Y66B6G9H",
    "balance": "1.0",
    "status": "active",
    "currency": {
      "id": 1,
      "title": "Bitcoin",
      "symbol": "BTC"
    }
  },
  "input_amount": "100.0",
  "input_currency": {
    "id": 2,
    "title": "Euro",
    "kind": "fiat",
    "symbol": "EUR"
  },
  "sending_amount": "0.049422",
  "sending_currency": {
    "id": 5,
    "title": "Ethereum",
    "kind": "crypto",
    "symbol": "ETH"
  },
  "input_to_sending_rate": "0.00049422",
  "sending_to_balance_debit_rate": "40.3258",
  "balance_debit_amount": "0.00122557",
  "balance_debit_currency": {
    "id": 1,
    "title": "Bitcoin",
    "kind": "crypto",
    "symbol": "BTC"
  },
  "beneficiary_payout_setting": {
    "id": 2,
    "created_at": "2025-03-07T10:39:33.152Z",
    "beneficiary_id": 1,
    "platform": {
      "id": 2,
      "title": "Ethereum",
      "id_name": "ethereum"
    },
    "crypto_address": "tb1qcq670zweall6zz4f96flfrefhr8myfxz9ll9l2",
    "crypto_address_metadata": null,
    "currency": {
      "id": 5,
      "title": "Ethereum",
      "kind": "crypto",
      "symbol": "ETH"
    }
  },
  "fees": {
    "service_fee": {
      "amount": "0.00001226",
      "currency": {
        "id": 1,
        "title": "Bitcoin",
        "kind": "crypto",
        "symbol": "BTC"
      }
    },
    "conversion_fee": {
      "amount": "0.00001226",
      "currency": {
        "id": 1,
        "title": "Bitcoin",
        "kind": "crypto",
        "symbol": "BTC"
      }
    }
  },
  "blockchain_transactions": [],
  "actions_required": {
    "confirm": "https://api.coingate.com/api/v2/send_requests/11/confirm",
    "cancel": "https://api.coingate.com/api/v2/send_requests/11/cancel"
  },
  "requires_2fa_confirmation": true
}
```