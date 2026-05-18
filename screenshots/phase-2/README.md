# Phase 2 Screenshots

Production Reliability + FinOps — Tracing, SLOs, Backups, Chaos, OpenCost, cosign, Falco, ARC.

## Capture list

| File | What to capture | How |
|------|----------------|-----|
| `01-tempo-trace.png` | End-to-end distributed trace for example-app in Grafana/Tempo | Grafana → Explore → Tempo datasource |
| `02-slo-dashboard.png` | SLO burn-rate dashboard with error budget remaining | Grafana → SLO dashboard (Pyrra/Sloth) |
| `03-opencost-namespace.png` | OpenCost cost breakdown by namespace + team label | OpenCost UI or Grafana OpenCost dashboard |
| `04-chaos-mesh-experiment.png` | Chaos Mesh pod-kill experiment running in staging | Chaos Mesh dashboard |
| `05-falco-alert.png` | Falco runtime alert firing on `kubectl exec` into prod pod | Grafana Alertmanager or Slack notification |
| `06-velero-backup.png` | Velero backup schedule + last successful backup timestamp | `kubectl get backups -n velero` terminal |
| `07-cosign-verify.png` | Kyverno blocking unsigned image in prod-apps | Terminal: apply unsigned image, see admission deny |
| `08-arc-runners.png` | ARC self-hosted runners autoscaling in cluster | `kubectl get pods -n actions-runner-system` |
