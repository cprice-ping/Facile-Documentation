---
layout: layouts/facile.njk
title: Bespoke Deployment
eleventyNavigation:
  key: Bespoke
  parent: Deployment
  order: 3
---

Bespoke deployment provides a `values.yaml` file that contains everything that's needed to **manually** deploy the Facile chart.
The Step 2 form allows for the customization of the deployment and associated Use Case configuration.

![Facile Bespoke](https://cdn.glitch.com/6f32d434-43ae-4e29-b7fe-c327613b6a03%2FFacile%20-%20Bespoke.png?v=1627398553555)

### Manual Helm deployment

To manually install via Helm, run the following command:

`helm install {releaseName} --repo https://cprice-ping.github.io/helm-charts ping-facile -f {filename}.yaml`

### Deleting the Release

Unlike [Auto-Deployment](./auto.md), Bespoke deployments need to be manually cleaned up.

- **Helm:** `helm uninstall {releaseName}`
- **PVCs:** `kubectl delete pvc --selector=app.kubernetes.io/instance={releaseName}`
- **PingOne:** Delete the `Admin SSO - {product}` applications (`Connections --> Applications`)

### Reusing the Release Name

You can reuse the Release Name - but you **must** delete the PVCs in-between deployments (the `pingconfig` assumes that nothing exists and builds from scratch)
