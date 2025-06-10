---
title: Send Request Statuses
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
| Status       | Description                                                                                                                                                                                               |
| :----------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| draft        | A new send request has been created and is awaiting 2FA confirmation in the dashboard.                                                                                                                    |
| in\_progress | Compliance checks have started, and the balance has been deducted from the account.                                                                                                                       |
| processing   | The send request is being processed by the network.                                                                                                                                                       |
| completed    | The send request was successful and has been completed.                                                                                                                                                   |
| expired      | The send requests where the exchange was not confirmed within 1 minute, or send requests requiring 2FA confirmation from the dashboard that were not confirmed within 30 days, will be marked as expired. |
| failed       | The send request was rejected by the network.                                                                                                                                                             |
| canceled     | The send request was canceled due to compliance reasons.                                                                                                                                                  |

## Status Changing Flow

![](https://files.readme.io/95063f03c11ed3af386d997adb3e09b9e9778fc7a971c14a9c48672a5f47be22-image.png)
