# Task file template: a 3D Short built by Claude in Blender

Copy this file into your project folder, fill in every `[...]`, and tell Claude: "Read TASK.md and do it."
Keep it as one file. The model should not need anything that isn't listed here.

---

## 0. Ground rules

- Work only inside this folder: `[project folder]`. Don't open other folders.
- No paid services and no image or video generation, unless written here: `[none / list]`.
- Keep a work log in `log.md`: what you did, what failed, how long renders took.
- If you stop for any reason (limit, error), the log must be enough to pick up where you left off.

## 1. Goal

- What: a 3D animated Short about `[story in one line]`.
- Format: 1080x1920, `[30 / 60]` fps, length `[N]` seconds (matches the voice track).
- Look: `[style in 2-3 lines: e.g. 2D cartoon characters in a toon-shaded 3D world, warm winter light]`.
- Final file: `final/[name].mp4`, plus `final/[name].en.srt`.

## 2. Materials (all in this folder)

- `script.md`: the approved script. Don't change the words.
- `voice/voice.wav` + `voice/timing.json`: the locked narration and character lines, with start and end time for every line and word. Every cut is timed to this.
- `characters/`: `[how characters are drawn: e.g. our 2D card engine, list of characters and emotions]`.
- `refs/`: `[reference images or a reference video, and what to take from them: pacing, camera, NOT the characters]`.
- `mistakes.md`: every mistake we made before. Read it first.

## 3. How to run Blender

- You can't run Blender from your sandbox. Put a job file into `[jobs/queue/]`; the render server on my computer runs it and writes the log to `[jobs/done/]`.
- One job = one Blender run: `blender -b --python [script.py] -- [args]`.
- Check the log after every job. A job without a log line didn't run.

## 4. Work in stages, with stops

**Stage 1: plan and test frames.**
1. A shot plan: one row per line of the script (time, what we see, camera, characters, emotion).
2. The cast: every character in every emotion the plan needs.
3. Four test frames: `[the opening shot, a wide shot of the world, an interior, a close-up of a material]`.

**STOP after stage 1.** Show me the plan and the test frames and wait for my notes. Don't build the full world before I answer.

**Stage 2: world and shots.**
1. Build the world as code, in passes: shapes in grey first, then materials and color, then light.
2. Characters and emotions per the plan. Faces change 3-7 times per shot, never frozen.
3. Before the full render, render every 20th frame as a preview sheet and check it: camera inside objects, props leaving the frame, black or empty frames, subtitles over faces.

**Stage 3: render, sound, edit.**
1. Full render. Log the time per frame.
2. Sound: voice at its own offset, music as a quiet bed under the voice (no lead melody), effects. Loudness about -14 LUFS.
3. Edit to the voice timing. Subtitles from `timing.json`.

## 5. Checks before you call it done

- [ ] Length matches the voice track.
- [ ] No black, empty or broken frames (contact sheet of the whole video).
- [ ] Subtitles never cover a face.
- [ ] The first second is a strong frame, the last frame loops into the first (if it's a loop).
- [ ] Every item in `mistakes.md` checked.

The model can't fully judge timing and sound. A human watches and listens to the final video before publishing.

## 6. What to hand back

- `final/[name].mp4` and `final/[name].en.srt`
- `log.md`: stages, time spent, render times, problems.
- `known-issues.md`: anything you know is not perfect. Be honest, it saves a round trip.
