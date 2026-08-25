---
title: Payout Links Overview
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
A payout link lets you pay someone who does not have a CoinGate account and whose payout details you do not know. You create the link for an amount, CoinGate reserves that amount from your ledger account and returns a URL, and the recipient chooses the currency and payout method themselves when they open it.

This is the difference from a [Send Request](https://developer.coingate.com/reference/send-request-overview): a send request needs a beneficiary with a saved payout setting, a payout link does not.

## Before you start

You need an active ledger account with enough balance to cover the amount and the fee. Ledger account IDs come from [List Ledger Accounts](https://developer.coingate.com/reference/ledger-accounts).

## How it works

1. **Create the link.** Call [Create Payout Link](https://developer.coingate.com/reference/create-payout-link) with the ledger account, the amount, the purpose, how long the link stays open for collection, and the recipient's email address.
2. **CoinGate reserves the funds.** The amount is converted to the ledger account currency and deducted immediately, so the money is committed the moment the link exists, not when it is collected.
3. **Deliver the link.** The response contains `payout_link_url`. Set `send_email: true` to have CoinGate email it to `recipient_email`, or leave it off and deliver the URL yourself.
4. **The recipient collects it.** Only the `recipient_email` address can collect the link. They pick the currency and payout method at collection time, which is why the response has no payout destination on it.
5. **Track the outcome.** Poll [Get Payout Link](https://developer.coingate.com/reference/get-payout-link) or set a `callback_url` and let CoinGate push every status change to you. See [Payout Link Statuses](https://developer.coingate.com/reference/payout-link-statuses) and [Payout Link Callback](https://developer.coingate.com/reference/payout-link-callback).

## Amounts and fees

Two amounts appear on the payout link object:

| Field                  | Meaning                                                                                      |
| :--------------------- | :------------------------------------------------------------------------------------------- |
| `input_amount`         | What you asked for, in `input_currency`.                                                     |
| `balance_debit_amount` | The value the recipient collects, in the ledger account currency (`balance_debit_currency`). |

The total reserved from your ledger account is `balance_debit_amount` plus the processing fee in `fees.service_fee.amount`. Fees are always added on top of the payout, so the recipient collects the full `balance_debit_amount`.

The conversion rate is fixed when the link is created, so the value the recipient collects does not move while the link is waiting.

## Getting the money back

The reserved amount returns to the ledger account it came from when the link is [canceled](https://developer.coingate.com/reference/cancel-payout-link) or when it expires uncollected. A link can be collected until the end of the day, UTC, that `expires_at` falls on — `expires_in_days` accepts 1 to 7 days.

## Payout approvals

If payout approvals are enabled on your account, a new link is created in `draft` and has to be approved in the dashboard before the recipient can collect it. Links created through the API require **two different approvers**: the API authenticates with a key rather than a user, so CoinGate cannot tell who made the call and requires a second person to sign off.

With approvals off, links are created in `pending` and can be collected straight away.
