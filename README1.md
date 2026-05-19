# dmiruke.dev — Portfolio

[![Platform Engineering Lab](https://img.shields.io/badge/Platform%20Engineering%20Lab-EKS%20%7C%20ArgoCD%20%7C%20Terraform-5fc77a?style=for-the-badge)](https://dmiruke-ai.github.io/platform-engineering-lab-public/)
[![AEGIS Certify](https://img.shields.io/badge/AEGIS%20Certify-AI%20Governance-b48cff?style=for-the-badge)](https://github.com/dmiruke-ai/aegis-certify-public)
[![Mnemos](https://img.shields.io/badge/Mnemos-Agentic%20Memory%20%7C%205--layer%20Code%20Graph-0ea5e9?style=for-the-badge)](https://github.com/dmiruke-ai/mnemos-public)

**Dattaram Miruke** — Principal AI Platform Architect · DevOps · Kubernetes · AWS · Distributed Systems

---

## About Me

I design and build **production-grade AI platforms and cloud-native systems** at scale.

- AI Control Planes, Multi-Agent Systems, RAG Pipelines
- Kubernetes Platform Engineering, Distributed Systems
- AWS Multi-Region Architectures, Event-Driven Systems
- AI Governance, Observability, and Policy Enforcement

I specialize in turning **ambiguous problems into structured, scalable systems**.

> *"Context and memory turn an LLM into a teammate."*

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
| **Evaluation pipelines** | RAGAS · DeepEval — automated LLM output scoring |
| **Policy enforcement** | OPA · RBAC · Zero Trust guardrails |
| **Observability** | Scoring engine + audit trail per evaluation run |
| **Validation** | Multi-agent workflow validation across agent topologies |
| **Source** | [github.com/dmiruke-ai/aegis-certify-public](https://github.com/dmiruke-ai/aegis-certify-public) |

---

### DevOps Agent — Infrastructure Orchestration System

> AI agent that converts intent into Terraform + CI/CD pipelines — natural language → production infrastructure.

| | |
|---|---|
| **Core capability** | Multi-cloud infra generation (AWS / Kubernetes) from plain-English intent |
| **Scoring** | Architecture scoring engine — validates generated plans before apply |
| **CI/CD** | GitHub Actions automation — full pipeline generation from spec |
| **Validation** | Plan preview + human-in-the-loop confirmation before execution |
| **Status** | Repo link coming soon |

---

### RAG Platform — Document Intelligence System

> End-to-end ingestion → embedding → retrieval → evaluation pipeline for production RAG workloads.

| | |
|---|---|
| **Ingestion** | Multi-channel: docs, APIs, streams |
| **Search** | Semantic search pipelines (vector + metadata hybrid) |
| **Prompting** | PromptBuilder for structured, reproducible prompt generation |
| **Memory** | Persistent AI memory via Mnemos integration |
| **Status** | Repo link coming soon |

---

### Mnemos — Persistent Agentic Memory with Provenance

[![Live API](https://img.shields.io/badge/Live%20API-Swagger%20UI-b48cff?style=flat-square)](http://37.27.97.75:8200/docs)
[![Dashboard](https://img.shields.io/badge/Dashboard-Mnemos%20UI-5fc77a?style=flat-square)](http://37.27.97.75:3002/)
[![Grafana](https://img.shields.io/badge/Observability-Grafana-f59e0b?style=flat-square)](http://37.27.97.75:10210/d/mnemos-overview/)
[![Public Repo](https://img.shields.io/badge/Repo-mnemos--public-0ea5e9?style=flat-square)](https://github.com/dmiruke-ai/mnemos-public)

> AI-accessible memory system that treats every fact as a **positioned, typed, graph-aware** unit — not an opaque embedded chunk. Documents keep their **page tree** so retrieval results carry `Doc > §3 > p.5` breadcrumbs. Codebases are ingested as a **5-layer semantic graph** (structural / AST / runtime-ops / semantic / relationship), not flat RAG.

#### Core capabilities

- **Long-term memory** for LLM systems — persists context across sessions and agents
- **Context enrichment pipelines** — augments prompts with relevant historical knowledge
- **Multi-agent memory sharing** — shared memory substrate for agent swarms
- **Retrieval optimization** — three-substrate fusion (symbol trie · vector · graph)

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

## Architecture Focus

The platform follows a layered agentic architecture:

```
User → API Gateway → LLM Control Plane → Agent Orchestrator → Tool Execution Layer
                                                    ↕
                                                 Memory
                                         (persistent · typed · graph-aware)
```

**Cross-cutting concerns across all layers:**

| Concern | Implementation |
|---|---|
| **Observability / Evaluation** | OpenTelemetry · Prometheus · Grafana · RAGAS scoring |
| **Governance / Policy** | OPA policy-as-code · Audit trails · AEGIS gate control plane |
| **Platform** | Kubernetes (EKS) · AWS multi-region · GitOps (ArgoCD) |

---

## Core Stack

### AI / Agent Systems
- LLM Control Planes
- LangChain / LangGraph
- RAG Pipelines
- Multi-Agent Orchestration
- Prompt Engineering Frameworks

### Cloud & Infrastructure
- AWS — EKS, Lambda, S3, RDS, Bedrock
- Multi-Region HA Architectures
- Event-Driven Systems — SNS/SQS, Step Functions

### DevOps / IaC
- Terraform, AWS CDK
- GitHub Actions, GitOps (ArgoCD)
- Kubernetes — EKS, CRDs, Controllers

### Observability
- OpenTelemetry
- Prometheus, Grafana
- ELK, CloudWatch

### Security & Governance
- OPA — Policy-as-Code
- RBAC, Zero Trust
- AI Guardrails

---

## Skills

<!-- Tier 1 — Core identity (largest) -->
![AI Platforms](https://img.shields.io/badge/AI%20Platforms-b48cff?style=for-the-badge)
![Kubernetes](https://img.shields.io/badge/Kubernetes-4ade80?style=for-the-badge)
![AWS](https://img.shields.io/badge/AWS-38bdf8?style=for-the-badge)
![LLM Control Planes](https://img.shields.io/badge/LLM%20Control%20Planes-b48cff?style=for-the-badge)

<!-- Tier 2 — Major expertise -->
![Terraform](https://img.shields.io/badge/Terraform-4ade80?style=for-the-badge)
![Multi-Agent Systems](https://img.shields.io/badge/Multi--Agent%20Systems-b48cff?style=for-the-badge)
![RAG Pipelines](https://img.shields.io/badge/RAG%20Pipelines-b48cff?style=for-the-badge)
![Python](https://img.shields.io/badge/Python-fb923c?style=for-the-badge)
![EKS](https://img.shields.io/badge/EKS-38bdf8?style=for-the-badge)

<!-- Tier 3 — Strong capabilities (flat) -->
![LangChain](https://img.shields.io/badge/LangChain-b48cff?style=flat&logoColor=white)
![LangGraph](https://img.shields.io/badge/LangGraph-b48cff?style=flat&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-fb923c?style=flat&logoColor=white)
![Observability](https://img.shields.io/badge/Observability-fbbf24?style=flat&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-4ade80?style=flat&logoColor=white)
![GitOps](https://img.shields.io/badge/GitOps-4ade80?style=flat&logoColor=white)
![pgvector](https://img.shields.io/badge/pgvector-22d3ee?style=flat&logoColor=white)

<!-- Tier 4 — Solid skills (flat-square) -->
![OpenTelemetry](https://img.shields.io/badge/OpenTelemetry-fbbf24?style=flat-square)
![Grafana](https://img.shields.io/badge/Grafana-fbbf24?style=flat-square)
![Lambda](https://img.shields.io/badge/Lambda-38bdf8?style=flat-square)
![Bedrock](https://img.shields.io/badge/Bedrock-38bdf8?style=flat-square)
![AWS CDK](https://img.shields.io/badge/AWS%20CDK-38bdf8?style=flat-square)
![OPA](https://img.shields.io/badge/OPA-fb7185?style=flat-square)
![RBAC](https://img.shields.io/badge/RBAC-fb7185?style=flat-square)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-22d3ee?style=flat-square)
![Redis](https://img.shields.io/badge/Redis-22d3ee?style=flat-square)
![Kafka](https://img.shields.io/badge/Kafka-22d3ee?style=flat-square)

<!-- Tier 5 — Supporting tech (flat-square, smaller palette) -->
![Step Functions](https://img.shields.io/badge/Step%20Functions-38bdf8?style=flat-square)
![SNS/SQS](https://img.shields.io/badge/SNS%2FSQS-38bdf8?style=flat-square)
![CloudFront](https://img.shields.io/badge/CloudFront-38bdf8?style=flat-square)
![Zero Trust](https://img.shields.io/badge/Zero%20Trust-fb7185?style=flat-square)
![AI Guardrails](https://img.shields.io/badge/AI%20Guardrails-fb7185?style=flat-square)
![Semantic Search](https://img.shields.io/badge/Semantic%20Search-b48cff?style=flat-square)
![DeepEval](https://img.shields.io/badge/DeepEval-b48cff?style=flat-square)
![RAGAS](https://img.shields.io/badge/RAGAS-b48cff?style=flat-square)
![Distributed Systems](https://img.shields.io/badge/Distributed%20Systems-4ade80?style=flat-square)
![Policy-as-Code](https://img.shields.io/badge/Policy--as--Code-fb7185?style=flat-square)
![Chaos Engineering](https://img.shields.io/badge/Chaos%20Engineering-4ade80?style=flat-square)

---

## Experience Highlights

### Principal AI Platform Architect — Inferloop
- Built multi-agent AI platform with Kubernetes + multi-LLM gateways
- Designed LLM control plane (routing, policy, cost optimization)
- Developed OpenBrain memory system (vector + metadata)
- Implemented AI evaluation governance frameworks

### AWS DevOps Architect (Consultant)
- Multi-region HA architectures on AWS
- Event-driven systems (Lambda, Step Functions, SNS/SQS)
- CI/CD automation + CI/CD pipelines

### Senior DevOps Engineer — Amazon
- Built distributed work-driven systems
- IaC platforms using AWS CDK
- Observability frameworks (CloudWatch, DORA metrics)

### Platform Engineering — Cisco / HP / Others
- Kubernetes CRDs + controllers for network services
- Chaos engineering frameworks
- OpenStack / SDN / NFV systems
- Large-scale distributed systems optimization

---

## Thought Leadership

- **Agentic Architecture Index** — in development
- *"Routing is the Interface"* — chapter in *Governance Through AI in Networks*, CRC Press
- *A Security Analysis of Siri VPS* — ACM Annual Conference

---

## Live Systems

| System | URL |
|---|---|
| Mnemos REST API | [http://37.27.97.75:8200/docs](http://37.27.97.75:8200/docs) |
| Mnemos Dashboard | [http://37.27.97.75:3002/](http://37.27.97.75:3002/) |
| Prometheus | [http://37.27.97.75:9091/](http://37.27.97.75:9091/) |
| Grafana | [http://37.27.97.75:10210/d/mnemos-overview/](http://37.27.97.75:10210/d/mnemos-overview/) |

---

## Contact

**Dattaram Miruke**
[dmiruke@gmail.com](mailto:dmiruke@gmail.com) · [github.com/dmiruke-ai](https://github.com/dmiruke-ai)

> Custom domain `dmiruke.dev` pending DNS propagation.
