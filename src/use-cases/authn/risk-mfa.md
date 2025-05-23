---
layout: layouts/facile.njk
title: AuthN - Risk
eleventyNavigation:
  key: Risk \ MFA
  parent: Authentication
  order: 2
---

Experience showing the Device Profiling step and branching based on the PingOne Risk result

* [Simple](../simple) --> PingOne Risk --> \[LOW\] --> Decoder
* [Simple](../simple) --> PingOne Risk --> \[MEDIUM\] --> PingOne MFA --> Decoder
* [Simple](../simple) --> PingOne Risk --> \[HIGH\]

#### Multi-Factor

With PingOne MFA 1.4.1 IK, JIT enrollment has been removed (a bogus email attribute is defined in the Adapter).
Authenticated Users will be prompted to enroll thier first (and additional) devices, including FIDO2.

**Note:** FIDO2 options depend on browser support - Chrome may be the one to demo with.

#### PingOne Risk Demos

As part of a deployment, I add an Override of the Deployment browser IP. This _should_ make the initial flow
generate a **MEDIUM** result and invoke an MFA Enrollment \ Authentication event.

To show the Risk policy being in control of this flow follow this to alter the override:

* Open PingOne Console
* Open the Risk event (Dashboard --> Audit)
  * Show what data we collect and release with the service
  * Copy the IP Address that was recorded
* Open the Risk Policy
  * Talk through the sliders
  * Open the Overrides
    * Set the Override for Whitelist to **LOW**
* Run the Experience again
  * Let SSO happen for [Simple](../simple)
  * MFA should not be invoked
* [Optional] Repeat for **HIGH** 
  * Experience should be blocked