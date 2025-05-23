---
layout: layouts/facile.njk
title: Outbound SMTP
eleventyNavigation:
  key: Outbound SMTP
  parent: Tools
  order: 6
---

Facile has an Outbound SMTP service available - this can be used for LIP Email Verification and other PF / PD notifications

\[**Internal**\] SMTP credentials can be found pinned in the `#project-facile` Slack channel

#### PingFed
1. Add SMTP Notifier (Server --> External Systems --> Notification Publisher --> Add new SMTP Provider)

**Note:** 
* If using the Facile service,  `From Address` must be **@pingidentity.cloud** or **@ping-demos.com**
* The `SMTP Port` needs to match the actual call, even when using SMTPS