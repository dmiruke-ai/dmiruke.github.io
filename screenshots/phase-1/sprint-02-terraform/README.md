# Sprint 02 — Terraform Foundation

| File | What to capture |
|------|----------------|
| `01-vpc-console.png` | AWS Console → VPC → VPC list showing `pel-vpc-dev` with 3 AZs, 6 subnets |
| `02-subnets-console.png` | AWS Console → VPC → Subnets filtered to `pel-vpc-dev` — 3 private + 3 public visible |
| `03-nat-gateways.png` | AWS Console → VPC → NAT Gateways — 3 NAT GWs one per AZ |
| `04-kms-keys.png` | AWS Console → KMS → Customer managed keys — `pel-*` keys with rotation enabled |
| `05-tf-plan-pr-comment.png` | GitHub PR comment showing `terraform plan` output posted by Actions |
| `06-checkov-pass.png` | GitHub Actions: checkov step green with `Passed checks: N, Failed checks: 0` |
