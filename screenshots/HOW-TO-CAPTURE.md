# How to Capture Portfolio Screenshots

---

## How nip.io Works — Network Architecture

### The Setup

Three machines are involved:

```
┌─────────────────────────┐        Remote Desktop         ┌──────────────────────────┐
│   Your Laptop / PC      │  ══════════════════════════►  │  Linux Server            │
│   (wherever you sit)    │  (VNC / RDP / NoMachine)      │  37.27.97.75             │
│                         │                               │                          │
│  ┌───────────────────┐  │                               │  • Claude Code runs here │
│  │  Browser          │  │                               │  • kubectl runs here     │
│  │  (your local one) │  │                               │  • git runs here         │
│  └─────────┬─────────┘  │                               └──────────────────────────┘
│            │            │
│            │ opens URL  │
│            ▼            │
│  grafana.35.82.130.149  │
│         .nip.io         │
└─────────────────────────┘
```

### What nip.io Does

nip.io is a free public DNS service. Any hostname in the pattern:

```
<label>.<ip-address>.nip.io
```

resolves to that IP address — no DNS configuration required.

```
grafana.35.82.130.149.nip.io   ──DNS lookup──►  35.82.130.149
prometheus.35.82.130.149.nip.io ─DNS lookup──►  35.82.130.149
backstage.35.82.130.149.nip.io  ─DNS lookup──►  35.82.130.149
```

All point to the same IP (the NLB). The **hostname** is what tells nginx which
backend to route to. Without a hostname, nginx wouldn't know whether to send the
request to Grafana, Backstage, or ArgoCD.

### Full Request Flow

```
Your Browser (local laptop)
        │
        │  GET http://grafana.35.82.130.149.nip.io/
        │
        ▼
┌───────────────────┐
│   Public DNS      │   nip.io nameserver answers:
│   (nip.io)        │   grafana.35.82.130.149.nip.io → 35.82.130.149
└────────┬──────────┘
         │
         │  TCP :80  →  35.82.130.149
         ▼
┌─────────────────────────────────────────────────────────────┐
│  AWS — us-west-2                                            │
│                                                             │
│  ┌──────────────────────────────────────────────────────┐  │
│  │  Network Load Balancer (NLB)                         │  │
│  │  pel-nlb-dev-e33ba6aef58c79e5.elb.us-west-2...       │  │
│  │  Public IP: 35.82.130.149  (+ 54.203.x.x, 35.167.x) │  │
│  └──────────────────┬───────────────────────────────────┘  │
│                     │  forwards to NodePort 31237           │
│                     ▼                                       │
│  ┌──────────────────────────────────────────────────────┐  │
│  │  EKS — pel-eks-dev                                   │  │
│  │                                                      │  │
│  │  ┌────────────────────────────────────────────────┐  │  │
│  │  │  ingress-nginx (ns: platform-system)           │  │  │
│  │  │                                                │  │  │
│  │  │  reads Host: header from HTTP request          │  │  │
│  │  │  "grafana.35.82.130.149.nip.io"                │  │  │
│  │  │        │                                       │  │  │
│  │  │        ├─ grafana.*      → Grafana svc :80     │  │  │
│  │  │        ├─ prometheus.*   → Prometheus svc :9090│  │  │
│  │  │        ├─ alertmanager.* → Alertmanager :9093  │  │  │
│  │  │        ├─ argocd.*       → ArgoCD svc :80      │  │  │
│  │  │        ├─ opencost.*     → OpenCost svc :9090  │  │  │
│  │  │        ├─ chaos.*        → Chaos Dashboard:2333│  │  │
│  │  │        └─ backstage.*    → Backstage svc :7007 │  │  │
│  │  └────────────────────────────────────────────────┘  │  │
│  └──────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────┘
```

### Why 37.27.97.75 Is NOT in the Picture

The Linux server at `37.27.97.75` (where you remote-desktop to) is **only used
for running kubectl, git, and Claude Code**. It is not in the data path for UI
traffic at all.

```
Browser request  ──►  NLB (35.82.130.149)  ──►  EKS pods
                                                  (no 37.27.97.75 involved)
```

Your browser connects directly from your laptop to AWS. The remote desktop is only
for operating the cluster — not for serving traffic.

### Why Not Port-Forward?

`kubectl port-forward` would require:

```
Browser → 37.27.97.75:3000 → tunnel through kubectl → Grafana pod
```

That means:
1. The tunnel runs on 37.27.97.75 (the remote server)
2. Your browser must reach `37.27.97.75:3000` — requires SSH tunnel or firewall rule
3. Breaks every time the connection drops

With nip.io ingress there is no tunnel. The path is direct and always-on.

### If the NLB IP Changes After Re-Apply

```bash
# Get new IPs
dig +short pel-nlb-dev-e33ba6aef58c79e5.elb.us-west-2.amazonaws.com | head -1

# Replace everywhere
OLD_IP="35.82.130.149"
NEW_IP="<new-ip>"
grep -rl "$OLD_IP" . --include="*.yaml" --include="*.md" \
  | xargs sed -i "s/$OLD_IP/$NEW_IP/g"
```

---

## Tool: `freeze` (Charm)

Installed at `~/.local/share/mise/installs/go/1.23.4/bin/freeze`.
Produces styled PNG/SVG from terminal command output.

### Basic syntax

```bash
freeze --execute "<command>" \
  --window --theme dracula \
  -o <output-path>.png
```

### Common flags

| Flag | Purpose |
|---|---|
| `--window` | Add macOS-style window chrome |
| `--theme dracula` | Dark theme (also: `monokai`, `github-dark`, `nord`) |
| `--width 1200` | Fix output width in px |
| `--padding 20` | Inner padding |
| `-o file.png` | Output path (`.png`, `.svg`, `.webp` all supported) |

---

## Naming convention

Files live under:
```
_project-docs/portfolio/screenshots/
  phase-1/sprint-XX-name/NN-description.png
  phase-2/sprint-XX-name/NN-description.png
  phase-3/sprint-XX-name/NN-description.png
```

`NN` = two-digit sequence within the sprint (01, 02, ...).

---

## Phase 1 — CLI captures

```bash
# Nodes
freeze --execute "kubectl get nodes -o wide" \
  --window --theme dracula \
  -o _project-docs/portfolio/screenshots/phase-1/sprint-03-eks/02-nodes-m6i-xlarge.png

# All ArgoCD apps
freeze --execute "kubectl get applications -n argocd --sort-by=.metadata.name" \
  --window --theme dracula \
  -o _project-docs/portfolio/screenshots/phase-1/sprint-04-cluster-bootstrap/07-all-apps-healthy.png

# Ingress resources
freeze --execute "kubectl get ingress -A" \
  --window --theme dracula \
  -o _project-docs/portfolio/screenshots/phase-1/sprint-05-gitops/01-argocd-ingress.png

# Observability pods
freeze --execute "kubectl get pods -n observability" \
  --window --theme dracula \
  -o _project-docs/portfolio/screenshots/phase-1/sprint-06-observability/02-obs-pods.png

# Kyverno policies
freeze --execute "kubectl get clusterpolicies" \
  --window --theme dracula \
  -o _project-docs/portfolio/screenshots/phase-1/sprint-07-security/06-cluster-policies.png

# TF state (what was created)
freeze --execute "cd infrastructure/phase-1-mvp/envs/dev && terraform state list" \
  --window --theme dracula \
  -o _project-docs/portfolio/screenshots/phase-1/sprint-02-terraform/02-tf-state-list.png
```

---

## Phase 2 — CLI captures

```bash
# Sprint 10 — Tempo on S3
freeze --execute "kubectl get pods -n observability -l app.kubernetes.io/name=tempo && aws s3 ls s3://pel-tempo-<AWS_ACCOUNT_ID>-dev/ --region us-west-2" \
  --window --theme dracula \
  -o _project-docs/portfolio/screenshots/phase-2/sprint-10-tracing/01-tempo-s3-running.png

# Sprint 11 — SLOs
freeze --execute "kubectl get pods -n observability -l app.kubernetes.io/name=sloth" \
  --window --theme dracula \
  -o _project-docs/portfolio/screenshots/phase-2/sprint-11-slos/01-sloth-slos.png

# Sprint 12 — Velero BSL
freeze --execute "kubectl get backupstoragelocations -n velero && kubectl get pods -n velero" \
  --window --theme dracula \
  -o _project-docs/portfolio/screenshots/phase-2/sprint-12-velero/01-velero-bsl-available.png

# Sprint 13 — Chaos Mesh
freeze --execute "kubectl get pods -n chaos-mesh" \
  --window --theme dracula \
  -o _project-docs/portfolio/screenshots/phase-2/sprint-13-chaos/01-chaos-mesh-pods.png

# Sprint 14 — OpenCost
freeze --execute "kubectl exec -n finops deployment/opencost -c opencost -- wget -qO- 'http://localhost:9003/allocation?window=1d&aggregate=namespace' | python3 -m json.tool | grep -E 'name|totalCost' | head -20" \
  --window --theme dracula \
  -o _project-docs/portfolio/screenshots/phase-2/sprint-14-opencost/01-opencost-namespace-cost.png

# Sprint 16 — Cosign
freeze --execute "cosign verify --certificate-identity-regexp 'https://github.com/mirdattamir/.*' --certificate-oidc-issuer 'https://token.actions.githubusercontent.com' <IMAGE>" \
  --window --theme dracula \
  -o _project-docs/portfolio/screenshots/phase-2/sprint-16-cosign/02-cosign-verify.png

# Sprint 17 — Falco
freeze --execute "kubectl get pods -n falco && kubectl get daemonset -n falco" \
  --window --theme dracula \
  -o _project-docs/portfolio/screenshots/phase-2/sprint-17-falco/01-falco-pods.png

# Sprint 19 — ARC runners
freeze --execute "kubectl get pods -n arc-systems" \
  --window --theme dracula \
  -o _project-docs/portfolio/screenshots/phase-2/sprint-19-arc-runners/01-arc-runners.png
```

---

## UI Screenshots — direct browser URLs (no port-forward)

> **NLB IP:** `35.82.130.149` — open these in the browser on your local machine.
> If the IP changes after re-apply, run:
> ```bash
> dig +short pel-nlb-dev-e33ba6aef58c79e5.elb.us-west-2.amazonaws.com | head -1
> ```
> Then: `grep -rl "35.82.130.149" . --include="*.yaml" --include="*.md" | xargs sed -i "s/35.82.130.149/<new-ip>/g"`

### Browser screenshot shortcut (Linux / Windows)
- **Region select:** `Shift + PrtScr` (Linux) or `Win + Shift + S` (Windows) ← best for portfolio
- **Full screen:** `PrtScr`
- **Active window:** `Alt + PrtScr`

---

### Credentials — all services

| Service | URL | Username | Password / Token | Notes |
|---|---|---|---|---|
| **ArgoCD** | `http://argocd.35.82.130.149.nip.io` | `admin` | `7T7D8ivzAfiIQ3TM` | Rotates on redeploy — re-run cmd below |
| **Grafana** | `http://grafana.35.82.130.149.nip.io` | `admin` | `changeme-use-eso-in-prod` | Set in values-dev.yaml |
| **Prometheus** | `http://prometheus.35.82.130.149.nip.io` | — | no login | Open access |
| **Alertmanager** | `http://alertmanager.35.82.130.149.nip.io` | — | no login | Open access |
| **OpenCost** | `http://opencost.35.82.130.149.nip.io` | — | no login | Open access |
| **Chaos Mesh** | `http://chaos.35.82.130.149.nip.io` | — | token (see below) | RBAC mode |
| **Backstage** | `http://backstage.35.82.130.149.nip.io` | — | click **Enter as Guest** | Guest auth enabled |

**Get current ArgoCD password (changes on each fresh install):**
```bash
kubectl get secret argocd-initial-admin-secret -n argocd \
  -o jsonpath='{.data.password}' | base64 -d && echo
```

**Chaos Mesh token** (viewer, read-only — valid until cluster teardown):
```bash
# Get token:
kubectl get secret chaos-viewer-token -n chaos-mesh \
  -o jsonpath='{.data.token}' | base64 -d && echo

# Token as of 2026-05-17:
# eyJhbGciOiJSUzI1NiIsImtpZCI6Ikd3U1Y3UlRFWjlOYmpS...
# (paste full token into the Chaos Mesh login screen)
```

---

### Phase 1 — UI Screenshots

#### ArgoCD — `phase-1/sprint-05-gitops/02-argocd-ui.png`
1. Open `http://argocd.35.82.130.149.nip.io`
2. Login: `admin` / `7T7D8ivzAfiIQ3TM`
3. Click **Applications** in left sidebar
4. All apps should show green (Synced / Healthy)
5. `Shift+PrtScr` → select full browser window → save

#### Grafana — Cluster Overview — `phase-1/sprint-06-observability/03-grafana-cluster.png`
1. Open `http://grafana.35.82.130.149.nip.io`
2. Login: `admin` / `changeme-use-eso-in-prod`
3. Left sidebar → **Dashboards**
4. Click **Kubernetes / Compute Resources / Cluster**
5. Time range (top-right): **Last 1 hour**
6. Screenshot the panel grid

#### Grafana — Node Exporter — `phase-1/sprint-06-observability/04-grafana-nodes.png`
1. Dashboards → search **"node exporter"** → open **Node Exporter Full**
2. Screenshot

#### Alertmanager — `phase-1/sprint-06-observability/05-alertmanager.png`
1. Open `http://alertmanager.35.82.130.149.nip.io`
2. Screenshot the Alerts or Status page

#### Prometheus — `phase-1/sprint-06-observability/06-prometheus-ui.png`
1. Open `http://prometheus.35.82.130.149.nip.io`
2. Run query: `up` → click **Execute**
3. Screenshot the table of targets

---

### Phase 2 — UI Screenshots

#### Grafana → Tempo traces — `phase-2/sprint-10-tracing/02-grafana-tempo.png`
1. Open `http://grafana.35.82.130.149.nip.io`
2. Left sidebar → **Explore** (compass icon)
3. Datasource dropdown (top-left) → select **Tempo**
4. Click **Run query** (leave filter blank)
5. Click into one trace → screenshot the span waterfall

#### Grafana → SLO Overview — `phase-2/sprint-11-slos/03-slo-dashboard.png`
1. Left sidebar → **Dashboards**
2. Search **"SLO"** → open **SLO Overview**
3. Time range: **Last 6 hours**
4. Screenshot showing availability + latency panels and burn-rate graphs
> Dashboard added via ConfigMap `grafana-dashboard-slo-overview` in ns `observability`

#### Chaos Mesh — `phase-2/sprint-13-chaos/03-chaos-mesh-ui.png`
1. Open `http://chaos.35.82.130.149.nip.io`
2. At login screen select **Token** mode
3. Paste the token from `kubectl get secret chaos-viewer-token -n chaos-mesh -o jsonpath='{.data.token}' | base64 -d`
4. Screenshot the **Dashboard** or **Experiments** page

#### OpenCost — `phase-2/sprint-14-opencost/03-opencost-ui.png`
1. Open `http://opencost.35.82.130.149.nip.io`
2. Click **Allocations** in left nav
3. Set **Aggregate by: Namespace**, window **Last 7 days**
4. Screenshot showing cost per namespace

#### Grafana → Falco Alerts — `phase-2/sprint-17-falco/02-falco-alerts.png`
1. Open `http://grafana.35.82.130.149.nip.io`
2. Left sidebar → **Alerting** → **Alert rules**
3. Search box: type **falco**
4. Screenshot the matching alert rules

---

### Phase 3 — Backstage UI Screenshots

> Backstage loads in ~10–15s on first hit. If blank, wait and refresh once.

#### Home page — `phase-3/sprint-20-backstage/02-backstage-home.png`
1. Open `http://backstage.35.82.130.149.nip.io`
2. Click **Enter as Guest**
3. Screenshot the home page (Platform Engineering Lab title)

#### Software Catalog — `phase-3/sprint-21-catalog/03-catalog-browser.png`
1. Navigate to `http://backstage.35.82.130.149.nip.io/catalog`
2. Screenshot showing list of components

#### Component Entity page — `phase-3/sprint-21-catalog/04-component-entity.png`
1. In catalog, click any component (e.g. **example-app**)
2. Screenshot the entity overview page (shows owner, links, relations)

#### TechDocs — `phase-3/sprint-22-techdocs/03-techdocs-page.png`
1. Navigate to `http://backstage.35.82.130.149.nip.io/docs`
2. Click any doc entry
3. Screenshot the rendered documentation

#### Scaffolder templates — `phase-3/sprint-23-go-template/02-scaffolder-ui.png`
1. Navigate to `http://backstage.35.82.130.149.nip.io/create`
2. Screenshot showing all template cards

#### Go Service template form — `phase-3/sprint-23-go-template/03-go-template-form.png`
1. Click **Go Service** template → **Choose**
2. Screenshot step 1 of the form

#### Team Onboarding form — `phase-3/sprint-28-team-onboarding/02-onboarding-form.png`
1. Back to `/create` → click **Team Onboarding** → **Choose**
2. Screenshot step 1
| Scaffolder templates | `http://backstage.35.82.130.149.nip.io/create` | Guest | `phase-3/sprint-23-go-template/02-scaffolder-ui.png` |
| Go template form | Click "Go Service" template → fill step 1 | Guest | `phase-3/sprint-23-go-template/03-go-template-form.png` |
| Team onboarding form | Click "Team Onboarding" template | Guest | `phase-3/sprint-28-team-onboarding/02-onboarding-form.png` |

### CLI capture of Backstage pods
```bash
freeze --execute "kubectl get pods -n backstage && kubectl get ingress -n backstage" \
  --window --theme dracula \
  -o _project-docs/portfolio/screenshots/phase-3/sprint-20-backstage/01-backstage-running.png
```

---

## Phase 4 — Agentic Layer CLI captures

```bash
# Sprint 33 — Agent file tree
freeze --execute "find agents/langgraph -type f -name '*.py' | sort" \
  --window --theme dracula \
  -o _project-docs/portfolio/screenshots/phase-4/sprint-33-foundation/01-agent-tree.png

# Sprint 33 — TF modules
freeze --execute "find infrastructure/phase-4-agentic -type f | sort" \
  --window --theme dracula \
  -o _project-docs/portfolio/screenshots/phase-4/sprint-33-foundation/02-tf-modules.png

# Sprint 34 — Intent parser tests passing
freeze --execute "cd agents/langgraph && pytest agents/intent_parser/tests/ -v --tb=short 2>&1 | tail -20" \
  --window --theme dracula \
  -o _project-docs/portfolio/screenshots/phase-4/sprint-34-intent-parser/01-tests-passing.png

# Sprint 33 — Orchestrator pod running (once deployed)
freeze --execute "kubectl get pods -n agents && kubectl get svc -n agents" \
  --window --theme dracula \
  -o _project-docs/portfolio/screenshots/phase-4/sprint-33-foundation/04-orchestrator-pod.png

# Sprint 33 — Agent run smoke test
freeze --execute "curl -s -XPOST http://localhost:8080/run -H 'Content-Type: application/json' -d '{\"nl_request\": \"Create a dev EKS cluster\", \"env\": \"dev\"}' | python3 -m json.tool" \
  --window --theme dracula \
  -o _project-docs/portfolio/screenshots/phase-4/sprint-33-foundation/05-smoke-run.png
```

---

## Refresh all at once

Run the capture script:
```bash
bash scripts/capture/capture-all-screenshots.sh
```
(Script to be created — use commands above as the basis.)
