---
api:
  file: v2.json
  operationId: post_contacts-id-upload-documents
hidden: false
link:
  new_tab: false
metadata:
  robots: index
---
<br />

<Callout icon="🚧" theme="warn">
  This feature is currently under development and available only for selected partners during the early access phase. To join the whitelist and receive updates about Payment Channels availability, visit: <Anchor label="CoinGate Payment Channels" target="_blank" href="https://coingate.com/payment-channels">CoinGate Payment Channels</Anchor>
</Callout>

Upload a compliance document (passport, national ID, signed contract, etc.) to a payment channel contact. Used during the contact verification flow when CoinGate compliance requests supporting documents.

**Allowed document types**

| Contact type | Allowed document_type values                |
| :----------- | :------------------------------------------ |
| person       | passport, national_id, residence_permit     |
| business     | signed_contract, service_agreement, invoice |

Submitting a value outside this list returns `422 DocumentUploadFailed`.

**File constraints**

| Property                                     | Limit                         |
| :------------------------------------------- | :---------------------------- |
| Max file size                                | 10 MB                         |
| Allowed extensions                           | pdf, png, jpg, jpeg, zip, csv |
| Allowed extensions for document_type=invoice | pdf only                      |

<br />
