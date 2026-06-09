---
api:
  file: v2.json
  operationId: get_contacts-id
hidden: true
link:
  new_tab: false
metadata:
  robots: index
---
Retrieve a single contact by its ID. Returns the contact's type, identity/company details, external reference, and current status. Country inputs supplied on creation as ISO codes (address_country, incorporation_country) are returned here as their resolved numeric IDs (address_country_id, incorporation_country_id).
