---
layout: layouts/facile.njk
title: Project Utile
eleventyNavigation:
  key: Directory Utility
  parent: Tools
  order: 5
---

Since you don't get access to the DataStore, a Directory Utility (Project Utile) was written to allow PD Directory API calls.

URL is tied to the `releaseName` --> `https://{releaseName}.ping-devops.com/utile/`

**Notes:**
* Utile is a SPA protect by PingAccess -- PA is doing OIDC tokens and injecting (via a Groovy script) into the PD REST API call
* Credentials are in the Dashboard