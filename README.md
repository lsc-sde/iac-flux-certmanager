# iac-flux-certmanager
Flux configuration for Certificate Manager

## Developer Guide
To test the changes, ensure that you are on your developer machine and that the context is set correctly to your local instance please amend the following script to use the target branch:

```bash
kubectl config use-context docker-desktop
kubectl create namespace cert-manager
flux create source git cert-manager --url="https://github.com/lsc-sde/iac-flux-certmanager" --branch=main --namespace=cert-manager
flux create kustomization cert-manager-sources --source="GitRepository/cert-manager" --namespace=cert-manager --path="./sources" --interval=1m --prune=true --health-check-timeout=10m --wait=false
flux create kustomization cert-manager-cluster-config --source="GitRepository/cert-manager" --namespace=cert-manager --path="./clusters/local" --interval=1m --prune=true --health-check-timeout=10m --wait=false
```

This should in turn deploy all of the resulting resources on your local cluster.