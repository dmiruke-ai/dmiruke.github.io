# Phase 1 Screenshots

Core Platform MVP — VPC, EKS, GitOps, Observability, Security, CI/CD, Demo App.

## Capture list

| File | What to capture | How |
|------|----------------|-----|
| `01-argocd-apps-healthy.png` | ArgoCD UI showing all applications Synced + Healthy | `kubectl port-forward svc/argocd-server -n argocd 8080:80` → https://localhost:8080 |
| `02-grafana-cluster-overview.png` | Grafana cluster-overview dashboard with live node/pod metrics | `kubectl port-forward svc/kube-prometheus-stack-grafana -n observability 3000:80` → http://localhost:3000 |
| `03-grafana-example-app.png` | Grafana example-app dashboard (request rate, error ratio, p99 latency) | Same Grafana port-forward |
| `04-grafana-argocd.png` | Grafana ArgoCD dashboard (sync ops, git fetch latency) | Same Grafana port-forward |
| `05-grafana-ingress-nginx.png` | Grafana ingress-nginx dashboard (request rate, 5xx rate) | Same Grafana port-forward |
| `06-kubectl-pods-all.png` | Terminal: `kubectl get pods -A` showing full stack running | Terminal screenshot |
| `07-example-app-browser.png` | example-app JSON response in browser with TLS lock icon | https://demo.dev.pel.<domain> |
| `08-kyverno-deny.png` | Kyverno blocking a privileged pod (`kubectl apply` denied) | Terminal: apply a privileged pod manifest |
| `09-cloudwatch-dashboard.png` | AWS CloudWatch dashboard `pel-phase-1-dev` | AWS Console → CloudWatch → Dashboards |
| `10-github-actions-passing.png` | GitHub Actions: build + checkov + trivy all green checks | GitHub repo → Actions tab |
