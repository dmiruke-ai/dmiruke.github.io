# Phase 4 Screenshots

Agentic Platform Engineering — LangGraph intent parser, Terraform generator, policy enforcer, FinOps advisor.

## Capture list

| File | What to capture | How |
|------|----------------|-----|
| `01-agent-intent-input.png` | Intent YAML input fed to the agent pipeline (cluster_type, env, team) | Terminal or agent UI |
| `02-agent-tf-output.png` | Generated Terraform plan output from infra-generator agent | Terminal: agent run output |
| `03-agent-policy-check.png` | Policy-agent validating the generated plan (Checkov + OPA) | Terminal: policy check result |
| `04-agent-finops-recommendation.png` | FinOps agent recommending instance rightsizing based on OpenCost data | Terminal or agent UI |
| `05-agent-remediation.png` | Remediation agent auto-fixing a Kyverno policy violation | Terminal: before/after patch |
| `06-langgraph-flow.png` | LangGraph agent DAG visualization showing the full pipeline | LangGraph Studio or rendered graph |
