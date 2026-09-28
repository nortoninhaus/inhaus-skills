---
name: mengto-ui
description: Use when designing or auditing UI/UX and prompting AI design tools. Guards against AI-slop, teaches first-principles UI prompting, and audits visual design quality. Load before UI mockup, design review, or AI-design output QA.
version: 1.0.0
author: Inhaus Corp
license: MIT
platforms: [macos, linux]
metadata:
  hermes:
    tags: [ui, ux, design, ai-slop, prompting, audit, design-system]
---

# MengTo UI Skills

Three playbooks for UI quality: `no-ai-design-slop`, `audit-ai-design-slop`,
`design-first-ui-prompting`. Purpose: produce and judge human-grade UI rather than
generic AI-generated visuals.

Source: https://github.com/MengTo/Skills/tree/main/agent-skills/ui

## When to use

- Creating UI mockups or desktop/preview designs for clients.
- Auditing or reviewing design output for "AI slop" artifacts.
- Prompting AI design tools (design-first prompting).

## Workflow

1. Load the matching playbook by task:
   - prompting a new design → `design-first-ui-prompting/SKILL.md`
   - reviewing/judging output → `audit-ai-design-slop/SKILL.md`
   - enforcing no-slop defaults → `no-ai-design-slop/SKILL.md`
2. Fetch at build time:
   - `https://raw.githubusercontent.com/MengTo/Skills/main/agent-skills/ui/<name>/SKILL.md`
3. Apply, then iterate visually in preview.

## Hard rules

- Load only the playbook you act on; never the whole corpus.
- These guards complement — not replace — client brand and design conventions.

## Verification

- Output is human-grade, not generic AI-slop (checked against the audit's criteria).
