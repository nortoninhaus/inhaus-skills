---
name: inhaus-kanban
version: 1.0
description: Multi-profile kanban routing conventions, skill inventory, cross-profile work patterns for Inhaus team.
author: Nico (brian)
tags: [kanban, routing, team]
---

# Inhaus Team Kanban Skill

Loaded by any profile that needs to understand multi-agent routing conventions.

## Profiles & Ownership

| Profile | Role | Model |
|---------|------|-------|
| brian | CoS / orchestration | deepseek-v4-flash-0731 |
| marketing-ads | Growth media strategy | deepseek-v4-flash-0731 |
| weaver | AI product engineer | qwen3.7-plus |
| insight | Analyst | deepseek-v4-pro-0813 |
| atlas | Research/intel + deploy | deepseek-v4-flash-0731 |
| domo | Creative director | qwen3.7-plus |
| forge | Full-stack engineering | deepseek-v4-pro-0813 |
| harbor | Client delivery mgmt | deepseek/v4-pro-0813 |
| pulse | Live media ops | deepseek-v4-flash-0731 |
| sentinel | Systems ops | deepseek-v4-flash-0731 |
| compliance | Legal/regulatory risk | deepseek-v4-flash-0731 |
| content | Long-form/repurposing | qwen3.7-plus |
| finance | Budget/revenue control | qwen3.7-plus |
| antigravity | Google Antigravity (agy CLI) operator — drives the agent harness for coding features, refactors, reviews, batch fixes | deepseek-v4-flash-0731 |

## Coding / agent-harness profiles — coordination

The engineering stack is split by interface, not by project:

| Profile | Interface | Route to it when... |
|---------|-----------|---------------------|
| `forge` | Direct Hermes code execution | Building web apps, dashboards, Flutter, backend APIs, DB schemas in-session |
| `weaver` | Direct Hermes code execution | Inhaus Brain / BrainWeave / PicoClaw / SkillWeave and related Flutter apps |
| `antigravity` | Google Antigravity CLI (`agy`) | A task needs Antigravity's agent harness (its `--print`/`--sandbox`/`--dangerously-skip-permissions` modes) — features, refactors, reviews, batch fixes. Operates in a git repo only. |

All three code in git repos, verify diffs/tests before reporting done, and never commit/push/merge without sign-off. They read the same kanban board; use `--assignee` to pick the interface for the task.

## Routing Rules

Cards assigned via --assignee <profile>; gateway auto-dispatches. When unsure who owns something, ask brian. Never assign a task that conflicts with another profile's ownership.

## Sub-Agents

verifier (QA), compliance-reviewer (legal check), data-backfiller (metric fetch), release-manager (merge gate).
