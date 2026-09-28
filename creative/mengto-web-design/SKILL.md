---
name: mengto-web-design
description: Use when designing, building or rewriting landing pages and marketing/site frontends. Load the matching MengTo web-design playbook before writing HTML/CSS/JS (WebGL, GSAP, animations, layouts). Read catalog first, then pull the one skill that fits the target look.
version: 1.0.0
author: Inhaus Corp
license: MIT
platforms: [macos, linux]
metadata:
  hermes:
    tags: [web-design, landing-page, webgl, threejs, gsap, animation, layout, css, frontend]
---

# MengTo Web-Design Skills

Curated library (88 playbooks) from the open MENGTO skills corpus for producing rich,
Awwwards-grade web frontends: layouts, WebGL/Three.js scenes, GSAP/Lenis motion,
scroll storytelling, hover/orbit effects, design-system aesthetics.

Source: https://github.com/MengTo/Skills/tree/main/agent-skills/web-design

## When to use

- Building or modernizing any client-facing landing page / marketing site (Inhaus web work).
- A specific visual technique is wanted: particle trails, glass/skeuomorphic/fabric mesh
  aesthetics, scroll-scrubbed reveals, bevel/laser/dither borders, Cobe/globe-WebGL, marquees.
- Animating interactions: mouse-driven orbit, shader cursor trails, scroll timelines.

## Workflow

1. **Catalog first.** Read the index before writing code:
   `agent-skills/web-design/README.md` + `WEB-DESIGN-SKILLS.md` map every playbook by name.
2. **Pick ONE playbook** that matches the requested look/effect. Load its raw `SKILL.md`
   and follow it. Do not stack unrelated playbooks.
3. **Retrieve the file** you need at build time:
   - Docs: `https://raw.githubusercontent.com/MengTo/Skills/main/agent-skills/web-design/<name>/SKILL.md`
4. Implement, then visually verify in the preview/browser toolset.

## Catalog topics (88)

Representative playbooks name a look, not a goal: `blue-cloudy-clean-modern`,
`clean-minimal-beige-light-mode`, `dark-glass-clean-layout`, `editorial-tech`,
`glass-dark-mode-clock`, `landing-page`, `cinematic-gsap-lenis-motion-system`,
`marquee-loop`, `beautiful-shadows`, `background-grid-webgl`, `gooey-blob-system`,
`masked-reveal`, `animation-on-scroll`, `add-mouse-driven-orbit` … See the README index
for the full 88.

## Hard rules

- **Fetch the skill at build time, not the whole corpus into context.** Read only the one
  matching playbook when you are about to implement.
- **Never invent the look** from the catalog name alone; open the SKILL.md (it carries the
  actual constraints/tokens/snippets) before producing code.
- **Client work wins on brand.** The playbooks are technique references; the client's design
  system and style guide still override their aesthetic defaults.
- Respect the user's cost rule: pull exactly the playbook you act on, not a batch.

## Pitfalls

- These are MENGTO corpus playbooks — many use Three.js/GSAP, so confirm the target
  browser support and bundle nothing the page does not use.
- Some playbooks reference sibling demo assets; the SKILL.md alone is the portable unit.
- Do not wholesale copy-page these playbooks into profile skills — they are meant to be
  fetched from upstream on demand.

## Verification

- The looked-up playbook name the summary references actually exists in the catalog.
- Rendered result matches the aesthetic the client approved (iterate visually).
