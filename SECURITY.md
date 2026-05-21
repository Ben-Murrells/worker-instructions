# Security & Access Control

GitHub Personal Access Token (PAT) Setup for Codex Agents

## How to Get Your PAT

1. Go to https://github.com/settings/tokens
2. Click "Personal access tokens (classic)" → "Generate new token (classic)"
3. Name: `codex-worker`
4. Choose expiration: 90 days (or auto-expire)
5. **Select scopes:**
   - `repo` — full control of private repos (required for PR workflows)
   - `workflow` — allow GitHub Actions (if needed)
   - `read:org` — read org membership (optional, for some CLI tools)
6. Generate token
7. **Copy the token** — it starts with `gho_xxxxxx` or `github_pat_xxxxxx`

## Storing Your Token

**On iMac (macOS):**
```bash
# Add to shell startup (e.g., ~/.zshrc or ~/.bash_profile)
export GITHUB_TOKEN="gho_xxxxxx_yourtokenhere"

# Reload shell
source ~/.zshrc
```

**On PC (Windows PowerShell):**
```powershell
# Add to profile
$env:GITHUB_TOKEN = "gho_xxxxxx_yourtokenhere"

# Save to profile file
echo '$env:GITHUB_TOKEN = "gho_xxxxxx_yourtokenhere"' >> $PROFILE

# Reload shell
. $PROFILE
```

## Verifying Token

```bash
gh auth status
```

You should see:
- `github.com: logged in as ben@benmurrells.com`
- ✓ Authentication successful

## Using Token in Codex

Codex agents will automatically pick up `GITHUB_TOKEN` environment variable.

If not set, run:
```bash
export GITHUB_TOKEN="your-token-here"
```

## Security Notes

- **Never commit tokens to GitHub** — they’re in `.env` files
- **Rotate every 90 days** — create a new PAT and update `.zshrc` / `$PROFILE`
- **Revoke if lost** — delete the old token from GitHub settings
- **Only Codex needs this** — don’t share it with other humans

## Emergency Revocation

If you suspect a leak:
1. Go to https://github.com/settings/tokens
2. Find `codex-worker` token
3. Click "Revoke"
4. Generate a new one and update `GITHUB_TOKEN`
