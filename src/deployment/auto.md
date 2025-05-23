---
layout: layouts/facile.njk
title: Automatic Deployment
eleventyNavigation:
  key: Automatic
  parent: Deployment
  order: 2
---

Automatic deployment does a complete Fullstack implementation of the CIAM configuration with no prior understanding of DevOps.

![Auto Deployment Screen](https://cdn.glitch.com/6f32d434-43ae-4e29-b7fe-c327613b6a03%2FFacile%20-%20Auto.png?v=1627398290120)

### Deployment Flow:

* PingOne details entered
* PingOne Admin Environment initialized
* Admin SSO Applications created for PF \ PA \ PAZ
* PingOne Release Environment created
  * Roles added to Admin User
  * `values.yaml` file created
  * `values.yaml` committed to GitHub repo
* GitHub Action triggered to perform `helm install` of Facile chart