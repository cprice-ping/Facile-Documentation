---
layout: layouts/facile.njk
title: AuthN - Passwordless
eleventyNavigation:
  key: Passwordless
  parent: Authentication
  order: 3
---

Simple flow where Password is replaced by MFA

Identifier-First --> PingOne MFA

**Note:** This only works if the User is already enrolled into PingOne MFA (PF doesn't consider the User already authenticated). 

Use the [Risk-MFA](../risk-mfa) Experience first (remember to trigger the MEDIUM --> MFA step)