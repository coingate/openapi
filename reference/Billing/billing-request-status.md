---
title: Billing overview
excerpt: >-
  The Billing Service enables you to request specific payments from your
  clients. It functions similarly to an advance payment invoice.


  ##Key Features

  **Billing Contacts**

  These are dedicated, billing-only customer contact records used for payment
  management.


  **Products (Optional)**

  Products are currency-specific, meaning each billing request can be created in
  a single currency, identified by a currency_id.

  You can choose to skip defining products and instead specify only the payment
  amount and currency.

  Additionally, setting a title for the billing request is optional.


  **Billing Request**

  The core of the service, a billing request, includes various statuses and
  configurable options:

  - due_days: Specifies the number of days within which the payment must be
  completed. If the payment is not completed in this timeframe, the request will
  expire.

  - underpaid_cover_pct: A percentage (0-10%) to cover minor underpayments.

  - receive_currency_id: Defines the currency in which you will receive the
  settlement.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
| Status    | Description                                                                                                                       |
| :-------- | :-------------------------------------------------------------------------------------------------------------------------------- |
| pending   | This is the initial status of the billing request, indicating that the request has been created.                                  |
| completed | The status changes to "Completed" when the client successfully pays the billing request.                                          |
| expired   | If the billing request has a due_days, and that time has passed without payment from the client, the status changes to "Expired." |
| canceled  | This status is applied when the billing request is terminated or revoked, meaning it will no longer be processed or paid.         |

## Status Changing Flow

![](https://files.readme.io/57f797dc28a0e8fe27eda4aec376e20c6bffaf9106071ddfb7a6e25d9a0fe1b9-image.png)