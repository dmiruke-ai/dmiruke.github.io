# Sprint 15 — Required Cost-Allocation Labels

| File | What to capture |
|------|----------------|
| `01-kyverno-label-deny.png` | Terminal: `kubectl apply` of pod missing `pel:cost-center` label → Kyverno deny in prod-apps |
| `02-kyverno-policy-report-labels.png` | Terminal: `kubectl get policyreport -n dev-apps` — audit violations for missing labels |
| `03-opencost-label-columns.png` | OpenCost UI → Cost Allocation grouped by `pel:cost-center` — non-empty column |
| `04-require-cost-labels-policy.png` | Terminal: `kubectl describe clusterpolicy require-cost-labels` — policy spec visible |
