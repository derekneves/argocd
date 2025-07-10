## install argocd (non HA)
kubectl apply -k https://github.com/argoproj/argo-cd/blob/master/manifests/install.yaml

### install CRDs (only when in namespace mode)
kubectl apply -k https://github.com/argoproj/argo-cd/manifests/crds\?ref\=stable


## password
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
