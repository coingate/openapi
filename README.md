# CoinGate API Documentation

This repository contains the source for the [CoinGate API documentation](https://developer.coingate.com) — the OpenAPI specification and the Markdown pages that make up the API reference.

## Repository layout

| Path                | Contents                                                                          |
| ------------------- | --------------------------------------------------------------------------------- |
| `reference/v2.json` | OpenAPI 3.1 specification for CoinGate API v2                                      |
| `reference/`        | API reference pages (Markdown with YAML frontmatter), one folder per category      |
| `custom_pages/`     | Standalone pages that don't belong to the reference                                |

Sidebar ordering within each category is controlled by the `_order.yaml` file in that directory.

## Branches

The `v2` branch (default) is the source of the published documentation for CoinGate API v2. Other branches (`v2_*`) are staging branches for changes under review.

## Using the OpenAPI specification

[`reference/v2.json`](reference/v2.json) is a standard OpenAPI 3.1 document describing the live API at `https://api.coingate.com/api/v2`. You can use it to generate API clients, import the API into tools like Postman or Insomnia, or build mocks against it.

Note that request/response schemas are kept inline (rather than under `#/components/schemas`) because that is what the documentation renderer requires.

## Feedback

Spotted a mistake or a gap in the documentation? Please [open an issue](https://github.com/coingate/openapi/issues). For questions about the API itself, contact [support@coingate.com](mailto:support@coingate.com).
