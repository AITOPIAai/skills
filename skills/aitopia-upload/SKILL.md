---
version: 0.1.0
name: aitopia-upload
description: "Upload a local file (photo, video, audio, document) to AITOPIA so AITOPIA tools can use it. Use when the user points at a file on their computer for an AITOPIA job, e.g. \"remove the background of ./photo.png\"."
argument-hint: "[local file path]"
---

# AITOPIA: upload

1. `create_upload_link` (optionally with `fileName`).
2. `curl -sS -T "<local path>" -H "X-File-Name: <file name>" "<uploadUrl>"` — up to 95 MB. For bigger files that are online, pass `sourceUrl` to `create_upload_link` instead (up to 200 MB).
3. Use the returned `assetUrl` in the next tool call.

## How AITOPIA works here

All work runs on your AITOPIA account through the `aitopia` MCP server's tools (`search_skills`, `generate_image`, `run_model`, …). The first call opens an AITOPIA sign-in in the browser. If those tools are not available, the AITOPIA server is not connected yet: point the user to https://github.com/AITOPIAai/skills#install (one command) and stop.

- **Start from the playbook.** Call `search_skills` with what the user wants, then `get_skill` on the best match, and follow its workflow and model guidance. The playbooks live on AITOPIA and are updated there.
- **Choose the model like AITOPIA does.** Follow the playbook; otherwise call `list_models` for the media type (add `q` with the capability or the model the user named) and pick by description. Models outside AITOPIA's recommended set need `allowAnyModel: true`, and only when the user named that model.
- **Local files.** Call `create_upload_link`, then upload with `curl -sS -T "<path>" -H "X-File-Name: <name>" "<uploadUrl>"`; the JSON reply has `assetUrl`. Never base64 a real file into a tool call. A file that is already online can go in `sourceUrl` instead.
- **Long runs (video).** `run_model` returns a `runToken`; poll `get_run_status` until it is completed or failed.
- **Results.** Give the user the file link and the `openInAitopia` link from the result. To keep a result locally, download the `assetUrl` with curl.
- **Credits.** Generation spends AITOPIA credits. Tell the user what you will make before expensive work (video, many images). If a call fails for lack of credits, give them the buy-credits link from the result instead of retrying.
