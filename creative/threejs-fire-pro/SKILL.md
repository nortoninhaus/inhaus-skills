---
name: threejs-fire-pro
description: Use when building real-time volumetric fire, smoke, explosions or ember/ash effects for Three.js WebGPU. Wraps the upstream threejs-fire-pro library (Weaver-grade lineterm Fire/Explosion system) — drop-in component for any WebGPURenderer scene, with a visual editor, export to standalone apps and JSON/JS configuration files, and a playback example. Use for flames, smoke plumes, pyrotechnics, muzzle flashes, campfires, explosions, fire tornados.
version: 1.0.0
author: Inhaus Corp
license: Apache-2.0
platforms: [macos, linux]
metadata:
  hermes:
    tags: [threejs, fire, smoke, explosion, volumetric, webgpu, gpu, simulation, vfx, 3d]
---

# threejs-fire-pro — Volumetric fire / smoke / explosions for Three.js WebGPU

Wrapper that drives the upstream **threejs-fire-pro** library: GPU-accelerated, voxel-based
volumetric fire, smoke and explosions that drop into any `WebGPURenderer` scene. Ships with a
visual editor for designing effects and exporting them to standalone apps or configuration files.

Source: https://github.com/dgreenheck/threejs-fire-pro (MIT)

## When to use

- Any scene that needs **fire, smoke, explosions, embers, ash, muzzle flashes, campfires,
  fire tornados, pyrotechnics** in Three.js.
- WebGPU rendering path only (`THREE.WebGPURenderer`). **No WebGL fallback** — a plain
  `WebGLRenderer` scene cannot use this.

## Requirements

- Browser with **WebGPU** enabled (recent Chrome, Edge or Safari) — no WebGL fallback.
- Node **20.19+ or 22.12+** for the editor (Vite dev server).
- Three.js **`0.185.1`** as a peer dependency of the library.
- A discrete or recent integrated GPU (effects are fill-rate and compute heavy).

## Editor

Run `npm install`, then `npm run dev`, and open the printed URL (default
`http://127.0.0.1:5173`), or use the hosted editor. `npm run dev` first builds the standalone
runtime that the **Full app** export bundles.

Four areas:
| Area | What it does |
| --- | --- |
| **Presets** (left) | Built-in effects, blank **New simulation**, your saved presets |
| **Hierarchy** | The simulation plus emitters, forces and colliders; `+` adds objects |
| **Viewport** (center) | Orbit with the mouse; click an emitter's wireframe guide to select it; toolbar plays/pauses/restarts/undo/redo, gizmos, debug views |
| **Inspector** (right) | Tabs per simulation-wide setting and per selected emitter/force/collider |

Work is auto-saved as a draft in the browser. **Save preset** stores it; **Import** opens an
exported ZIP / `simulation.js` / `simulation.json`; **Export code** downloads a standalone app,
`simulation.js` or `simulation.json`.

## How a simulation is set up

One document: preview **scene** + **camera** + **simulation** settings + lists of **emitters**,
**forces** and **colliders**. Positions in meters, world space, ground at `y = 0`.

- **Sparse, unbounded grid** — solver allocates voxels only near emitters and visible fluid, so
  effects can move through a large scene.
- **GPU fluid solver** — staggered velocity grid, pressure projection, buoyancy, vorticity
  confinement, MacCormack scalar transport, optional fuel combustion.
- **Volumetric rendering** — ray-marched flame and smoke with blackbody flame color,
  self-shadowing smoke, depth-correct compositing, optional half-resolution mode.
- **Scene lighting** — flames light nearby surfaces via point lights (one per emitter and per
  burning explosion with `ClusteredLighting`).
- Categories per emitter/force/collider have an **imperative API** (`FireSimulation`).

## Exporting

- **Full app** — standalone HTML app bundling the effect in the built-in scene.
- **JSON / JavaScript configuration** (`simulation.json` / `simulation.js`) — the document
  format for the export runtime; requires the library + camera/floor overrides at play time.
- The **playback example** (`examples/playback`) shows importing a configuration and playing it
  in your own scene with the library.

## Library API

The library is a drop-in: initialize a `FireSimulation` bound to your `WebGPURenderer` scene,
attach emitters/forces/colliders imperatively, and step/update it each frame. Effects are
art-directed, not physically accurate — heat is a relative buoyancy/ignition quantity, and flame
color comes from a blackbody curve over a simplified fuel model.

## Pitfalls (read before using)

- **WebGPU only** — `THREE.WebGPURenderer`; no WebGL fallback. Verify the renderer before
  promising fire.
- **Performance depends on GPU** — cost scales with active voxels (sim) and screen coverage
  (render). Large fine-voxel effects are too slow on integrated GPUs. Levers: `halfResolution`,
  coarser `voxelSize`, coarser velocity grid, fewer `raySteps`.
- **Fixed timestep** — solver steps at 1/60 s, at most one step per `update()`. Slow frames slow
  the effect down rather than skipping ahead.
- **Voxel budget** — past `grid.maxVoxels`, extra cells stay empty, so wide/long-lived smoke
  gets clipped. Raise the budget or shrink the domain.
- **World-space + fixed ground** — the simulation must sit at the identity transform and the
  solid ground is fixed at `y = 0`. No floor settings in the document.
- **Depth limits** — reversed/logarithmic depth buffers unsupported; volume composites against
  opaque geometry depth and is not depth-sorted with other transparent objects.
- **Mesh emitters/colliders must be rigid, non-instanced meshes** with no morph targets or
  skinning; colliders must be closed, consistently-wound, and re-added after geometry changes.
- **One renderer per simulation** — a `FireSimulation` is tied to the renderer it was
  initialized with.
- **Editor scenes are built-in** — you cannot import your own models into the editor preview;
  the **Full app** export always uses the built-in scene. To place an effect in your own world,
  export a configuration and use the library (playback example).

## Verification

- Properties of the smoke/fire hold: emitters positioned in meters at world space, ground y=0,
  `y` flame rises, ember/ash lifecycle bounded.
- If a renderer is `WebGLRenderer`, report the WebGPU-only limitation before promising fire.
- Runs on a WebGPU-capable browser and the effect is visually confirmed (screenshot/video), or
  state clearly that it was not visually verified.
