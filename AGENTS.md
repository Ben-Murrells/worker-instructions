# AGENTS.md — Worker Instructions

This is the shared instruction set for all Codex agents working across Frank’s infrastructure.

## Platform

- **Name:** Mac-Frank (Frank on Mac Mini)
- **Role:** Operator/PM, not coder
- **Mission:** Direct Codex agents, review PRs, merge after approval

## Codex Agents

- **Platform:** Ben’s iMac (macOS) or PC (Windows)
- **Role:** Coding worker under Frank’s direction
- **Mission:** Build, fix, refactor — always via PRs

## Workspace Management

- GitHub is source of truth
- `Ben-Murrells` is primary org (all current projects)
- Each machine clones repos into local workspace
- No mirroring — agents access live repos directly via CLI

## Workflow

1. **Frank assigns task** — via PR description, issue, or `WORKING.md`
2. **Codex creates branch** — `codex/<short-description>`
3. **Codex codes** — follows project `INFRA.md` rules
4. **Codex tests/lints** — `npm test && npm run lint`
5. **Codex pushes + opens PR** — `gh pr create`
6. **Frank reviews** — checks code, tests, infrastructure guardrails
7. **Frank merges** — only after approval

## Security

- Never hardcode secrets — use `process.env`
- Rotate credentials quarterly
- Log sensitive access in `ops/audit.json`
- No direct commits to `main` — PR-only

## Infrastructure Access

See `INFRA.md` for detailed access control:
- GitHub: `Ben-Murrells`, `FC-Life`, `HospitalityOwner-ai`
- Vercel: projects under `ben-4106`, `brain-app`, `vera`, `hospitality-owner`
- Cloudflare: domains `benmurrells.com`, `foodiecoaches.com`, etc.

## Current Tasks

See `WORKING.md` for current priorities.

## Emergency

Hotfixes:
- Branch: `hotfix/immediate-<issue>`
- Deploy direct CLI (bypass PR)
- Follow up with PR within 24h
