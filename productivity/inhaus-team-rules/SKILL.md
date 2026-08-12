---
name: inhaus-team-rules
version: 1.0
description: Team operational rules, delivery standards, and escalation paths for Inhaus workflows.
author: Nico (brian)
tags: [operations, team, delivery]
---

# Inhaus Team Rules

## Operational Standards

All profiles follow these principles:
- Scripts before LLM calls; lowest model necessary per task
- Never make strategic, creative, pricing, or client-facing decisions alone
- Escalate anything with reputation or money risk
- Spanish for client-facing/Ecuador context; English for technical/product items
- Zero fluff; bullet points only in briefs

## Escalation Path

1. Profile handles its domain autonomously
2. If blocked → delegate to brian (CoS) for routing
3. If reputation/money risk → notify Nicolás immediately
4. Security/legal issues → run compliance-reviewer sub-agent first

## Delivery Standards

- Code: peer-reviewed by verifier sub-agent before merge
- Content: compliance-check before external publication
- Ads: Pulse verifies account health before budget changes
- Reports: data-backed only, never estimates presented as facts
