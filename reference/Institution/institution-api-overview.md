---
title: Institution API Overview
excerpt: 'Authentication and request signing for the Institution API.'
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
The Institution API is a segregated surface for partner financial institutions and PSPs.
Every request must be authenticated with an API key and an HMAC-SHA256 request signature.

## Authentication

Send these headers with **every** request:

| Header            | Description                                                                 |
| :---------------- | :-------------------------------------------------------------------------- |
| `X-CG-Api-Key`    | Your Institution API key.                                                   |
| `X-CG-Nonce`      | Epoch milliseconds. Must be within ±5 minutes of CoinGate server time.      |
| `X-CG-Signature`  | HMAC-SHA256 signature of the request, prefixed with `v1=`.                  |

### Building the signature

Concatenate the following values **in order**, with no separators, then sign with your API
secret using HMAC-SHA256 and hex-encode the result:

```
message   = nonce + method + host + path + body
signature = "v1=" + HMAC_SHA256_hex(api_secret, message)
```

- `nonce` — the exact value sent in `X-CG-Nonce` (epoch milliseconds).
- `method` — the HTTP method in uppercase (`GET`, `POST`, `PUT`).
- `host` — the request hostname (e.g. `api.coingate.com`).
- `path` — the full request path, including any query string.
- `body` — the raw request body. Use an empty string for requests without a body.

The same nonce/signature pair cannot be reused within the validity window — exact replays
are rejected.

### Authentication errors

| Status | Body                                                                  | When                                                              |
| :----- | :-------------------------------------------------------------------- | :---------------------------------------------------------------- |
| `401`  | `{ "message": "Invalid API credentials", "reason": "InvalidApiCredentials" }` | Unknown/inactive key, IP not allowlisted, bad nonce, bad signature, or replay. |
| `503`  | —                                                                     | The Institution API is not enabled for your institution.          |

Verify your credentials with the [Test Connection](/reference/test-institution-connection) endpoint.
