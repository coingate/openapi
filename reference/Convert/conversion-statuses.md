---
title: Conversion Statuses
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
| Status    | Description                                                             |
| :-------- | :---------------------------------------------------------------------- |
| pending   | A new conversion has been created and is awaiting confirmation.         |
| completed | Conversion was successful and has been completed.                       |
| expired   | Conversion not confirmed before the expiration timestamp (`expires_at`) |
| error     | The conversion could not be completed due to an error.                  |
| canceled  | The conversion was canceled by the user.                                |

## Status Changing Flow

![](https://files.readme.io/36fff9b670c733d58be5eaf24e8761005545332a735e619351c906938cf40b2a-image.png)
