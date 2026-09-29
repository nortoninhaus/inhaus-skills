---
name: img2threejs
description: Use when turning an object/character reference image into a code-only, procedural, quality-gated, animation-ready Three.js model. Drives the img2threejs pipeline (forge/next.py state machine + grimoire reference docs). Use for image-to-3D reconstruction, sculpt specs, staged code generation.
version: 1.0.0
author: Inhaus Corp
license: Apache-2.0
platforms: [macos, linux]
metadata:
  hermes:
    tags: [threejs, 3d, image-to-3d, procedural, webgl, reconstruction, sculpt]
---

# img2threejs — Image to procedural Three.js

Wrapper that drives the upstream **img2threejs** pipeline: rebuild the object in a reference
image as a code-only procedural Three.js model, gated by a staged sculpting state machine and an
AI-vision self-correction loop. Reconstruction-by-code — not photogrammetry, mesh extraction, or
downloaded art packs.

Source: https://github.com/img2threejs/img2threejs (Apache-2.0, v2.0.0)

## When to use

- User attaches/points to an object or character image and wants a procedural Three.js model.
- Reconstruction / animation / destruction plan, sculpt spec, or staged code generation.
- Material studies, action-ready props, game objects, botanical/mechanical parts, stylized
  likeness-maximized characters.

## Requirements

- Python 3.10+ stdlib (no pip installs). Check `python3 --version`.
- A checkout of the repo. Clone once and reuse (do not re-clone per task):
  ```bash
  git clone --depth 1 https://github.com/img2threejs/img2threejs.git ~/img2threejs
  ```
- Agent vision/browser tooling for the screenshot self-correction loop (native image reading,
  browser MCP, or the project preview).

## Workflow — follow the router, never improvise

1. **Clone once** into a stable path (e.g. `~/img2threejs`). The repo's root `SKILL.md` is the
   always-loaded router: it holds the order of operations and every hard rule as one line.
2. **Run the state machine first, at every start/resume/correction:**
   ```bash
   python3 forge/next.py --state .img2threejs/state.json [<spec>]
   ```
   It reports the ordered checklist, the exact next command, evidence status, and bounded
   correction-loop status. Obey a hard stop; never continue from memory.
3. **Validate** the image is a suitable 3D target, **assess** class+complexity, write a
   `qualityContract` before any code, then **spec** it (hierarchy, materials, lighting, pivots,
   sockets, action anchors).
4. **Build pass-by-pass** (blockout → structure → form → material → lighting → interaction →
   optimization), **verify each pass** with a screenshot compared against the reference. Fail a
   pass if an identity-defining feature is wrong even when the global score looks fine.
5. Read the named `grimoire/` or `docs/` file **at the moment you reach that stage** — not before.

## Hard rules

- **Never one-shot a mesh.** Sculpt from the photo in order; the state machine is the authority.
- **Never continue from memory** — conversation context is disposable; `.img2threejs/state.json`
  is the local checklist authority.
- **State explicitly when output is approximate/stylized/low-poly.** A single image cannot reveal
  hidden sides or guarantee exact geometry — say so instead of faking confidence.
- **Never let a script score visuals** — that is the agent's job (screenshot vs reference).
- **Do not silently download meshes or art packs** — the code-only contract governs.
- Respect the user's cost rule: read only the stage file you are about to act on.

## Pitfalls

- **Do not install the upstream `SKILL.md` verbatim into Hermes** — it references `grimoire/`,
  `docs/`, and `forge/` sibling files that a Hermes skill install does not fetch. This wrapper
  points at a real checkout instead.
- **`forge/next.py` must run before every correction iteration**, not just at start.
- **Screenshot gate is mandatory** for visual reconstruction claims: capture, read back, and
  compare a side-by-side reference/render before reporting visual validation done.
- **`IMG2THREEJS_SHOWCASE_ROOT`** gates the TypeScript typecheck; without it those tests skip and a
  green run has not proven the emitted Three.js compiles.

## Verification

- `python3 forge/next.py --state .img2threejs/state.json` reports the expected next step.
- Each pass has a saved screenshot read back and compared against the reference.
- The emitted Three.js compiles (showcase typecheck when available).
- The summary names the stage files followed and any approximation/stylization caveats.
