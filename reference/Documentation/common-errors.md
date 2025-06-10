---
title: Errors
excerpt: CoinGate API error responses
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: ''
---
Most common API error responses are described below. Error response must be identified by **HTTP status** and **reason** attribute in your application.

Please note that specific API methods (for example [Create Order](doc:create-order)) have their own errors (e.g. 422 Unprocessable Entity - when order is not valid).

See [Common Issues](doc:issues) for troubleshooting.

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        HTTP Status
      </th>

      <th>
        Reason
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        401 (Unauthorized)
      </td>

      <td>
        BadCredentials
      </td>

      <td>
        API credentials are not valid
      </td>
    </tr>

    <tr>
      <td>
        404 (Not Found)
      </td>

      <td>
        PageNotFound
      </td>

      <td>
        Page, action or record not found
      </td>
    </tr>

    <tr>
      <td>
        404 (Not Found)
      </td>

      <td>
        RecordNotFound
      </td>

      <td>
        Record not found
      </td>
    </tr>

    <tr>
      <td>
        500 (Internal Server Error)
      </td>

      <td>
        InternalServerError
      </td>

      <td>
        Something wrong in CoinGate
      </td>
    </tr>

    <tr>
      <td>
        429 (Too Many Requests)
      </td>

      <td>
        RateLimitException
      </td>

      <td>
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
