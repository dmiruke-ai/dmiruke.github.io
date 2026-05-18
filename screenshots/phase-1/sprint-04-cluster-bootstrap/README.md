# Sprint 04 — Cluster Bootstrap

| File | What to capture |
|------|----------------|
| `01-kubectl-pods-platform.png` | Terminal: `kubectl get pods -n platform-system` — ingress-nginx, external-dns, ESO all Running |
| `02-cert-manager-pods.png` | Terminal: `kubectl get pods -n cert-manager` — 3 pods Running |
| `03-external-secrets-synced.png` | Terminal: `kubectl get externalsecret -A` — READY=True for all secrets |
| `04-ingress-class.png` | Terminal: `kubectl get ingressclass` — `nginx` listed as default |
| `05-nlb-console.png` | AWS Console → EC2 → Load Balancers — `pel-nlb-dev` Active |
