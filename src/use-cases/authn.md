---
layout: layouts/facile.njk
title: Authentication
eleventyNavigation:
  key: Authentication
  parent: Use Cases
---

One of the primary functions of a CIAM platform is to authenticate users. Ping allows you to configure different experiences and assign them to your applications.

| Experience | App Protocol | Description |
| --- | --- | --- |
| Simple | SAML | First factor HTML Form with Self-Service & Social (not configured) |
| Risk MFA | OIDC | First Factor --> Risk \[Auto Deploy\] --> PingOne MFA |
| ID Verify | SAML| \[Auto Deploy\] First Factor \ Registration with PingOne Verify |
| Passwordless | SAML | Identifier-First --> PingOne MFA |
| Authentication API | OIDC | Redirected to PingFed [Authentication Widget](https://github.com/pingidentity/pf-authn-js-widget)
| Single Log Out | All | Front-channel deletion of authentication session | 