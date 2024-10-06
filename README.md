<h2 align="center"> JAMF manifests</h2>

Manifests repository that contains Kustomize manifests and Helm Charts to deploy [go-jamf application](https://github.com/mimotej/jamf-go) GitOps ways.

# Structure of the the repository

Repository has following structure:

```
apps/
├─ app-of-apps/
├─ argo-apps/production/apps/
│  ├─ argocd.yaml
│  ├─ ...
├─ go-jamf/
cluster-scope/
├─ base/core/
│  ├─ namespaces/
├─ overlays/production/
```
Manifests are split into two parts `apps` and `cluster-scope`:

### Apps

`apps` contains manifests related to the deployment of applications. Those manifests include, various kustomize manifests for deployment of ArgoCD, ArgoCD application manifests and helm charts of the `go-jamf` application. They are structured in the way that we can reference these files in ArgoCD and they can be synced through `app-of-apps` that is central part of this structure.

### Cluster-scope

`cluster-scope` serves for deployment of infrastracture (in this case for definition of namespaces, but could also be used for cluster-wide limitRanges etc.). Separation of these two structures makes reviews easier and can provide options for further automation.

### Local deployment

These manifests should be deployable in any type of Kubernetes cluster, only requirement is nginx ingress controller, which can be setup either as an addon with minikube or can be installed using helm-charts/additional manifests.
