---
version: 0.1.0
name: aitopia-short-video
description: "Produce a short-form video (TikTok, Reels, Shorts, launch or promo video) end to end with AITOPIA."
argument-hint: "[topic or script] [platform e.g. TikTok]"
---

# AITOPIA: short video

Load AITOPIA's playbook for this job with `get_skill` name `short-form-video` and follow it step by step (models, order of steps, formats). Ask the user only for what the playbook needs and they have not given (e.g. the product photo).

## How AITOPIA works here

All work runs on your AITOPIA account through the `aitopia` MCP server's tools (`search_skills`, `generate_image`, `run_model`, …). The first call opens an AITOPIA sign-in in the browser. If those tools are not available, the AITOPIA server is not connected yet: point the user to https://github.com/AITOPIAai/skills#install (one command) and stop.

- **Start from the playbook.** Call `search_skills` with what the user wants, then `get_skill` on the best match, and follow its workflow and model guidance. The playbooks live on AITOPIA and are updated there.
- **Choose the model like AITOPIA does.** Follow the playbook; otherwise call `list_models` for the media type (add `q` with the capability or the model the user named) and pick by description. Models outside AITOPIA's recommended set need `allowAnyModel: true`, and only when the user named that model.
- **Local files.** Call `create_upload_link`, then upload with `curl -sS -T "<path>" -H "X-File-Name: <name>" "<uploadUrl>"`; the JSON reply has `assetUrl`. Never base64 a real file into a tool call. A file that is already online can go in `sourceUrl` instead.
- **Long runs (video).** `run_model` returns a `runToken`; poll `get_run_status` until it is completed or failed.
- **Results.** Give the user the file link and the `openInAitopia` link from the result. To keep a result locally, download the `assetUrl` with curl.
- **Credits.** Generation spends AITOPIA credits. Tell the user what you will make before expensive work (video, many images). If a call fails for lack of credits, give them the buy-credits link from the result instead of retrying.
