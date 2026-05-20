# dmiruke.dev — Portfolio

[![Platform Engineering Lab](https://img.shields.io/badge/Platform%20Engineering%20Lab-EKS%20%7C%20ArgoCD%20%7C%20Terraform-5fc77a?style=for-the-badge)](https://dmiruke-ai.github.io/platform-engineering-lab-public/)
[![AEGIS Certify](https://img.shields.io/badge/AEGIS%20Certify-AI%20Governance-b48cff?style=for-the-badge)](https://github.com/dmiruke-ai/aegis-certify-public)
[![Mnemos](https://img.shields.io/badge/Mnemos-Agentic%20Memory%20%7C%205--layer%20Code%20Graph-0ea5e9?style=for-the-badge)](https://github.com/dmiruke-ai/mnemos-public)

**Dattaram Miruke** — Principal AI Platform Architect · DevOps · Kubernetes · AWS · Distributed Systems

---

## Flagship Projects

### Platform Engineering Lab
> Production-grade internal Platform Engineering reference architecture on AWS EKS.

| | |
|---|---|
| **Stack** | Terraform · EKS · ArgoCD · ingress-nginx · cert-manager · Prometheus · Grafana · Loki · Tempo · Kyverno · OpenCost · Velero · External Secrets · GitHub Actions ARC |
| **Patterns** | Multi-env (dev/prod) · IRSA · GitOps app-of-apps · OPA policy-as-code · FinOps rightsizing · Phase 4 agentic IaC generation |
| **Deep dive** | [dmiruke-ai.github.io/platform-engineering-lab-public/](https://dmiruke-ai.github.io/platform-engineering-lab-public/) |
| **Build story** | [Sessions 1–6 · bugs · fixes · decisions](https://dmiruke-ai.github.io/platform-engineering-lab-public/blog-cluster-build-story.html) |
| **Showcase repo** | [github.com/dmiruke-ai/platform-engineering-lab-public](https://github.com/dmiruke-ai/platform-engineering-lab-public) |
| **Source** | [github.com/dmiruke-ai/platform-engineering-lab](https://github.com/dmiruke-ai/platform-engineering-lab) |

---

### AEGIS Certify — AI Trust & Evaluation Framework

[![AEGIS Certify](https://img.shields.io/badge/AEGIS%20Certify-AI%20Governance%20%7C%20115%20PCUs-b48cff?style=for-the-badge)](https://github.com/dmiruke-ai/aegis-certify-public)

> Deterministic AI compliance assurance — governance, evaluation, and safety layer for agentic AI systems.

| | |
|---|---|
| **Architecture** | 17-gate control plane (G1–G17) · FAIL-dominant lattice · Matroid independence |
| **Coverage** | 115 PCUs · 12 frameworks: GDPR, EU AI Act, NIST AI RMF, SOC 2, HIPAA, PCI-DSS, Agentic R1–R7 |
| **Interfaces** | REST API · gRPC · Python SDK · CLI · OPA/Kyverno bundle export |
| **Research** | H1–H7 hypotheses · 866 test cases · 0% false positive rate (H5) |
| **Source** | [github.com/dmiruke-ai/aegis-certify-public](https://github.com/dmiruke-ai/aegis-certify-public) |

---

### Mnemos — Persistent Agentic Memory with Provenance

[![Live API](https://img.shields.io/badge/Live%20API-Swagger%20UI-b48cff?style=flat-square)](http://37.27.97.75:8200/docs)
[![Dashboard](https://img.shields.io/badge/Dashboard-Mnemos%20UI-5fc77a?style=flat-square)](http://37.27.97.75:3002/)
[![Grafana](https://img.shields.io/badge/Observability-Grafana-f59e0b?style=flat-square)](http://37.27.97.75:10210/d/mnemos-overview/)
[![Public Repo](https://img.shields.io/badge/Repo-mnemos--public-0ea5e9?style=flat-square)](https://github.com/dmiruke-ai/mnemos-public)

> AI-accessible memory system that treats every fact as a **positioned, typed, graph-aware** unit — not an opaque embedded chunk. Documents keep their **page tree** so retrieval results carry `Doc > §3 > p.5` breadcrumbs. Codebases are ingested as a **5-layer semantic graph** (structural / AST / runtime-ops / semantic / relationship), not flat RAG.

#### The differentiator vs RAG-over-files

| | RAG-over-files | **Mnemos** |
|---|---|---|
| Provenance | snippet only | **Breadcrumb tree** + source-specific anchor |
| Code | embedded text chunks | **5-layer semantic graph** (symbols + callgraph + infra + relationships) |
| Retrieval substrates | one (vector) | **three** — symbol trie · vector · graph traversal |
| Agent surface | none | **27 MCP tools** (Claude Desktop / Cursor / any MCP client) |
| Operational reasoning | none | **infra_resources** parsed from terraform / k8s / GH-Actions / Dockerfile |
| Observability | none | **Prometheus + Grafana** — 36 custom series, <1% p99 latency overhead |

#### Live system

| | |
|---|---|
| **Dashboard** | [http://37.27.97.75:3002/](http://37.27.97.75:3002/) — `/memories` · `/search` · `/graph` · `/codebases` · `/admin` |
| **REST API (Swagger)** | [http://37.27.97.75:8200/docs](http://37.27.97.75:8200/docs) — 64 endpoints, interactive try-it-out |
| **Prometheus** | [http://37.27.97.75:9091/](http://37.27.97.75:9091/) — 36 custom series, 15-day retention |
| **Grafana** | [http://37.27.97.75:10210/d/mnemos-overview/](http://37.27.97.75:10210/d/mnemos-overview/) — 13-panel dashboard (anon viewer, admin `admin/mnemos`) |
| **MCP server** | 27 typed tools — `find_symbol`, `who_calls`, `get_symbol_callgraph`, `semantic_search` w/ breadcrumb, `get_infra_resources`, … |

#### Architecture at a glance

| | |
|---|---|
| **Stack** | Python · FastAPI · gunicorn · Postgres 16 · pgvector · pg_trgm · Redis · arq · Ollama (`mxbai-embed-large`) · Next.js · Prometheus · Grafana |
| **Storage substrates** | `memories` (typed AKUs) · `document_nodes` + `document_terms` (page tree) · `code_symbols` + `code_relationships` (executable graph) · `infra_resources` (terraform/k8s/CI) · `embeddings` (HNSW) |
| **Retrieval** | Three substrates fused: **A · symbol trie** (pg_trgm GIN, <1ms) · **B · vector** (pgvector HNSW + hybrid score) · **C · graph** (recursive CTE over edges, cross-file callgraph) |
| **Ingest** | Per-source map builders (PDF, Markdown, code AST) + infra parsers (terraform / kubernetes / github-actions / dockerfile) — all populated in one transaction per file |
| **Async tier** | arq on Redis; ingest endpoints >1s return 202 + job_id; embedding dispatcher polls every 30s |
| **Schema** | 21 numbered migrations; current `0.21.0`; forward + rollback pairs |

#### What it proves

| | |
|---|---|
| **End-to-end demo** | 108-page PDF ingest → page-tree built → `semantic_search` returns `Breadcrumb: Open Brain Architecture > p.5` + `Anchor: {"page_num": 5, ...}` |
| **5-layer code graph** | 2,526 symbols + 10,793 relationships extracted from mnemos itself (169 .py files) in one pass |
| **Cross-file callgraph** | `who_calls("get_pool") → get_conn at api/db_pool.py:68` resolved via recursive CTE |
| **Operational graph** | `aws_instance.web → aws_subnet.public`, `Deployment/api → ConfigMap/api-config`, `workflow.CI/job.deploy → workflow.CI/job.test` — dependency edges parsed from raw HCL / YAML |
| **MCP drift verification** | 25/27 tools pass against the live schema (2 expected env fails) — automated via `scripts/mcp_drift_verify.py` |
| **Observability** | Prom + Grafana stack with HTTP middleware, search counters, ingest counters, DB pool gauges — `<1%` added p99 latency, ~300 MB extra RAM |

#### Documentation

| | |
|---|---|
| **Public repo** | [github.com/dmiruke-ai/mnemos-public](https://github.com/dmiruke-ai/mnemos-public) |
| **Architecture** | [`docs/ARCHITECTURE.md`](https://github.com/dmiruke-ai/mnemos-public/blob/main/docs/ARCHITECTURE.md) — components, ingest, retrieval funnel, deployment, security |
| **Diagram** | [`docs/architecture.svg`](https://github.com/dmiruke-ai/mnemos-public/blob/main/docs/architecture.svg) — single-page system overview |
| **Product writeup** | [`docs/PRODUCT_WRITEUP.md`](https://github.com/dmiruke-ai/mnemos-public/blob/main/docs/PRODUCT_WRITEUP.md) — problem, solution, positioning, use cases |
| **5-layer code graph** | [`docs/CODE_INGESTION_5_LAYERS.md`](https://github.com/dmiruke-ai/mnemos-public/blob/main/docs/CODE_INGESTION_5_LAYERS.md) — the differentiator, full schema + worked example |
| **Memory taxonomy** | [`docs/MEMORY_TAXONOMY.md`](https://github.com/dmiruke-ai/mnemos-public/blob/main/docs/MEMORY_TAXONOMY.md) — 8 typed memory kinds, tag conventions |
| **API reference** | [`docs/API_REFERENCE.md`](https://github.com/dmiruke-ai/mnemos-public/blob/main/docs/API_REFERENCE.md) — curated endpoint map with live curl examples |
| **MCP tools** | [`docs/MCP_TOOLS.md`](https://github.com/dmiruke-ai/mnemos-public/blob/main/docs/MCP_TOOLS.md) — 27 tools + Claude Desktop / Cursor config |
| **Monitoring** | [`docs/MONITORING.md`](https://github.com/dmiruke-ai/mnemos-public/blob/main/docs/MONITORING.md) — what's instrumented, overhead measurements |

> **Patent pending.** The hosted demo is free for evaluation; commercial use, derivative work, and embedded integration require written permission.

---

### AgenticDevops — AI DevOps Agent Platform

[![AgenticDevops](https://img.shields.io/badge/AgenticDevops-AI%20DevOps%20%7C%20LangGraph%20%7C%20OPA-f0b95c?style=for-the-badge)](https://github.com/dmiruke-ai/agenticdevops-public)
[![Live API](https://img.shields.io/badge/Live%20API-Swagger%20UI-b48cff?style=flat-square)](http://37.27.97.75:8000/docs)
[![Grafana](https://img.shields.io/badge/Observability-Grafana-f59e0b?style=flat-square)](http://37.27.97.75:3010/)
[![Jaeger](https://img.shields.io/badge/Tracing-Jaeger-e08a2b?style=flat-square)](http://37.27.97.75:16686/)

> AI-powered multi-agent platform that converts natural language into production-ready Terraform, CI/CD pipelines, and IAM policies — with deterministic OPA safety gates, confidence-tracked intent, Tree-of-Thought FinOps scoring, and human-in-the-loop approval.

| | |
|---|---|
| **Stack** | LangGraph · FastAPI · Terraform · OPA (Rego) · OpenTelemetry · Prometheus · Grafana · Jaeger · Redis |
| **Patterns** | 4-band confidence intent · OPA intent gate (injection + IAM + SG) · 15-type error classifier · Tree-of-Thought FinOps · blast-radius HITL approval |
| **Tests** | 426 passing · 5 sprints complete |
| **API (Swagger UI)** | [http://37.27.97.75:8000/docs](http://37.27.97.75:8000/docs) |
| **Grafana** | [http://37.27.97.75:3010/](http://37.27.97.75:3010/) — anon viewer · admin `admin/devops123` |
| **Jaeger** | [http://37.27.97.75:16686/](http://37.27.97.75:16686/) — distributed traces |
| **Showcase repo** | [github.com/dmiruke-ai/agenticdevops-public](https://github.com/dmiruke-ai/agenticdevops-public) |
| **Source** | [github.com/dmiruke-ai/AgenticDevops](https://github.com/dmiruke-ai/AgenticDevops) |

---

## Contact

**Dattaram Miruke**
[dmiruke@gmail.com](mailto:dmiruke@gmail.com) · [github.com/dmiruke-ai](https://github.com/dmiruke-ai)
