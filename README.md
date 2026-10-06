# AITOPIA Skills

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](./LICENSE)
[![Version](https://img.shields.io/badge/version-0.1.0-green.svg)](./VERSION)
[![Skills](https://img.shields.io/badge/skills-8-9334EA.svg)](#skills)

AI agent skills for creating and editing images, video, voiceovers and music with [AITOPIA](https://aitopia.ai) — plus AITOPIA's production playbooks for product ads, UGC videos, short-form videos, YouTube thumbnails and brand kits. Works with Claude Code, Codex, Cursor and other agents that load Markdown skills, and with any MCP client through the AITOPIA server.

Everything runs on your AITOPIA account through the AITOPIA MCP server (`https://mcp.aitopia.ai/mcp`). There is nothing to install locally: the first AITOPIA action opens a browser sign-in, and every result is saved to your account, where you can keep working on it.

## Install

Pick one. The plugin installs (Claude Code, Codex, Cursor) connect the AITOPIA server for you.

### Claude Code marketplace — recommended for Claude Code

```
/plugin marketplace add AITOPIAai/skills
/plugin install aitopia@aitopia
```

### `npx skills` — cross-agent

```bash
npx skills add AITOPIAai/skills
```

Installs the skills into Claude Code, Codex, Cursor and [many other agents](https://github.com/vercel-labs/skills#supported-agents). Connect the AITOPIA server once as well (see [INSTALL.md](./INSTALL.md#connect-the-aitopia-server)).

### Codex

```bash
codex mcp add aitopia --url https://mcp.aitopia.ai/mcp
codex mcp login aitopia
npx skills add AITOPIAai/skills --agent codex
```

### One-click: Cursor, VS Code, Gemini CLI

[![Add to Cursor](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/en/install-mcp?name=aitopia&config=eyJ1cmwiOiJodHRwczovL21jcC5haXRvcGlhLmFpL21jcCJ9)
[![Install in VS Code](https://img.shields.io/badge/VS_Code-Install_AITOPIA-0098FF?logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect/mcp/install?name=aitopia&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A//mcp.aitopia.ai/mcp%22%7D)

Gemini CLI (server + playbooks):

```bash
gemini extensions install https://github.com/AITOPIAai/skills
```

Any other MCP client: add the remote server `https://mcp.aitopia.ai/mcp` (Streamable HTTP, OAuth sign-in).

### Claude (web and desktop)

Settings → Connectors → **Add custom connector** → `https://mcp.aitopia.ai/mcp`, then sign in with AITOPIA. Generated images and videos show inline in the conversation.

More options in [INSTALL.md](./INSTALL.md). Agent-driven install (paste into your agent): [INSTALL_FOR_AGENTS.md](./INSTALL_FOR_AGENTS.md).

## Skills

| Skill | What it does |
|---|---|
| [`aitopia-generate`](./skills/aitopia-generate)<br>`/aitopia:aitopia-generate` | Images, video, voiceover, music and sound effects. Picks the model for the job the way AITOPIA does; several images come back together in one call. |
| [`aitopia-edit`](./skills/aitopia-edit)<br>`/aitopia:aitopia-edit` | Join clips, add voiceover or music, trim, resize to 9:16 / 16:9 / 1:1, text and logo overlays, subtitles, fades, speed changes, mute / extract / normalize audio, animate a still image. |
| [`aitopia-upload`](./skills/aitopia-upload)<br>`/aitopia:aitopia-upload` | Send a local photo, video, audio file or document to AITOPIA (up to 95 MB; 200 MB from a public URL). |
| [`aitopia-product-ad`](./skills/aitopia-product-ad)<br>`/aitopia:aitopia-product-ad` | Product commercial from a product photo: hero keyframe, motion, voiceover, music. |
| [`aitopia-ugc-video`](./skills/aitopia-ugc-video)<br>`/aitopia:aitopia-ugc-video` | Creator-style UGC ad — testimonial, before/after, hook video, phone-shot feel. |
| [`aitopia-short-video`](./skills/aitopia-short-video)<br>`/aitopia:aitopia-short-video` | TikTok / Reels / Shorts, launch and promo videos end to end. |
| [`aitopia-youtube-thumbnail`](./skills/aitopia-youtube-thumbnail)<br>`/aitopia:aitopia-youtube-thumbnail` | High click-through YouTube thumbnails: bold subject, contrast, big readable text. |
| [`aitopia-brand-kit`](./skills/aitopia-brand-kit)<br>`/aitopia:aitopia-brand-kit` | Logo direction, color palette, typography and usage rules. |

The second line is the command in the Claude Code plugin; with `npx skills` the command is the skill name, e.g. `/aitopia-generate`.

Agents also use the skills on their own when a request fits. The playbooks behind the workflow skills live on AITOPIA and are loaded at run time, so they improve without reinstalling anything.

The skills chain: `aitopia-upload` turns a local file into an asset URL that every other skill accepts; `aitopia-generate` produces the stills and clips that `aitopia-edit` assembles; the workflow skills (`product-ad`, `ugc-video`, `short-video`, `youtube-thumbnail`, `brand-kit`) drive both.

## Quick Reference

| What you want | Skill | Note |
|---|---|---|
| An image, or several options of one | `aitopia-generate` | Up to 4 images in one call, shown side by side |
| A short video from a prompt or a photo | `aitopia-generate` | Long runs finish in the background; the result appears when ready |
| Voiceover, music or a sound effect | `aitopia-generate` | Voice and music use different models |
| Use a photo or video from your computer | `aitopia-upload` | Then pass the asset URL to any skill |
| Join clips, add music or voiceover | `aitopia-edit` | `video_editor` also joins audio files end to end |
| Reframe for Reels / TikTok / YouTube | `aitopia-edit` | `resize` with fit cover / contain |
| Titles, captions, logo, subtitles | `aitopia-edit` | `add_text`, `overlay`, `subtitle` |
| Remove a background, upscale, restore | `aitopia-generate` | AITOPIA picks a suitable model or store agent |
| Product commercial | `aitopia-product-ad` | Starts from the product photo |
| UGC ad | `aitopia-ugc-video` | Creator-style, phone-shot feel |
| YouTube thumbnail | `aitopia-youtube-thumbnail` | Several variants to choose from |
| Brand identity | `aitopia-brand-kit` | Logo direction, palette, type |

Recipes that combine skills: [COOKBOOK.md](./COOKBOOK.md).

## Credits

Generation spends AITOPIA credits from your account; editing and uploads are cheap or free. If a run needs more credits, the result links to [aitopia.ai/pricing](https://aitopia.ai/pricing).

## License

MIT — see [LICENSE](./LICENSE).
