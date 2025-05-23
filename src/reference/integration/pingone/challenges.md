---
layout: layouts/facile.njk
title: PingOne Challenges
eleventyNavigation:
  key: Challenges
  parent: PingOne
  order: 1
---

## PingOne challenges 

PingOne doesn't accomplish the above - there's a number of problems with integrating with an application:

* Out-of-date Samples
  * Node libraries out of date - no Custom Domain support
    * Not updated in over a year
    * Source not readily available to edit
  * There's a React app repo
    * No README to give any guidance
* Lack of CORS support
  * Requires Custom Domain -- P1 cookies used to access Flow \ User APIs
  * Not all calls are accepted
* SPA integrations
  * Back-channel token \ session revocation
  * Back-channel token acquisition \ renewal
    * [I think] lack of iFrames kills a silent `Code` flow
    * The Ping JS SDK specifically mentions using an iFrame for this - presumably it doesn't work
* PingOne delivered pages
  * Slow - takes ~4s to render the login page
    * There's a bunch of tracking JS we use
  * Inconsistent branding
    * We add a Grey page and spinner in the middle of the authentication
* All this interferes with any other Product
  * If you can't integrate the first step, things like Flow Manager are completely irrelevent as you can't get to them.
* One-to-One Branding
  * Only one branded UX \ domain allowed per Env
  * No CORS to support multiple DNS domains for Apps
* There is no concept of SDLC in P1
  * No ability to re-create, clone, export and import environments
  * How are teams expected to handle Dev \ Test \ Prod pipelines?
  