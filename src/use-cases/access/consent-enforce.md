---
layout: layouts/facile.njk
title: Consent Enforcement App
eleventyNavigation:
  key: Consent Enforcement
  parent: Access
  order: 4
---

Application URL: `https://{releaseName}.ping-devops.com/consent-enforce`

A single page application that shows PingAuthorize enforcing the contents of the Consent record managed in the [Consent Mangement SPA](../consent-mgmt).

PingAuthorize is responding to a request to display all Users, and returning **only** those that have the following:

* A `Facile-MarketingPrefs` consent record that is `approved`
* Display the contents of `mail`, `phoneNumber`, `postalAddress` - depending on the fine-grained data in the record

PingAccess integration is used to handle OIDC Authentication using the PF AuthN Widget, and no token processing is being done by the SPA. When the SPA needs a token for an API call,
it calls the PA App virtual resource on `/token` to receive the current WebSession token.

In addition, the `PingAuthorize Filter Response` rule is applied to the PD Directory API call to get the User information. This API is invoked anytime the `Refresh` button is pressed.

SPA code: [https://glitch.com/edit/#!/facile-apps?path=public/consent-enforce](https://glitch.com/edit/#!/facile-apps?path=public/consent-enforce)
