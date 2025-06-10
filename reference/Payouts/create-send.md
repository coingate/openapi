---
title: Create Send Request
excerpt: ''
api:
  file: v2.json
  operationId: create-send
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
**Send Request Behavior with 2FA**

**With 2FA Enabled**

Records are initially created in a draft state and require manual confirmation through the dashboard before processing can begin. Only after confirmation will requests be processed.

‘Send Request’ should be confirmed in the account dashboard under Payouts → Outgoing Payments

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/3cedf4c9ab4f232847a3189ad3a06a7950e36fc4ec5184680a5ce9e1836c05ed-image.png",
        null,
        ""
      ],
      "align": "center",
      "border": true
    }
  ]
}
[/block]


**With 2FA Disabled**

Requests are processed immediately upon creation, without requiring manual confirmation. You can enable or disable the 2FA setting at any time in the API section of the dashboard.

**2FA Configuration**

You can enable or disable the 2FA requirement for each ‘send request’ in API App → Select API App → 2FA Settings

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/9c7cdfde51778781c16e12a9d24b075e4b035378ba4cf95ceac5ccb1b562aae2-image.png",
        null,
        ""
      ],
      "align": "center",
      "border": true
    }
  ]
}
[/block]


**API Response of Send Request**

> 📘 Send Request Object
> 
> The Send Request response has the same structure as the Send Request Callback. For detailed descriptions of each field, please refer to the ‘[Send Request Callback](https://developer.coingate.com/reference/send-request-callback)’ documentation page.