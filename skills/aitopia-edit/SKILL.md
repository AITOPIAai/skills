---
version: 0.1.0
name: aitopia-edit
description: "Edit video and audio with AITOPIA: join clips, add voiceover or music, trim, resize to 9:16 / 16:9 / 1:1, add text or a logo, subtitles, fades, speed changes, mute or extract audio, animate a still image. Use for any media editing request."
argument-hint: "[edit to make] [file or asset URL]"
---

# AITOPIA: edit

Use the task-shaped media tools; each takes asset URLs (upload local files first):

- Join clips / put audio on a video / join audio files: `video_editor` (or `concat_audio`)
- Cut: `trim_video` · Resize or reframe: `resize` · Speed: `change_speed`
- Text on video: `add_text` · Logo/watermark: `overlay` · Subtitles: `subtitle`
- Fade in/out: `fade` · Mute / extract / normalize audio: `audio_tools`
- Voiceover: `add_narration` · Background music: `add_background_music` · Mix: `mix_audio_layers`, `sidechain_duck_audio`
- Still image to a moving clip: `image_to_video` · One frame: `extract_frame` · Inspect: `probe_media` · Format: `convert`

Check a clip with `probe_media` first when a tool asks whether it has audio.

## How AITOPIA works here

All work runs on your AITOPIA account through the `aitopia` MCP server's tools (`search_skills`, `generate_image`, `run_model`, …). The first call opens an AITOPIA sign-in in the browser. If those tools are not available, the AITOPIA server is not connected yet: point the user to https://github.com/AITOPIAai/skills#install (one command) and stop.

- **Start from the playbook.** Call `search_skills` with what the user wants, then `get_skill` on the best match, and follow its workflow and model guidance. The playbooks live on AITOPIA and are updated there.
- **Choose the model like AITOPIA does.** Follow the playbook; otherwise call `list_models` for the media type (add `q` with the capability or the model the user named) and pick by description. Models outside AITOPIA's recommended set need `allowAnyModel: true`, and only when the user named that model.
- **Local files.** Call `create_upload_link`, then upload with `curl -sS -T "<path>" -H "X-File-Name: <name>" "<uploadUrl>"`; the JSON reply has `assetUrl`. Never base64 a real file into a tool call. A file that is already online can go in `sourceUrl` instead.
- **Long runs (video).** `run_model` returns a `runToken`; poll `get_run_status` until it is completed or failed.
- **Results.** Give the user the file link and the `openInAitopia` link from the result. To keep a result locally, download the `assetUrl` with curl.
- **Credits.** Generation spends AITOPIA credits. Tell the user what you will make before expensive work (video, many images). If a call fails for lack of credits, give them the buy-credits link from the result instead of retrying.
