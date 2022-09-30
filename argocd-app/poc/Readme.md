# Create argocd application to create another applications
```bash
echo '
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: application-base
  namespace: argocd
spec:
  project: default

  source:
    repoURL: https://github.com/junjieyjj/arocd-app-config.git
    targetRevision: HEAD
    path: argocd-app
  destination:
    server: https://kubernetes.default.svc
    namespace: argocd

  syncPolicy:
    automated:
      prune: true
      selfHeal: true
    syncOptions:
    - CreateNamespace=true
' | kubectl apply -f -
```