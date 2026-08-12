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

## Routing Rules

Cards assigned via --assignee <profile>; gateway auto-dispatches. When unsure who owns something, ask brian. Never assign a task that conflicts with another profile's ownership.

## Sub-Agents

verifier (QA), compliance-reviewer (legal check), data-backfiller (metric fetch), release-manager (merge gate).
