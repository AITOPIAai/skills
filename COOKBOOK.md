# AITOPIA Skills — Cookbook

Recipes that chain the skills. Each one is a request you can give your agent as-is; the steps show what happens underneath.

## Recipe 1 — Product ad from a product photo

> *"Make a 9:16 product ad from ./mug.png with a warm voiceover and soft music."*

1. `aitopia-upload` — `./mug.png` becomes an asset URL.
2. `aitopia-product-ad` — loads AITOPIA's product-ad playbook: hero keyframe from the photo, motion clips, voiceover sized to the clips.
3. `aitopia-edit` — joins the clips, lays the voiceover, adds music under it (`add_background_music`, ducked under the voice).
4. Result: the video inline, a download link and **Open in AITOPIA**.

## Recipe 2 — Four image options, then animate the best one

> *"Give me four options for a moody coffee-shop poster, then animate the one I pick."*

1. `aitopia-generate` — one call with `count: 4`; the four images come back side by side.
2. The user picks one.
3. `aitopia-generate` — image-to-video with a video model from the playbook; the clip appears when it is ready.

## Recipe 3 — UGC ad for an app

> *"Create a 15 second UGC-style ad for my budgeting app, hook in the first two seconds."*

1. `aitopia-ugc-video` — AITOPIA's UGC playbook: hook, creator-style shots, natural voice.
2. `aitopia-edit` — captions with `add_text` or `subtitle`, 9:16 with `resize`.

## Recipe 4 — YouTube thumbnail with your face and logo

> *"Make three thumbnail options for 'I tried 30 days of cold showers', use ./me.jpg and ./logo.png."*

1. `aitopia-upload` — both files.
2. `aitopia-youtube-thumbnail` — variants with the face and logo, big readable text.

## Recipe 5 — Clean up and reframe an existing video

> *"Take ./talk.mp4, cut 0:05–0:40, make it 9:16, add our logo top-right and normalize the sound."*

1. `aitopia-upload` — `./talk.mp4`.
2. `aitopia-edit` — `trim_video` → `resize` (fit cover) → `overlay` → `audio_tools` normalize.

## Recipe 6 — Brand kit

> *"Build a brand kit for Mira, a plant shop in Istanbul."*

1. `aitopia-brand-kit` — logo direction, palette, typography and usage rules, then example assets.

## Quick reference — which recipe for what

| Goal | Recipe |
|---|---|
| Ad from a product photo | 1 |
| Explore options before committing | 2 |
| Social ad that feels native | 3 |
| Thumbnail | 4 |
| Fix / reformat footage you have | 5 |
| Visual identity | 6 |

## Patterns these recipes share

- **Upload first.** Local files go through `aitopia-upload`; everything else takes asset URLs.
- **Playbook first.** Workflow skills load AITOPIA's playbook, which decides the steps and the models.
- **Stills before motion, audio last.** Images, then clips from them, then voiceover and music sized to the real clip lengths.
- **Confirm before spending.** Agents say what they will make before expensive steps (video, many images).
- **Everything is saved.** Each result has an **Open in AITOPIA** link to keep working there.
