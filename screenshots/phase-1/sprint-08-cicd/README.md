# Sprint 08 — CI/CD Reusable Workflows

| File | What to capture |
|------|----------------|
| `01-github-actions-build-pass.png` | GitHub Actions: full build pipeline green — lint → trivy → build → push → sign |
| `02-ecr-image-signed.png` | AWS Console → ECR → repository — image with sha tag + cosign signature manifest |
| `03-tf-plan-comment.png` | GitHub PR: terraform plan posted as comment with resource diff |
| `04-tf-apply-approval.png` | GitHub Actions: environment protection gate requiring manual approval before apply |
| `05-actionlint-pass.png` | GitHub Actions: actionlint step green in the lint workflow |
