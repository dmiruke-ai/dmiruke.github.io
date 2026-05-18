# Sprint 19 — ARC Self-Hosted Runners

| File | What to capture |
|------|----------------|
| `01-arc-scale-zero.png` | Terminal: `kubectl get pods -n arc-runners` — 0 pods when no jobs queued |
| `02-arc-scale-up.png` | Terminal: `kubectl get pods -n arc-runners` — runner pods appearing during a build |
| `03-arc-scale-down.png` | Terminal: runner pods terminating after job completes (before/after) |
| `04-github-actions-self-hosted.png` | GitHub Actions job run detail — "Runs on: pel-self-hosted-arc" label visible |
| `05-arc-controller-pods.png` | Terminal: `kubectl get pods -n arc-systems` — controller Running |
