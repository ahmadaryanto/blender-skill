# CLAUDE.md — blender-skill-kit

Short context for Claude Code. Detail lives in `docs/` and the skill.

## What this is

Team kit for procedural 3D explainer reels built in headless Blender 4.5, then edited in Remotion. The example project is "Ke mana kotoran toilet pesawat?" (vertical 1080x1920, 30 fps, captions only).

## Skill

- `blender-explainer-video`: use for any Blender reel, scene, camera, environment, or export work. Path: `.claude/skills/blender-explainer-video/SKILL.md`.

## Rules

- Do not render unless the owner asks. Check from stills.
- Captions only unless the owner picks a voice.
- Indonesian captions, readable on a phone.
- Deliver full-size files only.
- Never animate waste or liquid leaving a vehicle.
- Do not use real people's names or likenesses.
- Do not commit `.blend` files, renders, media, or secrets (see `.gitignore`).
- Do not push to GitHub or delete files without approval.

## Token saving

Read `docs/TOKEN_EFFICIENCY.md` before a long session. Search before opening a file, read line ranges, and check from stills, not renders.

## Where things are

- Brand values (watermark, colours, fonts, captions, CTA): `brand/brand.json`. Brand change steps: `docs/BRAND_GUIDE.md`.
- Team overview: `README.md`.
- Blender path: set `BLENDER_EXE` in your environment.
