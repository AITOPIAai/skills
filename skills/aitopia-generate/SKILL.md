---
version: 0.1.0
name: aitopia-generate
description: "Generate images, video, voiceover, music or sound effects with AITOPIA. Use when the user asks to create, draw, render or animate something (e.g. \"make an image of…\", \"a 5 second video of…\", \"a voiceover for…\")."
argument-hint: "[what to make] [--image|--video|--audio] [--model <name>]"
---

# AITOPIA: generate

Make the image, video or audio the user asked for.

1. Call `search_skills` with the request in the user's words and load the best match with `get_skill`.
2. Images: `generate_image` with the chosen `selectedModelId`. For several images use one call with `count` (variations) or `prompts` (up to 4 different ones).
3. Voice, music, sound effects: `generate_audio` with the chosen model.
4. Video: `run_model` with a video model from the playbook or `list_models` (type `video`), then poll `get_run_status`.
5. Report what was made, with the links.

## How AITOPIA works here

All work runs on your AITOPIA account through the `aitopia` MCP server's tools (`search_skills`, `generate_image`, `run_model`, …). The first call opens an AITOPIA sign-in in the browser. If those tools are not available, the AITOPIA server is not connected yet: point the user to https://github.com/AITOPIAai/skills#install (one command) and stop.

- **Start from the playbook.** Call `search_skills` with what the user wants, then `get_skill` on the best match, and follow its workflow and model guidance. The playbooks live on AITOPIA and are updated there.
- **Choose the model like AITOPIA does.** Follow the playbook; otherwise call `list_models` for the media type (add `q` with the capability or the model the user named) and pick by description. Models outside AITOPIA's recommended set need `allowAnyModel: true`, and only when the user named that model.
- **Local files.** Call `create_upload_link`, then upload with `curl -sS -T "<path>" -H "X-File-Name: <name>" "<uploadUrl>"`; the JSON reply has `assetUrl`. Never base64 a real file into a tool call. A file that is already online can go in `sourceUrl` instead.
- **Long runs (video).** `run_model` returns a `runToken`; poll `get_run_status` until it is completed or failed.
- **Results.** Give the user the file link and the `openInAitopia` link from the result. To keep a result locally, download the `assetUrl` with curl.
- **Credits.** Generation spends AITOPIA credits. Tell the user what you will make before expensive work (video, many images). If a call fails for lack of credits, give them the buy-credits link from the result instead of retrying.
