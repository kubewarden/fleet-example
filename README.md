# Kubewarden Fleet example

This example will deploy Kubewarden packaged as Helm charts from the Kubewarden
Helm repo, https://charts.kubewarden.io, into the `cattle-fleet-system`
namespace. The defined Fleet modules have the chart dependencies codified via
`dependsOn`.

```yaml
kind: GitRepo
apiVersion: fleet.cattle.io/v1alpha1
metadata:
  name: kubewarden-example
  namespace: fleet-local
spec:
  repo: https://github.com/kubewarden/kubewarden-fleet
  branch: main
  paths:
    - cert-manager/
    - jaeger/
    - kubewarden/
    - open-telemetry/
    - rancher-monitoring/

  # remove any external change done by resources owned by Fleet:
  correctDrift:
    enabled: true
    force: true
```
