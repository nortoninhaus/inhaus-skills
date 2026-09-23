---
name: modern-web-guidance
description: Use when writing, reviewing or modernizing web frontend code. Consult Chrome's Modern Web Guidance guides before implementing UI, CSS, forms or performance work.
version: 1.0.0
author: Inhaus Corp
license: MIT
platforms: [macos, linux]
metadata:
  hermes:
    tags: [web, frontend, chrome, baseline, css, html, performance, accessibility, forms]
---

# Modern Web Guidance

Google Chrome's official web-platform guidance corpus (160+ guides), exposed as a searchable
reference. Use it to write modern, interoperable browser code instead of guessing at APIs or
reaching for a JavaScript library that the platform already replaces.

Source: https://developer.chrome.com/docs/modern-web-guidance

## When to use

- Implementing browser UI: dialogs, modals, popovers, tooltips, menus, tabs, accordions, carousels.
- CSS layout and modern features: container queries, anchor positioning, `:has()`,
  `@starting-style`, view transitions, `field-sizing`, scroll-driven animations.
- Forms: validation, input UX, autofill, error announcements.
- Performance: LCP, INP, long tasks, image/font loading, preloading on hover.
- Accessibility: focus management, keyboard navigation, semantics, reduced motion.
- Modernizing legacy code: jQuery modals, tooltip libraries, manual focus traps, scroll listeners.
- Reviewing web code before shipping, or auditing a site for modern best practices.

## Requirements

Node 18+ (`node --version`). The CLI runs through `npx`. The first call downloads the package
(a few seconds); later calls are cached.

## Core commands

Search — returns JSON with candidate guides:

```bash
npx --yes modern-web-guidance@latest search "animate a dialog backdrop"
```

Retrieve one guide by ID — returns the full markdown guide:

```bash
npx --yes modern-web-guidance@latest retrieve "<guide-id>"
```

## Workflow — follow this order

1. **Search before implementing, not after.** Query the user-visible behaviour
   ("light-dismiss a dialog", "sticky header on scroll"), not an API name.
2. **Read the JSON hits.** Pick by `similarity` and check `featuresUsed` against the project's
   Baseline/browser target. If the guide depends on a feature the target doesn't support, pick a
   different guide rather than shipping a broken one.
3. **Retrieve only the guides you will act on** (1-3). `tokenCount` is the cost of that guide;
   thousands of tokens is normal, but never retrieve a dozen "just in case" — that is the single
   fastest way to burn context on this skill.
4. **Prefer native platform features** over libraries: `<dialog>`, Popover API, `:has()`,
   container queries, `@starting-style`, view transitions, Invoker commands.
5. **Cite the guide id** in your summary of the change, so a reviewer can verify the reasoning.

## Categories in the corpus

`ui-behaviors`, `ui-components`, `ui-atoms`, `forms`, `css`, `visual-design`, `performance`,
`security`, `accessibility`, `html-web-components`, `js`, `motion`, `built-in-ai`, `webmcp`,
`pwa`, `privacy`, `wasm`.

## Hard rules

- **Never invent browser support.** The guides carry Baseline data — quote it, don't guess.
- **Do not upgrade a baseline target on your own.** If the guide needs a newer feature than the
  project targets, report the conflict instead of silently changing the target.
- **A guide is reference, not a mandate.** It is authoritative on platform capability; the
  project's own conventions and design system still win on style and structure.
- Accessibility and performance advice from these guides is not optional polish — apply it in the
  same pass, not as a follow-up.

## Pitfalls

- **`npx` output is not JSON-safe by default.** `search` prints a JSON array; pipe it through a
  parser rather than eyeballing it when you need several IDs.
- **Offline / rate-limited:** the guides are also plain markdown in the published repo at
  `skills/modern-web-guidance/guides/<category>/<guide-id>.md` on the `GoogleChrome/modern-web-guidance`
  repository. Fetch the raw file directly if the CLI cannot run.
- **Telemetry:** the CLI reports anonymous install counts and guide IDs to Google. Raw prompts are
  not collected. Flag this if a client forbids third-party telemetry.
- **Version pinning:** `@latest` can change behaviour between sessions. If a guide ID stops
  resolving, re-run `search` to get the current ID.

## Verification

Before reporting web work done:

- The guide id(s) you followed are named in the summary.
- Any feature you used is supported by the project's browser target.
- Accessibility behaviour (keyboard, focus, announcements) was checked, not assumed.