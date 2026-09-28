---
name: mengto-workflow
description: Use for agent workflow/ship discipline (progress screenshots, scoring to target, shipping a change, manager threads). Load before reporting progress or shipping web/creative work.
version: 1.0.0
author: Inhaus Corp
license: MIT
platforms: [macos, linux]
metadata:
  hermes:
    tags: [workflow, ship, progress, screenshots, threads, qa]
---

# MengTo Workflow Skills

Four playbooks on agent work discipline: `workflow-progress-screenshots`,
`workflow-score-to-target`, `workflow-ship-change`, `workflow-threads-manager`.

Source: https://github.com/MengTo/Skills/tree/main/agent-skills/workflow

## When to use

- Reporting visual progress on a build (progress screenshots).
- Scoring work against a target before declaring done.
- Shipping a change cleanly (commit/steps/verification).
- Managing threads/review loops.

## Workflow

1. Get the matching playbook at build time:
   - `https://raw.githubusercontent.com/MengTo/Skills/main/agent-skills/workflow/<name>/SKILL.md`
2. Follow its gates before reporting/shipping.

## Hard rules

- Load only the playbook you act on.
- These supplement — never override — Inhaus team rules and delivery standards.

## Verification

- Work is verified/score-checked before reported as done.
