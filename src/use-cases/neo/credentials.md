---
layout: layouts/facile.njk
title: Credentials
eleventyNavigation:
  key: Credential Demo Setup
  parent: Neo
---
## Setup
This demo requires Davinci to handle the Biographic GovID check (PingOne Verify) and the issuance of
the InternalAccess credential. 

Your Digital Wallet should be the PingID App (v3.0.0+).

**Note:** If you're doing a demo - you can only show the iOS PID App on-screen

Manual configuration of Davinci and the Davinci IK in PingFed is required.

### Davinci
1. Open the **`{releaseName}` - Neo** PingOne Environment
1. From that Env, Open the DV Console
1. Import the <a href="/public/FacileIssueInternalAccessCred.json" download>Facile - Issue InternalAccess Cred</a> Flow
1. Add the DV Worker details to the P1 Verify Connector (you'll be asked for it on Import)
1. Add the DV Worker details to Company Variables (`type` = "string") - `workerId` and `workerSecret`
    * **Note:** `type`="secret" doesn't work when base64 is needed for the CLIENT_SECRET_BASIC call - I've complained
1. Add the CredentialType ID to Company Variables (`type` = "string"):
    * PingOne --> Digital Credentials --> Management --> InternalAccess
1. Create a new Flow Policy: 
    * Applications --> PingOne SSO Connection

### PingFederate
1. Open the **`{releaseName}`** PingOne Environment
1. SSO into PingFederate
1. Open the `DV (Neo) - GovID (Biographic)` IDP Adapter:
    * Authentication --> IdP Adapters
1. Paste the PolicyID and APIKey into their respective fields
1. Replicate changes:
    * System --> Cluster Management

## Operating the Demo
The demo can be used to show all parts of Neo being used together.

### VerifiedEmployee

VerifiedEmployee is a spec-defined profile to be used as Proof-of-Employment (think of it like a Business card).
As a spec, this is also supported by EntraID - Neo can accept EntraID VerifiedEmployee credentials (**Note:** 
This demo won't work with them...)

The Presentation request doesn't request specific credenials - the Wallet will interpret that all All-Required

#### Credential Contents

| Claim | Source | Description |
| --- | --- | --- |
| givenName | P1 User -> Name - Given | Given Name |
| surname | P1 User -> Name - Family | Family Name |
| displayName | P1 User -> Name - Formatted | Full Name |
| email | P1 User - Email | Email Address |
| jobTitle | P1 User - Title | Job Title |


#### Issuing a Cred

1. Issuing a VerifedEmployee Credential:
    * Your `{releaseName}` - Neo Environment is pre-configured with a Credential set to AUTOMATIC for any 
 User in the Default Population (Issuance Rules)
    * Add a New User to the Env - Put your **legal** Name details and an email you can get to on your phone
      * If you fill the other fields, they'll also show up on the Cred
    * You should get a Wallet Pairing email - click the link and it'll open PingID and pair it
    * The VerifiedCredential should appear in the Creds section
1. Verify the credential in PingFederate
    * On Dashboard - Select the "Wallet based - Authenticate with InternalAccess" link
    * **Note:** This should fail in your Wallet - PF has been told to look for an InternalAccess cred

### VerifiedExternal

VerifiedExternal is a custom credential - the intent is to represent a Contractor \ 3rd Party that may need 
access to internal resources.

The Presentation request is for `mail`, `givenName`, `surname` - the Wallet should show this *Selective Disclosure*
You can add the non-required claims, but they're not used anywhere.

#### Credential Contents

| Claim | Source | Description |
| --- | --- | --- |
| givenName | P1 User -> Name - Given | Given Name |
| surname | P1 User -> Name - Family | Family Name |
| displayName | P1 User -> Name - Formatted | Full Name |
| email | P1 User - Email | Email Address |
| type | P1 User - Type | Type of External User |
| popId | P1 User - Population ID | Population ID |
| Contractor ID | P1 User - Account ID | Something to identify this at the 3rd Party | 

1. Issuing a VerifedExternal Credential:
    * Your `{releaseName}` - Neo Environment is pre-configured with a Credential set to AUTOMATIC for any 
 User in the "External" Population (Issuance Rules)
    * Add a New User to the Env - Put your **legal** Name details and an email you can get to on your phone
      * If you fill the other fields, they'll also show up on the Cred
    * You should get a Wallet Pairing email - click the link and it'll open PingID and pair it
    * The VerifiedCredential should appear in the Creds section
1. Verify the credential in PingFederate
    * On Dashboard - Select the "Wallet based - Authenticate with InternalAccess" link
    * **Note:** This should fail in your Wallet - PF has been told to look for an InternalAccess cred
 
### InternalAccess

This is a custom credential meant to show that we've converted a simple cred into a much higher assurance one
(through the P1 Verify process) that can be used to access Internal resources.

#### Credential Contents

| Claim | Source | Description |
| --- | --- | --- |
| userId | P1 User -> ID | P1 UserID (from the Neo Env) |
| verifiers | P1 Verify -> verifiers | [Ephemeral] The list of things that Verify verified |
| referenceSelfie | P1 Verify -> Selfie | [Ephemeral] The selfie captured during ID verification |


Use the VerifiedEmployee or VerifiedExternal Cred to get an InternalAccess credential
1. On Dashboard - Select the "Wallet based - Issue InternalAccess" link
1. Use your Wallet to present your VerifiedEmployee or VerifiedExternal Cred
1. You'll go through a P1 Verify GovID (Biographic) transaction
  * **Note:** This is why you need to make sure your Name is correct on the initial credential

If successful, you'll get a new EmployeeAccess Cred in your Wallet

### Authenticate InternalAccess
Use the InternalAccess Cred to authenticate
1. On Dashboard - Select the "Wallet based - Authenticate with InternalAccess" link
1. Use your Wallet to present your InternalAccess Cred
1. You should see Protect profiling the Device
1. [`riskLevel !== LOW`] - P1 Verify does a Selfie Verification - selfie comes from InternalAccess cred
    * **Note:** You may need to alter the Default Risk Policy to trigger a non-LOW response
1. On Success - you'll get an OIDC AuthZ Code that you can swap for tokens

### Switch between Employee and External
1. You can switch a User between Populations to show the different entry Credentials.
    * You should see the other `Verified` credential get revoked
1. **However** - if you've already received an `InternalAccess` Credential - this will need to be manually revoked
    * Remember that the `isInternal` flag is ephemeral and calculated on Issue -- you need to re-enroll to get a new
  Credential with the flag properly set.
