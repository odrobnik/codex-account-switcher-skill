# codex-account-switcher

Manage multiple OpenAI Codex accounts by saving, switching, comparing, and optionally syncing authentication tokens into OpenClaw.

⚠️ **Sensitive:** This skill reads and writes `~/.codex/auth.json`, `~/.codex/accounts/*.json`, and can explicitly sync credentials into `~/.openclaw/agents/*/agent/auth-profiles.json` / `auth.json`.

## ClawHub

Published on [ClawHub](https://clawhub.com/skills/codex-account-switcher).

## Usage

See [SKILL.md](SKILL.md) for full documentation.

```bash
./codex-accounts.py list          # List saved accounts
./codex-accounts.py add           # Add a new account (interactive)
./codex-accounts.py use <name>    # Switch to an account
./codex-accounts.py auto          # Switch to account with best quota
./codex-accounts.py sync          # Explicitly sync saved accounts into OpenClaw
./codex-accounts.py sync --dry-run
```

## Documentation

- [SKILL.md](SKILL.md) — agent-facing reference (commands, behavior, limitations)
- [SETUP.md](SETUP.md) — prerequisites, configuration, and setup instructions
- [ClawHub](https://www.clawhub.com/skills/codex-account-switcher) — install via ClawHub registry

## License

MIT
