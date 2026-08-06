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
A callback will be sent to the merchant's **callback\_url** when the send request is created or the status is changed

> 📘 API Callback Documentation
>
> Read more about common callback functionalities in the [API Callbacks section](doc:api-callbacks).

CoinGate callback sends the data below:

<Table>
  <thead>
    <tr>
      <th>
        Name
      </th>

      <th>
        Type
      </th>

      <th>
        Value
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        `id`
      </td>

      <td>
        Integer
      </td>

      <td>
        Unique identifier for the send request.
      </td>
    </tr>

    <tr>
      <td>
        `status`
      </td>

      <td>
        String
      </td>

      <td>
        The current status of the send request (e.g., pending, completed, failed). [Available Statuses](doc:send-request-statuses)
      </td>
    </tr>

    <tr>
      <td>
        `purpose`
      </td>

      <td>
        String
      </td>

      <td>
        Description of the purpose of the Send Request.
      </td>
    </tr>

    <tr>
      <td>
        `callback_url`
      </td>

      <td>
        String
      </td>

      <td>
        URL that will receive status change callbacks for this request.
      </td>
    </tr>

    <tr>
      <td>
        `created_at`
      </td>

      <td>
        String
      </td>

      <td>
        Timestamp indicating when the send request was created.
      </td>
    </tr>

    <tr>
      <td>
        `external_id`
      </td>

      <td>
        String
      </td>

      <td>
        A unique identifier provided by the merchant during record creation. (optional, string, max length: 50, uniq)
      </td>
    </tr>

    <tr>
      <td>
        `requestable_id`
      </td>

      <td>
        Integer
      </td>

      <td>
        ID of the batch payout or payout link the send request was created from. `null` when it was created directly.
      </td>
    </tr>

    <tr>
      <td>
        `requestable_type`
      </td>

      <td>
        String
      </td>

      <td>
        What created the send request — `batch_payout` or `payout_link`. `null` when it was created directly. Can be passed back to [List Send Requests](doc:list-send) as a filter.
      </td>
    </tr>

    <tr>
      <td>
        `ledger_account`
      </td>

      <td>
        Hash
      </td>

      <td>
        Ledger account used for deducting the sending amount.
      </td>
    </tr>

    <tr>
      <td>
        `input_amount`
      </td>

      <td>
        Float
      </td>

      <td>
        The amount you intend to send in the specified `input_currency`.
      </td>
    </tr>

    <tr>
      <td>
        `input_currency`
      </td>

      <td>
        Hash
      </td>

      <td>
        The currency in which the amount is provided. This will be converted into the `sending_currency` before sending. For example, if you want to send 100 EUR but the beneficiary’s currency is ETH, the amount will be converted accordingly.
      </td>
    </tr>

    <tr>
      <td>
        `sending_amount`
      </td>

      <td>
        Float
      </td>

      <td>
        The actual amount that will be sent to the beneficiary after conversion.
      </td>
    </tr>

    <tr>
      <td>
        `sending_currency`
      </td>

      <td>
        Hash
      </td>

      <td>
        The currency in which the beneficiary will receive the funds.
      </td>
    </tr>

    <tr>
      <td>
        `input_to_sending_rate`
      </td>

      <td>
        String
      </td>

      <td>
        The exchange rate used to convert `input_amount` from `input_currency` to `sending_amount` in `sending_currency`. For example, if sending 100 EUR (`input_currency`) to ETH (`sending_currency`), this rate determines how much ETH the beneficiary receives.
      </td>
    </tr>

    <tr>
      <td>
        `sending_to_balance_debit_rate`
      </td>

      <td>
        String
      </td>

      <td>
        The exchange rate between `sending_currency` and `balance_debit_currency`, used to determine the deducted amount from the ledger.
      </td>
    </tr>

    <tr>
      <td>
        `balance_debit_amount`
      </td>

      <td>
        Float
      </td>

      <td>
        The amount deducted from the [ledger account](https://developer.coingate.com/reference/get-ledger-account). If the sending currency and ledger account currency differ, the amount will be converted before deduction. For example, if you send 0.1 ETH, but your ledger balance is in USDC, then the equivalent USDC amount will be deducted.
      </td>
    </tr>

    <tr>
      <td>
        `balance_debit_currency`
      </td>

      <td>
        Hash
      </td>

      <td>
        The currency of the [ledger account](https://developer.coingate.com/reference/get-ledger-account) used for deduction.
      </td>
    </tr>

    <tr>
      <td>
        `beneficiary_payout_setting`
      </td>

      <td>
        Hash
      </td>

      <td>
        The payout settings associated with the [beneficiary](https://developer.coingate.com/reference/create-beneficiary). The beneficiary currency is the same as `sending_currency`.
      </td>
    </tr>

    <tr>
      <td>
        `fees`
      </td>

      <td>
        Hash
      </td>

      <td>
        The fees applied to the transaction. Possible fee types include:  

        * `service_fee`: A fee for processing the transaction.
        * `conversion_fee`: A fee applied when converting between `sending_currency`and `balance_debit_currency`.
      </td>
    </tr>

    <tr>
      <td>
        `blockchain_transactions`
      </td>

      <td>
        Array
      </td>

      <td>
        An array containing details of blockchain transactions related to this request. Each transaction includes:  

        * `txid`: The blockchain transaction ID.
        * `amount`: The amount transferred in the transaction.
        * `status`: The current status of the transaction.
        * `network_confirmations`: The number of confirmations received on the blockchain.
      </td>
    </tr>

    <tr>
      <td>
        `actions_required`
      </td>

      <td>
        Hash
      </td>

      <td>
        The `actions_required` field is present only when an exchange is needed (i.e., when `sending_currency` and `balance_debit_currency` are different). If currency conversion is not required, user confirmation is not needed. Note that the conversion is based on `sending_currency` and `balance_debit_currency`, not `input_currency`, even if the currencies differ. Possible actions: `PATCH(cancel)` or `PATCH(confirm)`.
      </td>
    </tr>

    <tr>
      <td>
        `requires_2fa_confirmation`
      </td>

      <td>
        Boolean
      </td>

      <td>
        Indicates whether the operation requires additional manual confirmation in the account dashboard using two-factor authentication (2FA).
      </td>
    </tr>
  </tbody>
</Table>

An example of callback in JSON:

```json
{
  "id": 11,
  "status": "draft",
  "purpose": "Sending 100 EUR Value",
  "callback_url": "https://example.com/callback_url",
  "created_at": "2025-03-13T00:45:17.250Z",
  "external_id": "1",
  "requestable_id": 7,
  "requestable_type": "batch_payout",
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
