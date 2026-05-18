# Sprint 16 — cosign Image Signing + Kyverno Verification

| File | What to capture |
|------|----------------|
| `01-ecr-signed-image.png` | AWS Console → ECR → image list — sha-tagged image + cosign signature manifest alongside it |
| `02-cosign-verify-terminal.png` | Terminal: `cosign verify ... <image>` returning exit 0 with Rekor log entry |
| `03-kyverno-unsigned-deny.png` | Terminal: apply unsigned image to prod-apps → Kyverno deny with "image not signed" message |
| `04-kyverno-unsigned-audit.png` | Terminal: `kubectl get policyreport -n dev-apps` — unsigned image audit violation visible |
| `05-github-actions-sign-step.png` | GitHub Actions workflow run — cosign sign step green with Rekor URL in output |
