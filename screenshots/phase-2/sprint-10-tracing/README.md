# Sprint 10 — Distributed Tracing (Tempo + OTel)

| File | What to capture |
|------|----------------|
| `01-tempo-trace-view.png` | Grafana → Explore → Tempo — full trace for a demo-app request with all spans expanded |
| `02-tempo-service-graph.png` | Grafana → Tempo → Service Graph — nodes and edges between services |
| `03-otel-collector-pods.png` | Terminal: `kubectl get pods -n observability \| grep otel` — collector Running |
| `04-tempo-s3-bucket.png` | AWS Console → S3 → `pel-tempo-*` bucket — objects growing (trace data) |
