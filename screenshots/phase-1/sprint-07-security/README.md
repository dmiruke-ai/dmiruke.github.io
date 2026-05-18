# Sprint 07 — Security Baseline

| File | What to capture |
|------|----------------|
| `01-kyverno-deny-privileged.png` | Terminal: `kubectl apply` of a privileged pod → admission denied by Kyverno |
| `02-kyverno-deny-no-limits.png` | Terminal: `kubectl apply` of pod missing resource limits → admission denied |
| `03-kyverno-policy-list.png` | Terminal: `kubectl get clusterpolicy` — all policies listed with READY=True |
| `04-kyverno-policy-report.png` | Terminal: `kubectl get policyreport -A` — audit results per namespace |
| `05-trivy-operator-report.png` | Terminal: `kubectl get vulnerabilityreport -A` — CVE scan results for running images |
| `06-checkov-pr-block.png` | GitHub Actions: checkov blocking a PR that adds unencrypted S3 bucket |
