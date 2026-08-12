---
name: agy-cli
description: "Use when controlling Google Antigravity CLI (agy)."
version: 1.0.0
author: Brian + Hermes Agent
license: MIT
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [coding-agent, CLI, google-antigravity]
    related_skills: [codex, claude-code, opencode]
---

# AGY CLI — Usage Reference

## Prerequisites

- Binary at `/opt/homebrew/bin/agy`
- Auth via system keyring / Google Sign-In
- Git repo required — Antigravity refuses outside one

## Core Commands

| Command | Purpose |
|---------|---------|
| `agy <prompt>` | Interactive TUI chat |
| `agy --print "<prompt>"` | Non-interactive, print response, exit |
| `agy --continue` | Continue most recent conversation (interactive) |
| `agy --conversation <id>` | Resume by ID |
| `agy models` | List available models |
| `agy update` | Update binary |

## Flags

| Flag | Effect |
|------|--------|
| `--print` / `-p` | Single prompt, non-interactive, prints result |
| `--print-timeout N` | Timeout for print mode (default 5m) |
| `--dangerously-skip-permissions` | Auto-approve all tool prompts |
| `--sandbox` | Terminal restrictions enabled |
| `--model <label>` | Override model selection |
| `-c` | Alias for `--continue` |

## When to Use

Load this skill whenever you need to delegate coding or agentic tasks to Google Antigravity through its CLI. Use it in the antigravity profile for features, refactors, reviews, and batch fixes.

## Patterns

### One-shot task
```bash
agy --print "Refactor utils/auth.js to use token-based auth. Only modify that file."
```

### Longer work with continuation
```bash
agy --print "Start building the dashboard page structure..."
agy --print "Continue implementing the sidebar nav..." --continue
```

### Sandbox mode (recommended for autonomous work)
```bash
agy --sandbox --print "Fix the login form validation in src/components/Login.tsx"
```

### Dangerous auto-approval (only when explicitly requested)
```bash
agy --dangerously-skip-permissions --print "Apply changes across the codebase..."
```

## Model Selection

```bash
agy --print "Build X" --model "Gemini 3.6 Flash (High)"
```

## Common Pitfalls

1. **No git repo = no execution** — always `cd $(mktemp -d) && git init` for scratch
2. **`agy models` can hang** on network/auth; prefer `--print` which handles auth inline
3. **Stdout capture fails in background shell** — transcript stored in:
   `~/.gemini/antigravity-cli/brain/<conv-id>/.system_generated/logs/transcript_full.jsonl`
4. **Concurrent sessions conflict** — serialize with `flock ~/.agy.lock`
5. **Settings persist** in `~/.gemini/antigravity-cli/settings.json`; edit via `/config` or directly

## Verification Checklist

After each agy task:
- [ ] Diff files changed (`git diff --stat`)
- [ ] Tests pass
- [ ] No secrets leaked
- [ ] Output matches expected behavior
