---
layout: layouts/facile.njk
title: Widget - Redirectless
eleventyNavigation:
  key: Widget - Redirectless
  parent: Tools
  order: 7
---

This app is used to show the PingFed AuthN Widget in a redirectless flow (PF proprietary). It uses the `response_mode=pi.flow` to initiate the OIDC request
without starting at PingFed.

If you want to change the branding:

1. Start with a new copy of the app -- [Remix Widget](https://glitch.new/~facile-redirectless)
2. Add your Logo image to the `/assets` folder
3. Copy the Logo URL and follow the instructions in the [README](https://glitch.com/edit/#!/facile-redirectless)