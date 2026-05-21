# Infrastructure Access for Codex Agents

## GitHub Accounts

**Primary:** `ben@benmurrells.com` (Business ChatGPT → Personal Max migration TBD)

**Orgs:**
- `Ben-Murrells` — primary, all current projects
- `FC-Life` — Vera/coaching
- `HospitalityOwner-ai` — HospitalityOwner

**CLI Setup:**
```bash
gh auth login --scopes repo,workflow
gh config host set github.com
```

**Permissions:**
- ✅ Create branches
- ✅ Push to feature branches
- ✅ Open PRs
- ✅ Comment on PRs
- ✅ Run GitHub Actions
- ❌ Delete branches (requires approval)
- ❌ Merge `main` (Frank only)
- ❌ Access private repos outside orgs

---

## Vercel Accounts

**Primary Project:** `ben-4106` (benmurrells.com)
**Other Projects:**
- `brain-app` (Frank’s brain)
- `hospitality-owner`
- `vera`

**CLI Setup:**
```bash
vercel login
vercel link --project ben-4106
```

**Permissions:**
- ✅ Deploy branches
- ✅ Create preview deployments
- ✅ View environment variables (read-only)
- ❌ Delete production deployments
- ❌ Modify billing
- ❌ Transfer projects

---

## Cloudflare Accounts

**Domains:**
- `benmurrells.com`
- `foodiecoaches.com`
- `hospitalityowner.ai`
- `offtapwatch.com`

**CLI Setup:**
```bash
wrangler login
```

**Permissions:**
- ✅ Update DNS records (A, CNAME, TXT, MX, etc.)
- ✅ Deploy Workers (preview/prod branches)
- ✅ View analytics
- ❌ Delete zones
- ❌ Modify SSL/TLS settings
- ❌ Upgrade to_paid plans

---

## Other Services

### GitHub Actions
- CI/CD pipelines run on every PR
- Frank reviews actions output before merge

### Neon Postgres
- Dev DB: `dev-<project>` (Codex can modify schema)
- Prod DB: `prod-<project>` (Frank only)

### OpenAI/Codex API
- Use `openai-codex/gpt-5.5` OAuth token
- No raw API key usage in production

---

## Guardrails Summary

- **Never delete anything** (branches, deploys, zones) without approval
- **No billing changes** under any circumstances
- **Production merges only after Frank review**
- **Preview deployments allowed** for testing
- **Log all sensitive actions** in `ops/audit.json`

---

## Emergency Access

For urgent hotfixes:
1. Create `hotfix/immediate-<issue>` branch
2. Deploy direct via CLI (bypass PR)
3. Follow up with PR within 24h
