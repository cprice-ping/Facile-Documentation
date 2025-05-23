---
layout: layouts/facile.njk
title: Neo
eleventyNavigation:
  key: Neo
  parent: Use Cases
---
Demonstrating next generation Identity - Verification and Wallet-based Credentials.

Integration is done using [PingFederate](./credentials) \ PingOne Neo \ PingID \ [PingOne Davinci](./davinciflow)

## PingFederate

The demo is deliberately PingFed-centric - due to the Wallet being used is the PingID App. The majority of our PingID Customers
are using PingFed as their IDP. Below are the pieces added to implement a plausible Credential demo using PingFed Policies.

#### IDP Adapters

| IDP Adapter Name | Adapter Type | Description |
| --- | --- | --- |
| Cred - Internal Access | PingOne Credentials | Used to handle `InternalAccess` Credentials |
| Cred - VerifiedEmployee | PingOne Credentials | Used to handle `VerifiedEmployee` Credentials |
| Cred - VerifiedExternal | PingOne Credentials | Used to handle `VerifiedExternal` Credentials |
| | | **Note:** This separation is needed to handle the attribute mappings of each CredentialType |
| DV (VerifiedEmployee) - GovID (Biographic) | PingOne Davinci | Maps ChainedAttributes from `Cred - VerifiedEmployee` into the DV Widget call |
| DV (VerifiedExternal) - GovID (Biographic) | PingOne Davinci | Maps ChainedAttributes from `Cred - VerifiedExternal` into the DV Widget call<br>This is a child of `DV (VerifiedEmployee) - GovID (Biographic)` |
| PingOne Verify (Selfie from Credential) | PingOne Verify | Maps `referenceSelfie` ChainedAttribute from  `Cred - InternalAccess` into a Verify transaction |


#### Fragments

| Fragment Name | Components | Description |
| --- | --- | --- |
| Cred_InternalAccess | Cred - InternalAccess | Handles a InternalAccess Credential verification |
| Cred_VerifiedEmployee | Cred - VerifiedEmployee | Handles a VerifiedEmployee Credential verification |
| Cred_VerifiedExternal | Cred - VerifiedExternal | Handles a VerifiedExternal Credential verification |
| Issue_InternalAccess_Employee | Cred - VerifiedEmployee<br>DV (VerifiedEmployee) - GovID (Biographic) | VerifiedEmployee --> P1 Verify --> InternalAccess |
| Issue_InternalAccess_External | Cred - VerifiedExternal<br>DV (VerifiedExternal) - GovID (Biographic) | VerifiedExternal --> P1 Verify --> InternalAccess |
| Verified_Credential | Cred - InternalAccess<br>PingOne Protect<br>PingOne Verify (Selfie from Credential) | Used to show `InternalAccess` as an AuthN source<br>If Protect != `LOW` do a Verify Selfie (`referenceSelfie` is on the `InternalAccess` credential) |

#### Selectors

Because I'm a little lazy - I trigger these calls from Dashboard using the `PingLogon` OIDC client, using `acr_values` to select them.
You'll see in the PF Policies that the fragments are added to the `Sample AuthN Context` Policy **only**

| `acr_value` | Description |
| --- | --- |
| Issue_InternalAccess_Employee | `Cred - VerifiedEmployee` Presentation Request --> `InternalAccess` Issuance |
| Issue_InternalAccess_External | `Cred - VerifiedExternal` Presentation Request --> `InternalAccess` Issuance |
| Verified_Credential | `Cred - InternalAccess` used to authenticate and get an OIDC Code \ Token

## PingOne

Neo capabilities exist as PingOne Services. Facile already deploys a CIAM-focused Environment (that contains PingOne Verify). 
However, The publically accessible Wallet exists in the PingID App - and you need to add PingID to an Environment to be able
to use it.

Since you can't add PingID to an Existing Env (and it would break the PingOne MFA integration with Facile) - I deploy a second
Environment - `{releaseName}` - Neo to host the Credentials and PingID integration

#### Services

| Name | Description |
| --- | --- |
| PingOne SSO | Needed to create Users for Creds to be issued to |
| PingID | Adds the PID Mobile App that incudes the `digitalWalletAppId` for Neo |
| PingOne Verify | Default Policy to handle GovID + Selfie during `InternalAccess` issuance |
| PingOne Creds | `VerifiedEmployee` (AUTOMATED - Issuance Rule)<br>`VerifiedExternal` (AUTOMATED - Issuance Rule)<br>`InternalAccess` (MANAGED - Davinci) |
| PingOne Davinci | A [Flow](./davinciflow) that handles the Issuance experience for `Verified*` --> `InternalAccess` Credentials |
