---
layout: layouts/facile.njk
title: Davinci Flow
eleventyNavigation:
  key: Davinci Flow
  parent: Neo
  order: 2
---
# Davinci Flow

Davinci is being used to overcome a couple of limitations of the Credential Adapter in PingFederate:
* Credential Issuance is not supported - only Presentation
* Verify IK does not support Biographic Name matching

To perform these functions, the PF Davinci IK is used to pass information from the Neo IKs into a Flow.

## Davinci Flow

<img src="https://cdn.glitch.global/6f32d434-43ae-4e29-b7fe-c327613b6a03/DaVinciFlow-67.png?v=1739984087235" alt="Davinci Flow" width="100%" height="auto">

### Notes

1. The Input Schema is populated from the Credential used to begin the transaction
    * User must be created in the Neo Env and `VerifiedEmployee` \ `VerifiedExternal` credential issued
1. The Verify `CreateTransaction` node uses the Input `givenName` and `surname` values
    * There's a Custom JS Function used to extract the `BABEL_STREET` object from the Metadata, that is checked to see that it's not `NONE` or `LOW`
      * **Note:** This is why it's important to use your Legal name on the Credential (unless you want to demo the failed verification)
1. There are a couple of calls in the Flow that are not currently available in the DV Connectors - these need a Worker token
    * I reuse the `PingOne Davinci Connector` Worker App (easier than adding one)
    * This is a `CLIENT_SECRET_BASIC` App - I use the `String` connector to construct the `Authorization: Basic` header
      * There's a FR to allow Variable Secrets to be used in this Action - this is why it's a String    
1. The 2 calls that use this Worker:
    * `P1 Branding` - I do the Branding in the Verify QR display from PingOne Branding - change the Logo there
      * The branding carries over into the Verify WebApp, but not PID App
    * `Issue Credential` - The DV Connector doesn't support `MANAGED` or the `credData` object that is injected into the call  
1. The `InternalAccess` Credential has a flag - `isInternal` that is dependant on the Credential you used to get it:
    * `VerifiedEmployee` sets `isInternal: true`
    * `VerifiedExternal` sets `isInternal: false`
1. This attribute is exposed in PingFed in the `Cred - InternalAccess` IK and can be used to add additional Rules in Policy 
    * Look at the `Verified_Credential` Fragment - there's already a rule for `riskLevel != LOW`