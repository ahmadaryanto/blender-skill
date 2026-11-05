---
name: blender-explainer-video
description: Build a procedural 3D explainer reel (vertical 1080x1920, captions only by default, Indonesian) with headless Blender 4.5, then edit captions, crossfades, and loudness in Remotion and export. Use for any Blender explainer reel, a 3D animation reel, or changes to the plane-toilet project in this kit.
---

# Blender explainer video (procedural, headless)

Pipeline for procedural 3D explainer reels. Scenes are built in code, rendered headless with Blender, then edited and exported. Read `CLAUDE.md` for team rules and `brand/brand.json` for brand values before you change anything.

## Hard rules

- **Do not render** until the owner asks. Check with stills first.
- **Captions only** by default. No voiceover unless the owner picks one.
- Deliver the **full-size file only**. No cut-down or "small" versions.
- Captions are text overlays added in the edit, never baked into the 3D frames.
- The watermark (`brand.watermark`) sits below the caption area, so the two never collide.
- Indonesian captions, casual tone. Keep English terms in English (AI, ChatGPT, LLM).
- **Never animate waste or liquid** falling out of a vehicle or object. Use abstract particles that go into a sealed system.
- Do not add real people's likenesses or names to the scene.
- Use only licensed music, SFX, and fonts.

## Layout (expected project structure)

```
<project>/
  blender/
    build.py            source of truth: builds the whole scene procedurally
    render_all.ps1      main render plus environment handles (crossfades)
    *.blend             optional snapshot for viewing in the GUI (do not commit, see .gitignore)
  edit/
    audio.mjs           synthesised ambience and timed SFX -> audio.wav
    assemble.ps1        crossfade blend -> render.mp4 -> Remotion -> final export
    video/src/          captions (CAPS array), watermark, audio, composition
  renders/              PNG frames and final output (not in git)
```

## Running Blender

- Blender location: set the `BLENDER_EXE` environment variable to the path of `blender.exe`. Do not hard-code a path in the scripts.
- Always run headless: `blender -b -P build.py -- <args>`.
- **Do not** run `build.py` from the Blender GUI Scripting tab. It resets the factory settings, reads arguments, and renders at the end, so it can error or hang. To inspect the scene in the GUI, save a snapshot with `--save <path.blend>` and open that file.
- Arguments: `--out <dir>`, `--still <sec>` (repeatable, PNG stills), `--pct <n>` (resolution percent), `--frames a:b`, `--env cruise|airport`, `--samples <n>`.
- Frame number = `round(sec * 30) + 1` (the `F(sec)` helper in `build.py`).

## Timeline and scenes

- The timeline is the `T` dictionary in `build.py`. Each key is a scene start time in seconds. Change times there, not in the render commands.
- Cameras use `cam_key(t, location, look_at, lens)`, which keys a camera plus a track target.
- Environments switch at a set time (`env_at(t)`). Crossfade windows need their own rendered handles.

## Rendering and partial re-renders

- Full render: `render_all.ps1` (main at 24 samples, then the two environment handles). It is slow, so run it in the background.
- Partial re-render: `--frames a:b` writes only those frames into the existing folder. Use it when a change touches a few seconds.
- **Off-by-one trap:** `--env` forces the environment on every frame in the range. Do not force an environment on a range that crosses the switch time. Split the range instead.
- If a scene changes near a crossfade window, re-render the handles for that window too.

## Editing and export

1. Generate audio: `node audio.mjs <path>/audio.wav`. If the timeline changed, update the SFX times in `audio.mjs` to match `T`.
2. Run `assemble.ps1`. It copies the main frames, blends the crossfade windows with ffmpeg, encodes the render, renders the Remotion composition, and exports the final file at about -14 LUFS.
3. Check the output: loudness with `ffmpeg -af ebur128`, plus a contact sheet from each scene.

## Adding text to the 3D scene (labels)

Flat text objects work well for signs and labels:

- Use `bpy.ops.object.text_add`, set `body`, `size`, centre alignment, and a small `extrude` (0.01).
- Text faces +Z by default. Rotate by 90° on X to face the camera side.
- On a curved surface, tilt the plate to the surface normal.
- Put labels in the shell material list so they fade with the cutaway.
- Test each label with a `--still` before a full render. Check that the camera frame does not cut it off.

## Known gotchas

- `box()` needs `transform_apply(location=False, rotation=False, scale=True)`. The default moves objects to the origin.
- The look uses Eevee Next with AgX. Keep emission on lights and glowing parts low, or they blow out.
- Test stills at the start, middle, and end of each scene. Props such as cones or trucks can block the shot.
- For keyframed visibility or alpha, use the `key_vis` and `key_socket` helpers, and keep shell materials in the shell list.

## Reference (MIT)

The repo https://github.com/arjun988/blender-skills (MIT) has Blender skills built for live Blender MCP control. Its rules transfer to headless builds, but do not copy its MCP steps. Use these when writing or reviewing a scene:

- `camera-cinematography`: lens choice (18–28 mm wide, 35–50 mm story shots, 85–135 mm close detail), horizon level, headroom, no tangents on the frame edge.
- `lighting`: three-point lighting (key, fill at 1/2 to 1/4 intensity, rim). Warm light for interiors, cool light for overcast skies.
- `rendering`: Eevee for previews and stylised looks, Cycles for realistic final frames. Stills use low samples; raise samples for any final hero shot.
- `materials`: reuse master materials and change only parameters.
- `qa-review`: severity list (Blocker, Major, Minor, Note) and a ship or no-ship verdict. Use it for the stills check before each full render.

## Checklist before delivering

- [ ] Stills from every scene look right (no clipping, cut-off text, or floating objects).
- [ ] Caption timings match the caption list in the Remotion source.
- [ ] Loudness is about -14 LUFS.
- [ ] Watermark is readable and does not overlap captions.
- [ ] Output is the full-size file only, in the owner's delivery folder.
- [ ] Owner has approved the stills before any full render.
