# dmiruke.dev — Portfolio

[![Live Site](https://img.shields.io/badge/Live%20Site-dmiruke.dev-6aa7ff?style=for-the-badge&logo=github)](https://dmiruke-ai.github.io/dmiruke.github.io/)
[![Platform Engineering Lab](https://img.shields.io/badge/Platform%20Engineering%20Lab-EKS%20%7C%20ArgoCD%20%7C%20Terraform-5fc77a?style=for-the-badge)](https://dmiruke-ai.github.io/dmiruke.github.io/platform-engineering-lab/)
[![AEGIS Certify](https://img.shields.io/badge/AEGIS%20Certify-AI%20Governance%20%7C%20115%20PCUs-b48cff?style=for-the-badge)](https://dmiruke-ai.github.io/dmiruke.github.io/platform-engineering-lab/aegis.html)

**Dattaram Miruke** — Principal AI Platform Architect · DevOps · Kubernetes · AWS · Distributed Systems

---

## Portfolio

> **[→ View live portfolio](https://dmiruke-ai.github.io/dmiruke.github.io/portfolio/)**

Role-tailored views available via `?role=` parameter:

| URL | Tailored for |
|-----|-------------|
| [`/portfolio/`](https://dmiruke-ai.github.io/dmiruke.github.io/portfolio/) | General / default |
| [`/portfolio/?role=platform`](https://dmiruke-ai.github.io/dmiruke.github.io/portfolio/?role=platform) | Platform / Infra roles |
| [`/portfolio/?role=mlops`](https://dmiruke-ai.github.io/dmiruke.github.io/portfolio/?role=mlops) | MLOps / AI Platform |
| [`/portfolio/?role=rag`](https://dmiruke-ai.github.io/dmiruke.github.io/portfolio/?role=rag) | Applied GenAI / RAG |
| [`/portfolio/?role=genai-lead`](https://dmiruke-ai.github.io/dmiruke.github.io/portfolio/?role=genai-lead) | GenAI Engineering Lead |

---

## Flagship Projects

### Platform Engineering Lab
> Production-grade internal Platform Engineering reference architecture on AWS EKS.

| | |
|---|---|
| **Stack** | Terraform · EKS · ArgoCD · ingress-nginx · cert-manager · Prometheus · Grafana · Loki · Tempo · Kyverno · OpenCost · Velero · External Secrets · GitHub Actions ARC |
| **Patterns** | Multi-env (dev/prod) · IRSA · GitOps app-of-apps · OPA policy-as-code · FinOps rightsizing · Phase 4 agentic IaC generation |
| **Deep dive** | [platform-engineering-lab/](https://dmiruke-ai.github.io/dmiruke.github.io/platform-engineering-lab/) |
| **Build story** | [9 sessions · bugs · fixes · decisions](https://dmiruke-ai.github.io/dmiruke.github.io/platform-engineering-lab/blog-cluster-build-story.html) |
| **Source** | [github.com/dmiruke-ai/platform-engineering-lab](https://github.com/dmiruke-ai/platform-engineering-lab) |

---

### AEGIS Certify — AI Trust & Evaluation Framework
> Deterministic AI compliance assurance — governance, evaluation, and safety layer for agentic AI systems.

| | |
|---|---|
| **Architecture** | 17-gate control plane (G1–G17) · FAIL-dominant lattice · Matroid independence |
| **Coverage** | 115 PCUs · 12 frameworks: GDPR, EU AI Act, NIST AI RMF, SOC 2, HIPAA, PCI-DSS, Agentic R1–R7 |
| **Interfaces** | REST API · gRPC · Python SDK · CLI · OPA/Kyverno bundle export |
| **Research** | H1–H7 hypotheses · 866 test cases · 0% false positive rate (H5) |
| **Deep dive** | [platform-engineering-lab/aegis.html](https://dmiruke-ai.github.io/dmiruke.github.io/platform-engineering-lab/aegis.html) |
| **Source** | [github.com/dmiruke-ai/aegis-certify-public](https://github.com/dmiruke-ai/aegis-certify-public) |

---

## Repo Structure

```
dmiruke.github.io/
├── index.html                       ← landing page
├── platform-engineering-lab/
│   ├── index.html                   ← EKS architecture deep dive
│   ├── blog-cluster-build-story.html ← build story (sessions 1–6)
│   └── aegis.html                   ← AI governance framework
└── portfolio/
    ├── index.html                   ← role-tailored recruiter portfolio
    ├── screenshots/                 ← infrastructure evidence captures
    └── assets/                      ← roles.js · roles.json · resume PDFs
```

---

## Contact

**Dattaram Miruke**
[dmiruke@gmail.com](mailto:dmiruke@gmail.com) · [github.com/dmiruke-ai](https://github.com/dmiruke-ai)

> Custom domain `dmiruke.dev` pending DNS propagation — github.io links above are live now.
