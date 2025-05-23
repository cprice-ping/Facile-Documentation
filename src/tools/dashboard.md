---
layout: layouts/facile.njk
title: Dashboard
eleventyNavigation:
  key: Dashboard
  parent: Tools
  order: 2
---

The [Dashboard](https://facile.pingidentity.cloud/dashboard/{releaseName}) tool is used to present User-focused experiences \ applications that are wired into Facile.

URL is dynamic -- `https://facile.pingidentity.cloud/dashboard/{releaseName}`

`releaseName` is the release name you used in [Deployer](https://facile.pingidentity.cloud)

**Note:** Dashboard is maintained to the current release of Facile - older instances may not work as things are added to it

#### Bespoke Dashboards

Dashboards can be launched for Bespoke deployments - use the same URL format as above

**Differences**
* No PingOne Admin button
* No Delete button (`helm uninstall` and associated other cleanups for that)
* Experiences reflect **FullStack** (i.e. all check-boxes)