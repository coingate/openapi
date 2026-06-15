---
api:
  file: v2.json
  operationId: create-billing-request
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Creates a new billing request and returns a payment link that can be shared with a customer. Billing requests are typically used to send one-off crypto payment links to customers outside of a full shopping cart experience.

**Time-Based Behaviors**:

<Accordion title="Billing Request">
  The **pay button** on the billing link is disabled if:

  * The **due\_days** period has expired, **or**
  * The associated invoice is already paid.
</Accordion>

<Accordion title="Invoice">
  * Invoice is valid for 2 hours unless payment details are generated.

  * Once the customer reaches the payment details view, they have a fixed window of 20 minutes to complete the payment
</Accordion>