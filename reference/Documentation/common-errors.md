---
title: Errors
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

Most common API error responses described below. Error response must be identified by **HTTP status** and **reason** attribute in your application.\
Please note, that specific API methods, for example [Create Order](doc:create-order) has their own errors (422 Unprocessable Entity - when order is not valid).

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th style={{ textAlign: "left" }}>
        HTTP Status
      </th>

      <th style={{ textAlign: "left" }}>
        Reason
      </th>

      <th style={{ textAlign: "left" }}>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style={{ textAlign: "left" }}>
        401 (Unauthorized)
      </td>

      <td style={{ textAlign: "left" }}>
        BadCredentials
      </td>

      <td style={{ textAlign: "left" }}>
        API credentials is not valid
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        404 (Not Found)
      </td>

      <td style={{ textAlign: "left" }}>
        PageNotFound
      </td>

      <td style={{ textAlign: "left" }}>
        Page, action or record not found
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        404 (Not Found)
      </td>

      <td style={{ textAlign: "left" }}>
        RecordNotFound
      </td>

      <td style={{ textAlign: "left" }}>
        Record not found
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        500 (Internal Server Error)
      </td>

      <td style={{ textAlign: "left" }}>
        InternalServerError
      </td>

      <td style={{ textAlign: "left" }}>
        Something wrong in CoinGate
      </td>
    </tr>

    <tr>
      <td style={{ textAlign: "left" }}>
        429 (Too Many Requests)
      </td>

      <td style={{ textAlign: "left" }}>
        RateLimitException
      </td>

      <td style={{ textAlign: "left" }}>
        API request limit is exceeded
      </td>
    </tr>
  </tbody>
</Table>

Response example:

```json
{
  "message": "Not found App by Access-Key",
  "reason": "BadCredentials"
}
```
