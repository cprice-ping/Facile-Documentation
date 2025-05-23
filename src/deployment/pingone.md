---
layout: layouts/facile.njk
title: PingOne Configuration
eleventyNavigation:
  key: PingOne Config
  parent: Deployment
  order: 1
---

Facile is designed to be integrated with PingOne. A new Environment will be created that contains all the Software and Services deployed for that release.

## PingOne pre-requisites

1. Sign up for PingOne
2. Login as your Administrator account
3. Create a Worker App in the Administrators environment
* Connections --> Applications --> Worker App
* Name: `Facile - Worker` --> take remaining defaults
* Retrieve the `client_id` and `client_secret` from the Worker app
4. Get the Admin User URL
* Identities --> Admin User --> Admin API tab