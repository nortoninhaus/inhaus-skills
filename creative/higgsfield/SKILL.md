---
name: higgsfield
version: 0.1.0
description: |
  Generate images/videos/3D assets/audio via the Higgsfield CLI (higgsfield.ai).
  Defaults: GPT Image 2 for image/design/text, Seedance 2.0 for video, Nano
  Banana 2/Lite/Pro for character/reference images, Marketing Studio for ads,
  Seed Audio 1.0 for audio. Use when: "generate an image", "make a video",
  "animate this photo", "image-to-video", "edit/stylize/remix this image",
  "reframe this video", "create a 3D model/GLB", "create a sound effect",
  "make music", "create an ad", "make a UGC video", or "analyze video virality".
  NOT for: Soul training, brand books, photoshoots, thumbnails, explainers,
  playable games (use the matching dedicated Higgsfield skill), or TTS.
argument-hint: "[prompt-or-analysis-request] [--model <name>] [--image|--video <path-or-id>]"
allowed-tools: Bash
---

# Higgsfield Generate (via CLI)

Submit jobs to any Higgsfield model with the locally-installed `higgsfield` CLI.
Covers generic image/video/3D/audio generation, Marketing Studio (branded ads,
avatars, products, hooks, settings), and Virality Predictor video scoring.

## Step 0 — Prereqs (already installed)

- `higgsfield` CLI lives at `~/.npm-global/bin/higgsfield` (installed via npm).
- If `higgsfield account status` fails with `Session expired` / `Not authenticated`,
  ask the user to run `higgsfield auth login` (interactive) and wait for confirmation.
- Do NOT reinstall via curl|sh; the CLI is already present.

## UX Rules

1. Be concise. No raw IDs, no JSON dumps in chat. Print the media URL for generated
   assets, or the text summary for Virality Predictor.
2. Detect the user's language from the first message and reply in it. Technical args
   (`--aspect_ratio 16:9`) stay English.
3. Don't batch-ask. Pick a sane default model and ask one thing at a time only if
   genuinely missing.
4. Pass `--wait` to `generate create` so the command blocks until done and prints the
   result URL itself.

## Discovery guardrail

When looking for a feature/model, first run `higgsfield model list --json` and inspect
likely `job_set_type` names; verify with the full list before answering. Workflows are
separate from models: `higgsfield workflow list`, `higgsfield workflow get <name>`.
Virality Predictor = `job_set_type` `brain_activity`, video-in/text-out. Route
"analyze this video / score this ad / evaluate the hook" to `brain_activity`.

## Workflow — generic generation

1. **Pick a model** (defaults unless the brief needs a specialist):
   - **GPT Image 2** → default image: design, UI, banners, typography, on-image text.
   - **Seedance 2.0** → default video: serious motion, cinematic, multi-shot,
     image-to-video, 4–15s up to 4K.
   - **Nano Banana 2/Lite/Pro** → character, cartoon, stylized, reference image work.
   - **Marketing Studio** → ads, UGC, product demos, unboxing, TV spots, presenter videos.
   - **Seed Audio 1.0** → default audio: text-to-audio, SFX, ambience, foley, music-like.
   - **Soul 2.0 / Soul Cinema** → aesthetic UGC / fashion editorial / cinematic stills.
   - **Multi-Image to 3D** (`multi_image_to_3d`) → GLB from 1–4 reference images,
     `--should_texture true` when needed.
   - Map display names → IDs with `higgsfield model list --json`.

2. **Pass media straight to flags.** Media flags accept a local path or a UUID;
   CLI auto-uploads paths. See `higgsfield model get <jst>` for accepted roles.

3. **Submit and wait in one shot:** `higgsfield generate create <jst> [--prompt "..."] [media flags] --wait`.
   `--json` for machine-readable output.

4. **Deliver:** primary result URL + one-line summary (model, duration/GLB). For
   Virality Predictor: scores + business interpretation + Open report link.

Examples:

```bash
higgsfield generate create gpt_image_2 --prompt "neon city at dusk" --aspect_ratio 16:9 --resolution 2k --wait
higgsfield generate create seedance_2_0 --prompt "camera dollies in" --start-image ./first.png --duration 12 --resolution 4k --wait
higgsfield generate create seed_audio --prompt "cinematic rain ambience" --wait
higgsfield generate create multi_image_to_3d --image ./front.png --image ./side.png --should_texture true --wait
higgsfield generate create brain_activity --video ./ad.mp4 --wait
```

## Marketing Studio

Branded ad image/video gen: `marketing_studio_video` / `marketing_studio_image`.
Concepts: Avatar (presenter), Product (brand item), Hook (opening angle), Setting
(scene), Brand kit, Ad format. Discovery:

```bash
higgsfield marketing-studio avatars list --json
higgsfield marketing-studio products list --json
higgsfield marketing-studio hooks list --json
higgsfield marketing-studio settings list --json
higgsfield marketing-studio ad-references list --json
higgsfield marketing-studio brand-kits list --json
higgsfield marketing-studio ad-formats list --json
```

Quick ad video: get/create product → pick avatar → optionally hook/setting → generate:

```bash
higgsfield generate create marketing_studio_video \
  --prompt "..." --avatars @"$AVATARS_JSON" --product_ids @"$PRODUCTS_JSON" \
  --mode ugc --duration 15 --resolution 720p --aspect_ratio 9:16 --wait
```

`product_ids` and `avatars` are JSON arrays passed via `@file.json`; `--hook_id`/`--setting_id`
valid only on `marketing_studio_video` for `ugc`/`ugc_how_to`/`ugc_unboxing`/`product_review`/`ugc_virtual_try_on`.
Click-to-Ad shortcut: pass `--url https://shop...` to `marketing_studio_video` to reuse a fetched product.

## Virality Predictor video scoring

```bash
higgsfield generate create brain_activity --video ./creative.mp4 --wait
```
Text result: overall score, peak hook second, sustain, strongest/weakest regions,
Open report URL. Higher Visual/Auditory/Language/Attention = stronger stimulus; lower
Default Mode is better (less mind-wandering). Send the report URL, not raw artifact URLs.

## Workflows

```bash
higgsfield generate workflow reframe --video ./src.mp4 --aspect-ratio 9:16 --wait
higgsfield generate workflow draw_to_video --video ./src.mp4 --sketch ./frame.png --timestamp 3.2 --wait
higgsfield generate workflow dubbing --video ./src.mp4 --target_language spa --wait
higgsfield generate workflow voice-change --video ./src.mp4 --voice_type preset --voice_id <id> --wait
```

## Errors

- `Missing required params: prompt` → ask for a prompt.
- `Missing required params: medias` on `brain_activity` → pass one `--video`.
- `Invalid values: aspect_ratio=...` → pick from allowed enums.
- `Unknown params: foo` → check `higgsfield model get <jst>`.
- `Session expired` → ask user to run `higgsfield auth login`.
