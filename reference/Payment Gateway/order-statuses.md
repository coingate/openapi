---
title: Order Status
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
  pages:
    - type: link
      title: What’s a merchant refund feature & how to use it?
      url: https://coingate.com/blog/post/merchant-refund
    - type: link
      title: ' My customer overpaid for his order. How do I issue refunds? '
      url: https://support.coingate.com/hc/en-us/articles/4402499190418
    - type: link
      title: ' Is it possible to complete an order after it has been canceled or expired? '
      url: https://support.coingate.com/hc/en-us/articles/10420045425948
---
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
        new
      </td>

      <td style={{ textAlign: "left" }}>
        Newly created invoice. The shopper has not yet selected a [payment currency](https://developer.coingate.com/reference/currencies) or [crypto platform](https://developer.coingate.com/reference/platforms). If the shopper does not make a selection, the order status will eventually change to Expired 2 hours after the order creation time.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        pending
      </td>

      <td style={{ textAlign: "left" }}>
        The shopper has selected a payment currency and crypto platform. Awaiting payment. If the shopper does not complete the payment within 20 minutes, the order status will change to Expired.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        confirming
      </td>

      <td style={{ textAlign: "left" }}>
        Shopper transferred the payment for the invoice. Awaiting blockchain network confirmation.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        paid
      </td>

      <td style={{ textAlign: "left" }}>
        Payment is confirmed by the network, and has been credited to the merchant. Purchased goods/services can be safely delivered to the shopper.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        invalid
      </td>

      <td style={{ textAlign: "left" }}>
        The payment was either not confirmed by the blockchain network or was marked as invalid due to AML/CTF compliance reasons.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        expired
      </td>

      <td style={{ textAlign: "left" }}>
        An order will expire in the following cases:  

        * For a new order: the shopper does not select a payment currency and crypto platform within 2 hours.
        * For a pending order: the shopper does not complete the payment within 20 minutes.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        canceled
      </td>

      <td style={{ textAlign: "left" }}>
        Shopper canceled the invoice.
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        refunded
      </td>

      <td style={{ textAlign: "left" }}>
        Payment was refunded to the shopper. [Read more about refunds](https://coingate.com/blog/post/merchant-refund)
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        partially\_refunded
      </td>

      <td style={{ textAlign: "left" }}>
        Payment was partially refunded to the shopper. [Read more about refunds](https://coingate.com/blog/post/merchant-refund)
      </td>
    </tr>
  </tbody>
</Table>

## Order Status Changing Flow

<Image align="center" src="https://files.readme.io/28732a5-Order_Status_Changing_Flow4.png" />
