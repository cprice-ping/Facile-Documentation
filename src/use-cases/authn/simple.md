---
layout: layouts/facile.njk
title: AuthN - Simple
eleventyNavigation:
  key: Simple
  parent: Authentication
  order: 1
---

OOTB PingFed HTML Form with LIP and Social.

* [Simple](.) --> Decoder

Adapter Features:
* OOTB config
* Self-Service Password Reset \ Recovery
  * Uses *Forgot Password* AuthN Policy --> PingOne MFA
* Local Identity Profile (`registrationIdentityProfile`)

#### Social Connections

The LIP includes Facebook and Google, but the adapters are not configured. 

**Facebook**

[Dev Console](https://developer.facebook.com)

* Create a new App
  * Copy the `App ID` & `App Secret` -- these go into the PingFed IK Adapter
* Add `Facebook Login`
* **Valid OAuth Redirect URIs** -- `https://{releaseName}.ping-devops.com/ext/facebook-authn`


**Google**

[Dev Console](https://console.cloud.google.com/home/dashboard)

#### reCaptcha

reChapcha can be enabled if you configure the `System` provider first.

1. Signup for reCaptcha \([https://www.google.com/recaptcha/admin](https://www.google.com/recaptcha/admin)\)
2. Create `v2 Invisible` site
  * Enter your Facile deployment domain
3. Copy the `site key` and `secret key` into PingFed (Server --> External Systems --> Captcha Settings)
