---
name: codex-account-switcher
version: 1.3.0
homepage: https://github.com/odrobnik/codex-account-switcher-skill
description: >
  Manage multiple OpenAI Codex accounts. Capture current login tokens and switch
  between them instantly. Syncs tokens to all OpenClaw agent auth-profiles using
  email-based profile keys. ⚠️ Reads and writes ~/.codex/auth.json and
  ~/.codex/accounts/*.json (sensitive authentication tokens).
metadata:
  openclaw:
    emoji: "🎭"
    requires:
      bins: ["python3"]
    configPaths:
      - "~/.codex/auth.json"
      - "~/.codex/accounts/"
      - "~/.openclaw/agents/*/agent/auth-profiles.json"
---

# Codex Account Switcher

Manage multiple OpenAI Codex identities (e.g. personal vs. work) by swapping the authentication token file.

## Usage

### 1. List Accounts
Show saved accounts (active one is marked). Default output is compact.

- `--verbose` includes refresh age + token TTL (debug)
- `--json` outputs the verbose info as JSON
```bash
python3 {baseDir}/scripts/codex-accounts.py list
python3 {baseDir}/scripts/codex-accounts.py list --verbose
```

### 2. Add an Account
Interactive wizard to capture login(s).

- **Always starts a fresh browser login** (`codex logout && codex login`) so you explicitly choose the identity to capture.
- After each login it saves a snapshot.
- In an interactive terminal it asks if you want to add another.
- When invoked non-interactively, it runs **single-shot** (no "add another" prompt).
- When naming an account, **press Enter** to accept the default name (local-part of the detected email, e.g. `oliver` from `oliver@…`).

```bash
python3 {baseDir}/scripts/codex-accounts.py add
```

### 3. Switch Account
Instantly swap the active login. Syncs the token to all OpenClaw agents' `auth-profiles.json`.
```bash
python3 {baseDir}/scripts/codex-accounts.py use oliver
```

### 4. Auto-Switch to Best Quota
Check all accounts and switch to the one with most weekly quota available.
```bash
python3 {baseDir}/scripts/codex-accounts.py auto
python3 {baseDir}/scripts/codex-accounts.py auto --json
```

### 5. Sync All Profiles
Ensure every saved Codex snapshot is mirrored to OpenClaw auth-profiles.
```bash
python3 {baseDir}/scripts/codex-accounts.py sync
```

## OpenClaw Integration

On every account switch, the script:
1. Updates `~/.codex/auth.json` with the selected account's token
2. Syncs the token to **all** OpenClaw agents' `auth-profiles.json` (main, leon, etc.)
3. Profile keys use the account email: `openai-codex:oliver@drobnik.com`
4. Migrates old name-based keys (`openai-codex:oliver`) to email-based keys
5. Logs the switch to `~/.codex/account-activity.jsonl` for quota attribution

## Setup

See [SETUP.md](SETUP.md) for prerequisites and setup instructions.
