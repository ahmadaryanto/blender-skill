# Token efficiency

Rules for keeping Claude sessions cheap and focused on Blender reels.

## 1. Reading discipline

- Read `CLAUDE.md` first. Then open only the doc or code section the task needs.
- Search before opening a file. Read only the line range you need, not the whole `build.py`.
- Do not re-read a file you already read this session unless it changed.
- Do not re-watch reference videos or re-read the MIT reference repo. Its key rules are summarised in the skill.

## 2. Asking and answering

- Ask for one scene or one fix at a time, with the scene key (for example `s7`) and the time in seconds.
- Answer in short lists. Point to file paths instead of pasting code.
- Do not paste the `.blend` file or long render logs into chat. Paste the last 20 lines of the error only.

## 3. Session habits

- Run `/clear` between unrelated tasks, for example from a new scene to the export step.
- Run `/compact` when a session gets long, and keep the decisions.
- Keep `CLAUDE.md` short. It loads every session.

## 4. Render cost

- Stills are cheap. Full renders are slow and expensive. Check stills first.
- Use `--frames a:b` for partial re-renders instead of the whole sequence.
- Use low samples for stills and raise them only for final hero shots.
- Run the full render in the background and check the result later.

## 5. Model choice

| Use the bigger model for | Use the smaller model for |
|---|---|
| A new scene layout or camera plan | Changing a time in `T` |
| A new environment or lighting setup | Caption timing and caption list edits |
| Debugging a tricky geometry or material problem | Running a still and reading the result |
| Export or loudness problems | Updating docs and logs |

## 6. Validation order

Cheapest first:
1. Syntax check of the changed script.
2. Stills at the start, middle, end, and each boundary.
3. Contact sheet of stills per scene.
4. Full render only when the owner asks.
