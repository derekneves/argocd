## cert-manager
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.18.2/cert-manager.yaml

## Bootstrap Kargo

pass=$(openssl rand -base64 48 | tr -d "=+/" | head -c 32)
echo "Password: $pass"
echo "Password Hash: $(htpasswd -bnBC 10 "" $pass | tr -d ':\n')"
echo "Signing Key: $(openssl rand -base64 48 | tr -d "=+/" | head -c 32)"

# use app spec 
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: kargo
  namespace: argocd
spec:
  project: default
  destination:
    namespace: kargo
    server: https://kubernetes.default.svc
  sources:
    - repoURL: ghcr.io/akuity/kargo-charts
      chart: kargo
      targetRevision: "1.7.4"
      helm:
        valueFiles:
          - $values/kargo/values.yaml
    - repoURL: https://github.com/example/repo.git
      targetRevision: main
      ref: values
      path: kargo/additional-manifests
  syncPolicy:
    syncOptions:
    - CreateNamespace=true