# Claude + Blender: task file template and a list of traps

Free files from the Render Bench video about building a 3D Short with Claude and Blender.

A 3D animated Short was built by Claude Fable 5.2 in Blender. It wasn't one prompt. It took six steps, two notes from a human, and one usage limit. This repo has the two things that helped most:

- [`TASK-TEMPLATE.md`](TASK-TEMPLATE.md): the task file structure we gave the model, with blanks for your own project.
- The list of traps below: real problems from our runs, and how to avoid them.

## How the setup works

1. Give Claude a folder on your computer (Claude app: **+** → **Add folder**).
2. Claude runs commands in a sandbox, so it can't open Blender on your machine directly. Ask Claude to write a tiny render server: one Terminal window that watches a folder, runs every job file that lands there (Blender in background mode with a Python script), and logs how long each job took.
3. Claude writes Blender Python scripts and drops job files into that folder. No Blender plugin needed.
4. One task file (template in this repo) tells the model everything: the goal, the materials, the rules, and where to stop.

Everything besides Claude can be free: Blender, a free voice model (we used Qwen3-TTS), ffmpeg.

## Traps we hit

**1. The first real render came out black.**
A fog volume filled the whole world and swallowed the sun.
Fix: keep fog inside a bounded box, never as a world-wide volume.

**2. Snowflakes rendered as cubes the size of a fist.**
Particles looked fine in the code and terrible on screen, right over the most important prop in the shot.
Fix: check particle size against a known object (a door, a person) in a test frame.

**3. The camera bumped into a goblet, and a chest slid out of the shot.**
Still test frames didn't show it. Motion did.
Fix: before the full render, render every 20th frame as a preview sheet and look through it.

**4. The model never watched its own video.**
It checked still frames, never the finished video, and never listened to the sound.
Fix: this step is yours. Watch it, listen to it, and only then publish.

**5. The voice was pasted at second zero.**
The video opened with the Short's own sound, and the narrator talked over it, a few seconds ahead of the picture.
Fix: every audio track gets an explicit start offset in the mix, and you check the first 10 seconds by ear.

**6. Subtitles landed on a character's face.**
Fix: in the plan, mark shots where a face sits low in the frame and move subtitles for those.

**7. A voice came out far too high.**
Our king was over 200 Hz. Words like "laughs easily" in the voice description pushed the pitch up.
Fix: describe the voice with low, calm words, measure the pitch, and lock the voice before anything else. Every cut is timed to it.

**8. The model hit the usage limit mid-job.**
Our five-hour limit went from 11% to 96%, and the run stopped right before the final edit. It continued about an hour later.
Fix: give the model one clear stop point and a work log, so it can resume. If your plan is tight, a cheaper model can run the same task file (in our test, Opus 5.5 used about 4% of the weekly limit for the same job).

**9. Changes after the voice is recorded are expensive.**
Fix: approve the script before any voice or render. Then approve the voice before any edit.

**10. Music for the whole video, picked blind.**
Fix: try the music on a 10-second clip first, pick from a few versions, then score the whole video. Keep music as a background bed, no lead melody under the narrator.

**11. Re-sending a file under the same name delivered the old version.**
Fix: when files move between the sandbox and your computer, give every new version a new file name.

## License

Use, copy and change these files for your own videos, commercial ones included. A link back to the video is appreciated.
