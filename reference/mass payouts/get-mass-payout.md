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
An endpoint to retrieve **_Mass Payout's_** information. In case of status  **_draft_** (which is set by [creating Mass Payout](ref:create-mass-payout)), the status is set to **_pending_**. This way we may confirm that you have retrieved our latest pricing proposal. 

In order to **_confirm_** the Mass Payout, use [confirm Mass Payout endpoint](ref:confirm-mass-payout).