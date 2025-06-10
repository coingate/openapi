---
title: Conversion Rates
excerpt: List Supported Conversion Rates
api:
  file: v2.json
  operationId: conversion-rates
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Retrieve a list of all supported currency conversion rates available on CoinGate. This includes the available base currencies, quote currencies, and their respective rates, which can be used both via the CoinGate dashboard and the API.

You can use this endpoint in three ways:

1. List all supported conversion pairs and rates:  
   `GET /api/v2/ledger/conversions/rates`
2. List supported conversion pairs and rates for a specific base currency:  
   `GET /api/v2/ledger/conversions/rates/{base_currency}`  
   _Example_: `/api/v2/ledger/conversions/rates/BTC` → returns all quote currencies and rates available for BTC.
3. Get the direct conversion rate between a specific base and quote currency:  
   `GET /api/v2/ledger/conversions/rates/{base_currency}/{quote_currency}`  
   _Example_: `/api/v2/ledger/conversions/rates/BTC/EUR` → returns the current conversion rate from BTC to EUR.