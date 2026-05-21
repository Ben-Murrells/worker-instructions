# Codex Worker Instructions

Central instructions for Codex agents to work across Frank’s infrastructure.

## Setup

1. Install CLI tools on machine:
   - macOS: `brew install gh vercel @openai/codex`
   - Windows: `winget install GitHub.cli Vercel.openai.codex`

2. Authenticate:
   ```bash
   gh auth login
   vercel login
   wrangler whoami  # Cloudflare CLI
   ```

3. Clone this repo and project repos:
   ```bash
   gh repo clone Ben-Murrells/worker-instructions
   gh repo clone Ben-Murrells/<project-name>
   cd <project-name>
   ```

## Infrastructure Access

Codex agents have access to:

### GitHub

**Orgs:**
- `Ben-Murrells` — primary org
- `FC-Life` — Vera/coaching repos
- `HospitalityOwner-ai` — HospitalityOwner website

**Permissions:**
- Create branches
- Open PRs (PR-only workflow)
- Merge after approval (Frank only)
- Run GitHub Actions

**Guardrails:**
- Never delete branches/refs without approval
- Pin to production branches only with review

### Vercel

**Projects:**
- `brain-app` — Frank’s brain / Mission Control
- `ben-4106` — benmurrells.com
- `hospitality-owner` — hospitalityowner.ai
- `vera` — FC Knowledge

**Permissions:**
- Deploy branches
- Create preview deployments
- Update environment variables (read-only, except dev vars)

**Guardrails:**
- No delete production deployments
- No billing changes
- Preview-only for unreviewed work

### Cloudflare

**Domains:**
- `benmurrells.com`
- `foodiecoaches.com`
- `hospitalityowner.ai`
- `offtapwatch.com`

**Permissions:**
- Update DNS records
- Deploy Workers (if using Cloudflare Pages/Workers)

**Guardrails:**
- No delete zones
- No SSL/TLS changes without review
- No paid plan upgrades

## Workflow Principles

1. **Every change gets a branch** — never commit directly to `main`
2. **PR-only merge** — Frank reviews and merges
3. **Read INFRA.md first** — understand which projects/accounts apply
4. **Test locally** — run checks before opening PR
5. **Deploy after merge** — Frank handles production deployments

## Project Context

Each project repo should have its own `INFRA.md` that specifies:
- Which GitHub repo
- Which Vercel project
- Which Cloudflare domain
- Any other services (DBs, API keys, etc.)

## Security

- Never hardcode API keys in code
- Use environment variables
- Rotate credentials quarterly
- Log all sensitive access in `ops/audit.json`

## Emergency Access

For urgent hotfixes:
1. Create branch `hotfix/immediate-<issue>`
2. Deploy via Vercel CLI directly (bypass PR)
3. Create follow-up PR within 24h
