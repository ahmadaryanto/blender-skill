# Brand guide: make the Blender reels your company's

The kit ships with the values from the example reel. Follow these steps to switch it to your company brand. Most of the work is one file.

## 1. What you change

All brand values live in `brand/brand.json`:

| Field | What it controls |
|---|---|
| `name` | Brand name, used in titles |
| `watermark` | Handle shown below the caption area |
| `logo` | Logo file and corner placement |
| `font` | Caption, watermark, and heading fonts |
| `colors` | Caption text, caption box, watermark, background, accent |
| `captions` | Size, box, corner radius, shadow, language |
| `audio` | Loudness target and voice policy |
| `cta` | Closing question and optional comment keyword |
| `endTitle` | Title and tagline on the final card |

## 2. Steps

1. **Make a branch.** Do not edit `main` directly.
   ```
   git checkout -b brand/your-company
   ```
2. **Add your logo.** Save a transparent PNG at `brand/assets/logo.png`. Keep it small. If it is large, store it in shared storage and put the link in `logo.file`.
3. **Edit `brand/brand.json`.** Change each field.
4. **Match the font in the Remotion source.** The fonts are defined in `lib/theme.ts` of the edit project. Change the font loaders there to your brand fonts, using Google Fonts where possible. Then update `font` in `brand/brand.json` to match.
5. **Update the watermark and captions in the source.** The watermark and the caption list are in the Remotion composition (`Plane.tsx` in the example). Change the handle there to match `watermark`.
6. **Check the colours.** Caption text on a dark box needs a contrast ratio of at least 4.5:1.
7. **Run a check.** Ask Claude Code: "Read `brand/brand.json` and list any field that still has an example value."
8. **Test on one still.** Ask for one still. Confirm the watermark, colours, and font. Do not render a full video to test.
9. **Commit and open a pull request** for the owner to review.

## 3. Captions and readability

- Keep captions readable on a phone. No small copy.
- Keep the caption box or shadow. It keeps text readable over any frame.
- Keep captions in the caption area, and the watermark below it.
- Captions are text overlays in the edit. Never bake them into the 3D frames.

## 4. Watermark and logo

- The watermark is below the caption area, never over it.
- The logo sits in a corner, small, and off the caption area.
- Do not stretch or recolour the logo.

## 5. Voice and language

- Captions follow `captions.language`. The example is Indonesian (`id`).
- Voiceover is off by default. Only the owner picks a voice, and only if the team has the rights to it.
- Set the tone in `CLAUDE.md`, under the rules.

## 6. Safety rules that stay the same

- Do not use real people's names or likenesses in the 3D scene.
- Do not show a real person in an event they did not take part in.
- Do not fabricate facts. Check claims before they go into captions.
- Use only licensed music, SFX, fonts, and images.
- Do not commit `.blend` files, renders, or keys.
- Do not render unless the owner asks.

## 7. Quick reference

| I want to change | Edit this |
|---|---|
| Brand name, watermark, colours, captions, CTA | `brand/brand.json` |
| Logo | `brand/assets/logo.png`, then `logo` in `brand/brand.json` |
| Fonts | Font loaders in `lib/theme.ts` (edit project), then `font` in `brand/brand.json` |
| Watermark text and caption list | Remotion composition (`Plane.tsx` in the example) |
| Scene timing | `T` in `build.py` |
| Tone of voice | `CLAUDE.md` rules |
