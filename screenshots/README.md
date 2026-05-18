# Portfolio Screenshots

Screenshots organized by phase and sprint. Drop PNG files into the matching sprint folder — the README in each folder lists exactly what to capture and how.

## Naming convention

```
<sequence>-<what-it-shows>.png
```

Sequence is two digits (01, 02, ...) so files sort in display order. Name describes the content, not the tool (`grafana-cluster-overview` not `dashboard-1`). PNG preferred; crop to the relevant UI region; max 1920×1080.

## Folder structure

```
screenshots/
├── phase-1/                         # Core Platform MVP
│   ├── sprint-01-bootstrap/
│   ├── sprint-02-terraform/
│   ├── sprint-03-eks/
│   ├── sprint-04-cluster-bootstrap/
│   ├── sprint-05-gitops/
│   ├── sprint-06-observability/
│   ├── sprint-07-security/
│   ├── sprint-08-cicd/
│   └── sprint-09-demo-app/
└── phase-2/                         # Reliability + FinOps
    ├── sprint-10-tracing/
    ├── sprint-11-slos/
    ├── sprint-12-velero/
    ├── sprint-13-chaos/
    ├── sprint-14-opencost/
    ├── sprint-15-cost-labels/
    ├── sprint-16-cosign/
    ├── sprint-17-falco/
    ├── sprint-18-conftest/
    └── sprint-19-arc-runners/
```

## Status

| Phase | Sprints | Status |
|-------|---------|--------|
| Phase 1 — MVP | 01–09 | ⏳ capturing |
| Phase 2 — Reliability | 10–19 | ⏳ capturing |
| Phase 3 — Platform | 20–32 | 📋 planned |
| Phase 4 — Agentic | 33–45 | 📋 planned |

## High-value composites (take these first)

| Composite | Files needed |
|-----------|-------------|
| ArgoCD all-green app tree | `phase-1/sprint-05-gitops/01-argocd-app-tree.png` |
| Grafana cluster + cost side-by-side | `sprint-06/01-grafana-cluster-overview.png` + `sprint-14/03-grafana-cost-overview.png` |
| Kyverno admission deny (terminal) | `sprint-07/01-kyverno-deny-privileged.png` |
| Falco exec detection | `sprint-17/01-falco-exec-alert.png` + `sprint-17/02-slack-falco-alert.png` |
| Full CI pipeline green | `sprint-08/01-github-actions-build-pass.png` |
