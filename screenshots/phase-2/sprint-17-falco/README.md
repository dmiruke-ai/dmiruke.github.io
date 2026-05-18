# Sprint 17 — Falco Runtime Threat Detection

| File | What to capture |
|------|----------------|
| `01-falco-exec-alert.png` | Terminal: `kubectl exec` into a prod pod, then show Falco log entry appearing within 5s |
| `02-slack-falco-alert.png` | Slack #platform-alerts: Falco alert message for the exec event |
| `03-s3-falco-audit.png` | AWS Console → S3 → `pel-falco-audit-dev` — JSON event objects present |
| `04-falco-pods-running.png` | Terminal: `kubectl get pods -n security \| grep falco` — falco + falcosidekick Running |
| `05-grafana-falco-alerts.png` | Grafana → Alertmanager alerts panel — Falco alert group visible |
