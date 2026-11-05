# Blender Skill Kit

Shared skill, brand config, and guides for procedural 3D explainer reels. Scenes are built in headless Blender 4.5 with code, then edited and exported in Remotion.

This repo holds **documentation, skills, and brand settings only**. The Blender scripts, `.blend` files, renders, audio, and media stay in the project folder or shared storage.

## What is in here

| Path | Purpose |
|---|---|
| `CLAUDE.md` | Short project context loaded every session. |
| `.claude/skills/blender-explainer-video/SKILL.md` | The pipeline: running Blender, timeline, renders, editing, export, gotchas. |
| `brand/brand.json` | Brand values: watermark, logo, fonts, colours, captions, CTA. Edit this to use your brand. |
| `docs/BRAND_GUIDE.md` | Step-by-step guide for switching to your company brand. |
| `docs/TOKEN_EFFICIENCY.md` | Rules for keeping sessions cheap and renders minimal. |

## Make it your brand

Brand values live in `brand/brand.json`. To switch the kit to your company brand, follow `docs/BRAND_GUIDE.md`. Most of the work is that one file, plus the font loaders and watermark in the Remotion source.

## How to use it

1. Clone the repo.
2. Install Blender 4.5 and set the `BLENDER_EXE` environment variable to the path of `blender.exe`.
3. Open Claude Code inside your **project folder**, not your home folder.
4. Ask for one scene or one fix at a time, for example: "Check scene s7 with a still. Do not render."
5. Approve stills before any full render.

## Team rules

- **Do not render** until the owner says so. Stills are fine.
- **Captions only** unless the owner picks a voice.
- **Indonesian captions**, readable on a phone.
- **Full-size files only** for delivery.
- **Never animate waste or liquid** leaving a vehicle.
- **No real people's names or likenesses** in scenes.
- **Licensed music, SFX, and fonts** only.
- **No secrets in the repo.** API keys go in environment variables.

## Credits

The skill references rules from https://github.com/arjun988/blender-skills (MIT). The rules are summarised in the skill, not copied.
