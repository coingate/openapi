---
title: Contact Callback
deprecated: false
hidden: false
metadata:
  robots: index
---
CoinGate POSTs a contact callback to your server every time a Payment-Channel contact's status changes. Use it to mirror the contact's verification state in your own system, surface KYC progress to your end user, and react to a suspended / rejected contact (e.g. block the customer from opening a new channel until they re-submit documents).

> 📘 API Callback Documentation
>
> The callback is delivered as a `POST` request with a `application/json` body. For shared callback behavior — retry policy, IP allowlist, manual resend — see the <Anchor label="API Callbacks " target="_blank" href="https://developer.coingate.com/reference/api-callbacks">API Callbacks </Anchor>reference.

**When the callback fires**

| Event                       | Meaning                                                                                                                                                    |
| :-------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------- |
| contact.status.under_review | Compliance has picked up the contact and is reviewing the documents / KYC data. The channel stays active.                                                  |
| contact.status.verified     | KYC passed. Documents are approved and the channel stays active. Terminal "happy path" state.                                                              |
| contact.status.suspended    | All incoming payments on this contact's channel are placed on hold pending compliance review. Funds are not credited until compliance reviews the contact. |
| contact.status.rejected     | KYC failed or the contact triggered a compliance rule. The channel is set to disabled and any incoming payments are marked invalid.                        |

<br />
