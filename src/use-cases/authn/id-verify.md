---
layout: layouts/facile.njk
title: Authentication
eleventyNavigation:
  key: ID Verification
  parent: Authentication
  order: 4
---

Experience with PingOne Verify - Authentication or Registration

HTML Form (`verifyForm`) with LIP (`verifyIdentityProfile`) --> Decoder

**Notes:**
* Auto-deploy uses the Product team's Demo Environment
  * You see it in PF --> Server --> External Systems --> PingOne Connections
* Authentication flow only works once per user
* Registration uses Name data from the scanned ID
  * This is why it uses a different Form / LIP and Fragment