---
title: Order Statuses
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: ''
---
> ❗️ API v1 is DEPRECATED
>
> API v1 is DEPRECATED and no longer maintained. Please use API v2 [http://developer.coingate.com/v2](http://developer.coingate.com/v2)

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th style={{ textAlign: "left" }}>
        Status
      </th>

      <th style={{ textAlign: "left" }}>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        pending
      </td>

      <td style={{ textAlign: "left" }}>
        Awaiting payment from the buyer.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        confirming
      </td>

      <td style={{ textAlign: "left" }}>
        Buyer sent a payment for the invoice. Waiting for confirmation from the Bitcoin network.\
        It can take up to:

        * \~10 sec if price \< 300 EUR
        * [\~10 min](https://blockchain.info/charts/avg-confirmation-time) if price >= 300 EUR
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        paid
      </td>

      <td style={{ textAlign: "left" }}>
        Payment confirmed by the Bitcoin network and merchant order is "ready to be shipped".
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        invalid
      </td>

      <td style={{ textAlign: "left" }}>
        Payment rejected by the Bitcoin network.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        expired
      </td>

      <td style={{ textAlign: "left" }}>
        Buyer did not pay within 20 minutes and the invoice expired.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        canceled
      </td>

      <td style={{ textAlign: "left" }}>
        Buyer canceled the invoice.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        refunded
      </td>

      <td style={{ textAlign: "left" }}>
        Payment refunded to buyer or merchant.
      </td>
    </tr>
  </tbody>
</Table>

**Statuses by priority:**

1. pending
2. confirming
3. paid OR invalid OR expired OR canceled
4. refunded

## Statuses and Merchant App Behavior

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Status
      </th>

      <th>
        Behavior
      </th>

      <th>
        Sends Callback
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        pending
      </td>

      <td>
        Mark order status as *unpaid* in database.\
        Display "Unpaid" order status for buyer.
      </td>

      <td>
        No
      </td>
    </tr>

    <tr>
      <td>
        confirming
      </td>

      <td>
        Mark order status as *pending* or *confirming* or *processing* in database.\
        Display "Waiting payment from CoinGate" status for buyer.
      </td>

      <td>
        Yes\*
      </td>
    </tr>

    <tr>
      <td>
        paid
      </td>

      <td>
        Mark order as *paid* in database.\
        Display "Paid" order status for buyer.
      </td>

      <td>
        Yes
      </td>
    </tr>

    <tr>
      <td>
        invalid
      </td>

      <td>
        Mark order as *invalid* or *rejected* in database.\
        Display "Invalid" or "Rejected" order status for buyer.
      </td>

      <td>
        Yes
      </td>
    </tr>

    <tr>
      <td>
        expired
      </td>

      <td>
        Mark order as *expired* or *unpaid* in database.\
        Display "Expired" or "Unpaid" order status for buyer.
      </td>

      <td>
        Yes
      </td>
    </tr>

    <tr>
      <td>
        canceled
      </td>

      <td>
        Mark order as *canceled* or *unpaid* in database.\
        Display "Canceled" or "Unpaid" order status for buyer.
      </td>

      <td>
        Yes
      </td>
    </tr>

    <tr>
      <td>
        refunded
      </td>

      <td>
        Mark order as *refunded* in database.\
        Display "Refunded" or "Unpaid" order status for buyer.
      </td>

      <td>
        Yes
      </td>
    </tr>
  </tbody>
</Table>

\*The "confirming" status is sometimes skipped and "paid" or "invalid" status is sent instead.
