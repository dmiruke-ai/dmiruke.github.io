# Sprint 03 — EKS Cluster + Node Groups

| File | What to capture |
|------|----------------|
| `01-eks-console.png` | AWS Console → EKS → `pel-eks-dev` cluster — status ACTIVE, k8s version visible |
| `02-node-groups.png` | AWS Console → EKS → `pel-eks-dev` → Compute — both node groups listed |
| `03-kubectl-get-nodes.png` | Terminal: `kubectl get nodes -o wide` — 2 Ready nodes with AZ spread |
| `04-irsa-roles.png` | AWS Console → IAM → Roles — filtered to `pel-irsa-*` showing all IRSA roles |
| `05-oidc-provider.png` | AWS Console → IAM → Identity providers — EKS OIDC provider for `pel-eks-dev` |
