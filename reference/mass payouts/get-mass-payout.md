---
title: Get Mass Payout
excerpt: Get single mass payout by its ID
api:
  file: v2.json
  operationId: get-mass-payout
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
An endpoint to retrieve ***Mass Payout's*** information. In case of status  ***draft*** (which is set by [creating Mass Payout](ref:create-mass-payout)), the status is set to ***pending***. This way we may confirm that you have retrieved our latest pricing proposal. 

In order to ***confirm*** the Mass Payout, use [confirm Mass Payout endpoint](ref:confirm-mass-payout).
