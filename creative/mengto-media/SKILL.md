---
name: mengto-media
description: Use when sourcing or generating asset images for web/creative work (Unsplash asset images, Aura asset images). Load before picking stock photos or generating visual assets for a client landing/creative.
version: 1.0.0
author: Inhaus Corp
license: MIT
platforms: [macos, linux]
metadata:
  hermes:
    tags: [media, images, unsplash, aura, assets, stock-photo]
---

# MengTo Media Skills

Two playbooks for visual asset sourcing/generation: `unsplash-asset-images` (curated
stock photo selection) and `aura-asset-images` (Aura-generated asset images).

Source: https://github.com/MengTo/Skills/tree/main/agent-skills/media

## When to use

- Picking stock/Unsplash images for a landing page, ad creative, or brand piece.
- Generating asset images (Aura) to match a design direction.

## Workflow

1. Get the matching playbook at build time:
   - `https://raw.githubusercontent.com/MengTo/Skills/main/agent-skills/media/<name>/SKILL.md`
2. Apply the selection/generation criteria at the moment you need assets.

## Hard rules

- Load only the playbook you act on.
- License-conscious: prefer documented free/CC sources (Unsplash); flag any licensing
  ambiguity before client use.

## Verification

- Assets match the approved brand tone and are license-appropriate.
