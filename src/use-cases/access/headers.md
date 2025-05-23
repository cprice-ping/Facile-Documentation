---
layout: layouts/facile.njk
title: Headers
eleventyNavigation:
  key: Headers
  parent: Access
  order: 1
---

Application URL: `https://{releaseName}.ping-devops.com/headers`

An application that shows PingAccess performing an OIDC authentication with PingFederate (OIDC Client: `PingLogon`) and converting the authenticated User
into Headers. 

The app is a simple table of **all** the Incoming Headers - the ones that PingAccess injected are prefixed with `ping-`

This application is hosted in the [Facile Decoder](https://decoder.pingidentity.cloud) (`/headers`).

There is also a demonstration of convering the User information into a JWT Header - use `https://{releaseName}.ping-devops.com/headersjwt`
