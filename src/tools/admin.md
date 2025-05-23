---
layout: layouts/facile.njk
title: Admin Consoles
eleventyNavigation:
  key: Admin Consoles
  parent: Tools
  order: 1
---

Admin Consoles can be accessed via PingOne with the *Administration* button on the Dashboard. This will take you to the Release Environment Overview in PingOne.

Admin SSO will take you straight into PingFed and PingAccess.

PingData products (PD \ PDS \ PAZ) share a console that doesn't use SSO:

| Product | ServerName | Credential |
| --- | --- | --- |
| PingDirectory | `ldaps://{releaseName}-pingdirectory-cluster:1636` | administrator / 2FederateM0re |
| PingDataSync | `ldaps://{releaseName}-pingdatasync-cluster:1636` | administrator / 2FederateM0re |
| PingAuthorize | `ldaps://{releaseName}-pingauthorize-cluster:1636`| administrator / 2FederateM0re |
| PingAuthorize PAP | `https://pingauthorizepap-{releaseName}.ping-devops.com/` | admin / password123 |