[![Stable](https://img.shields.io/badge/status-stable-brightgreen?style=for-the-badge)](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#stable)

# Kubewarden Fleet example

This example will deploy Kubewarden packaged as the `admission-controller`
Helm chart from the Kubewarden Helm repo, https://charts.kubewarden.io, into
the `cattle-kubewarden-system` namespace, along with its optional
dependencies (cert-manager, Jaeger, OpenTelemetry, Rancher Monitoring).
These chart optional dependencies are codified via `dependsOn` in the Fleet
bundles.

```yaml
cat > example.yaml << "EOF"
kind: GitRepo
apiVersion: fleet.cattle.io/v1alpha1
metadata:
  name: kubewarden-example
  namespace: fleet-local
spec:
  repo: https://github.com/kubewarden/fleet-example
  branch: main
  paths:
    - cert-manager/
    - jaeger-operator/
    - kubewarden/
    - open-telemetry/
    - rancher-monitoring/

  # remove any external change done to resources owned by Fleet:
  correctDrift:
    enabled: true
    force: true
EOF

kubectl apply -f example.yaml
```
