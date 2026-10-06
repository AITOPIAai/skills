# AITOPIA

The `aitopia` MCP server makes images, video, speech, music and sound on the user's AITOPIA account, and edits media files (upscale, remove background, reframe, trim, subtitles, narration, music, merges).

- The first call opens AITOPIA sign-in in the browser.
- Generation spends the user's AITOPIA credits. Before anything expensive (video, many images, long audio) say what you will make and roughly what it costs; most tools take `dryRun: true` to price a call without running it.
- For a workflow (product ad, UGC video, short-form video, YouTube thumbnail, brand kit), follow the matching playbook in `skills/<name>/SKILL.md` of this extension, or call the server's `search_skills` / `get_skill` tools.
- Local files: upload them first with `upload_asset` or `create_upload_link`, then pass the returned URL.
