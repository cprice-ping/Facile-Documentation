---
layout: layouts/facile.njk
title: PingOne Challenges
eleventyNavigation:
  key: Technical
  parent: PingOne
  order: 2
---

## Things we need (Tech)

We need to simplify the **client-first** integration between an application and Ping Products.
Without this, none of the capabilites of the platform can be realized
  
* Ping-branded SDK \ library to perform OIDC with Ping Products
  * Features:
    * OIDC AuthZ Code flow with PCKE
      * [Optional] Implicit flow handling
      * [Optional] `pi.flow` integration - Code flow should be fully handled by SDK
        * Today, you get the Code and have write everything else
    * Token handling -- `access_token` \ `id_token`
    * UserInfo
    * Token \ Session revocation
  * Make this for **both** PingOne and PingFed
    * *Minimally* replace `environmentId` with AS URL
    * Use `Issuer` and `.well-known` to simplify?
* Ping-branded SDK \ library to perform Flow API with Ping Products
  * Flow `status` isn't consistent between PingFed and PingOne
  * BXRetail has done this work for P1 - maybe useful to review
* Flow API is limited - only basic flows are exposed through it
  * Email only registration \ No MFA enrollment \ Progressive registration without password \ etc
  * Management APIs have to be invoked to perform more interesting transactions
  * How does a SPA handle this context switch? 
    * Mgmt APIs need `client_secret` to get tokens
  * Does Flow Manager resolve this?
    * Still need to resolve the **client-first** problem before getting to this
* Fix CORS in PingOne
  * Difficult to make calls between domains
  * Custom Domains don't appear to work properly
  * Allow list for approved domains to make calls into the Env
* PingOne Authentication Widget
  * Similar to PF Widget
  * Allows broader branding of the experience without full custom UX
  * Handles the shifting Flow without code in the app
  * Updated along with new P1 Products - MFA \ Verify \ Risk \ FM
* Ping-branded SDK (Web) for handling MFA calls
  * Our insistence on starting with a Mobile App (MFA \ Verify) is misguided
    * Barrier to entry is very high
* Guidance on how to use these:
  * Triggered authentication (On App load \ On button click \ etc)
  * Is the User still authenticated?
  * Session \ Token revocation
  * Accessing the User data -- UserInfo \ `id_token` \ `access_token` if calling APIs
  * Requesting new `access_tokens` in the User Context for scoped APIs


Could this even be a **PingOne Service**? (Note: We should really do both)
  * Take the things that PingAccess does for SPAs and deliver in P1
    * Endpoint for UserDetails (`/user`)
    * Return 401 if not Authenticated
      * Send an OIDC PCKE URL pointing to the AuthN Orchestration (PF \ PF \ FM \ anything)
      * `redirect_uri` is PingOne endpoint
      * Perform initial token swap **and** retrieve new tokens from P1 as they expire
      * Create P1 session for the User
    * Convert OIDC claims into the `/user` response
    * Allow request for a token (`/token`) to be made from the App
    * Handle logoff -- token revocation & session teardown
  * We should perform the standards via "best practices" on behalf of the developer
    * Make it simple to start that process
    * Make it simple to consume the results
    * The Dev doesn't need to know about AuthN \ OIDC -- just know that we've done all that well