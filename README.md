# .openclaw

Local state and workspace for OpenClaw.

This directory stores OpenClaw runtime configuration, agent workspaces, sessions, logs, channel credentials, and local automation assets.

## What This Repository Contains

- OpenClaw config and runtime state (`openclaw.json`, backups, update metadata)
- Agent data and per-agent session history (`agents/`)
- CLI shell completions for multiple shells (`completions/`)
- Channel/device credential and pairing metadata (`credentials/`, `devices/`, `identity/`)
- Scheduled automation job definitions (`cron/jobs.json`)
- Local logs and audits (`logs/`)
- The primary agent workspace and skills (`workspace/`)

## Directory Layout

```text
.openclaw/
├── openclaw.json              # Main OpenClaw configuration
├── agents/                    # Agent profiles and conversation sessions
├── completions/               # Bash/Fish/PowerShell/Zsh completion scripts
├── credentials/               # Channel and integration credentials
├── cron/                      # Scheduled job definitions
├── devices/                   # Paired and pending device records
├── identity/                  # Local device identity and auth material
├── logs/                      # Runtime and audit logs
└── workspace/                 # Agent workspace docs, memory, and local skills
```

## Typical Workflow

1. Configure or update the local setup:

```bash
openclaw configure
```

2. Validate health and common misconfigurations:

```bash
openclaw doctor
```

3. Inspect overall system status:

```bash
openclaw status
```

4. Open the local dashboard:

```bash
openclaw dashboard
```

## Workspace Conventions

- `workspace/AGENTS.md` defines startup and behavior rules for the local agent workspace.
- `workspace/skills/` contains local skills and orchestration scripts.
- `agents/main/sessions/` stores conversation transcripts and reset snapshots.

## Security Notes

- This folder may contain secrets (tokens, API keys, auth material, and session logs).
- Avoid committing sensitive state to source control.
- Rotate credentials immediately if any sensitive file has been exposed.

## Secrets Best Practice

This repo keeps `openclaw.json` tracked, but stores secrets in `.env` and references them from config.

- Real secrets: `.env` (ignored by git)
- Template: `.env.example` (safe to commit)
- Config references use env-backed values (for example `${SLACK_BOT_TOKEN}`) and OpenClaw SecretRef objects.

Recommended maintenance flow:

```bash
openclaw secrets audit --check
openclaw secrets configure
openclaw secrets reload
```

## Backups

Create and verify local backups before major changes:

```bash
openclaw backup create --verify
```
