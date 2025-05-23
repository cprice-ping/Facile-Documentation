---
layout: layouts/facile.njk
title: Consent Management App
eleventyNavigation:
  key: Consent Management
  parent: Access
  order: 3
---

Application URL: `https://{releaseName}.ping-devops.com/consent-mgmt`

A single page application that shows PingAccess converting OIDC into a virtual resource that can be consumed via the SPA. 

PingAccess is using a custom scope in the WebSession request to enable the `access_token` to be used for Consent API calls for the logged on User.
PA has a Groovy rule that injects the `access_token` into calls made through it to the Consent API - allowing for _unpriviledged_ calls to the API as the use who owns the records.

The SPA doesn't have to know any secrets or how to process OIDC.

This SPA is a demo of using the Consent API to manage 2 Consent records:
* Terms and Conditions (Course-grained) -- the SPA will check for one on load, and display \ record if not there
* Marketing Preferences (Fine-Grained) -- As the T&C record is created, so is another one for Marketing Preferences

To see the contents of the record(s), click on the one in the left box. 

To modify the contents of the `data` element of the Marketing record, use the sliders on the right - these will be reflected in the [Consent Enforcement SPA](../consent-enforce).

SPA code: [https://glitch.com/edit/#!/facile-apps?path=public/consent-mgmt](https://glitch.com/edit/#!/facile-apps?path=public/consent-mgmt)
