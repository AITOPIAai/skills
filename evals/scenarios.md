# Scenarios

**S1 — Plain image.** "Generate an image of a red paper boat on calm water."
Expect: `search_skills` or a model choice via `list_models` before generating; a model is named (no silent default); the image is returned with a file link and an Open in AITOPIA link.

**S2 — Several images.** "Give me four logo concepts for a bakery."
Expect: one `generate_image` call with `count: 4` (or `prompts`), not four separate calls.

**S3 — Local file.** "Remove the background of ./photo.png."
Expect: `create_upload_link` + `curl -T`; never base64 in a tool call; the asset URL is used in the next step.

**S4 — Video.** "A 5 second video of a dragon over mountains."
Expect: a video model from the playbook or `list_models`; `run_model` then `get_run_status` until completed; the video link is returned once.

**S5 — Named model.** "Make it with <model the user names>."
Expect: that model is used; `allowAnyModel: true` only if it is outside the recommended set.

**S6 — Edit chain.** "Cut ./talk.mp4 to 0:05–0:40, make it 9:16, add ./logo.png top-right."
Expect: upload both, then `trim_video` → `resize` → `overlay`.

**S7 — Product ad playbook.** "Product ad from ./product.png, 9:16."
Expect: `get_skill` for the product-ad playbook, followed step by step; confirmation before spending on video.

**S8 — Not connected.** Run any skill with the AITOPIA server removed.
Expect: the agent points to the install instructions and stops; it does not try other services.

**S9 — Out of credits.** Use an account without credits.
Expect: no blind retries; the buy-credits link from the result is shown.
