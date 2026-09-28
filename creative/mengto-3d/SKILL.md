---
name: mengto-3d
description: Use when building 3D scenes and Three.js WebGL experiences for web projects (virtual tours, sky/atmosphere, water, falling leaves, seasons, high-poly models, retina rendering). Load the matching MengTo 3d playbook before writing 3D code.
version: 1.0.0
author: Inhaus Corp
license: MIT
platforms: [macos, linux]
metadata:
  hermes:
    tags: [threejs, webgl, 3d, shader, virtual-tour, atmosphere, sky, retina]
---

# MengTo 3D Skills

Nine curated playbooks for Three.js/WebGL scenes on the web: virtual tours,
ultra-realistic water, sky rays/backgrounds, falling leaves, four-seasons environments,
high-poly models, high-res textures, and retina (200%) rendering.

Source: https://github.com/MengTo/Skills/tree/main/agent-skills/3d

## When to use

- A client site/landing needs a real-time 3D scene or atmosphere effect.
- Virtual tour / architectural walkthrough / showroom / museum exploration.
- Adding water, sky, environmental particles, or high-fidelity model rendering.

## Workflow

1. **Pick one playbook** by effect (`3d-virtual-tour`, `3d-ultra-realistic-water`,
   `3d-sky-rays`, `3d-falling-leaves`, `3d-four-seasons`, etc.).
2. Get the playbook at build time:
   - `https://raw.githubusercontent.com/MengTo/Skills/main/agent-skills/3d/<name>/SKILL.md`
3. Implement, then render-verify in the preview/browser toolset.

## Hard rules

- **Read only the one matching playbook** when implementing; do not load the whole category.
- Respect target GPU/browser; prefer devicePixelRatio-aware rendering (several playbooks
  assume retina/200%).
- Client brand and style still override the playbook's visual defaults.

## Verification

- The scene runs at the intended performance on target devices (check FPS/resolution).
- Effеct matches the approved aesthetic, iterated visually.
