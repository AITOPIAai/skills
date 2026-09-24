# Install AITOPIA Skills

Eight skills ship in this repo:

- **`aitopia-generate`** — images, video, voiceover, music and sound effects, with the model chosen for the job
- **`aitopia-edit`** — join, trim, resize, text, logo, subtitles, fades, speed, music, voiceover and audio clean-up
- **`aitopia-upload`** — send a local file to AITOPIA so any skill can use it
- **`aitopia-product-ad`**, **`aitopia-ugc-video`**, **`aitopia-short-video`**, **`aitopia-youtube-thumbnail`**, **`aitopia-brand-kit`** — AITOPIA's production playbooks, loaded from AITOPIA at run time

All of them work through the AITOPIA MCP server at `https://mcp.aitopia.ai/mcp`, on your AITOPIA account.

## Prerequisites

- An AITOPIA account — sign up at [aitopia.ai](https://aitopia.ai). Generation spends credits from it.
- Nothing to install locally. Sign-in happens in the browser the first time an AITOPIA tool runs.

## Option 1 — Claude Code marketplace (recommended for Claude Code)

```
/plugin marketplace add AITOPIAai/skills
/plugin install aitopia@aitopia
```

Installs the skills and connects the AITOPIA server.

## Option 2 — `npx skills` (cross-agent)

```bash
npx skills add AITOPIAai/skills                    # choose agents interactively
npx skills add AITOPIAai/skills --agent codex      # or target one agent
npx skills add AITOPIAai/skills --skill aitopia-generate   # or one skill
```

Then [connect the AITOPIA server](#connect-the-aitopia-server) in that agent.

## Option 3 — Codex

```bash
codex mcp add aitopia --url https://mcp.aitopia.ai/mcp
codex mcp login aitopia
npx skills add AITOPIAai/skills --agent codex
```

## Option 4 — Cursor

Install the plugin from this repo (it ships `.cursor-plugin/plugin.json` with the server), or add the server by hand and install the skills with `npx skills add AITOPIAai/skills --agent cursor`.

## Option 5 — Claude (web and desktop)

Settings → Connectors → **Add custom connector** → `https://mcp.aitopia.ai/mcp`, then sign in with AITOPIA. The skills are not needed there: the server brings AITOPIA's playbooks with it, and images and videos show inline in the conversation.

## Connect the AITOPIA server

| Client | How |
|---|---|
| Claude Code | `claude mcp add --transport http aitopia https://mcp.aitopia.ai/mcp` (the plugin does this for you) |
| Codex | `codex mcp add aitopia --url https://mcp.aitopia.ai/mcp` then `codex mcp login aitopia` |
| Cursor | Add to `~/.cursor/mcp.json`: `{"mcpServers": {"aitopia": {"url": "https://mcp.aitopia.ai/mcp"}}}` |
| Claude web / desktop | Settings → Connectors → Add custom connector |
| Any MCP client | Streamable HTTP, `https://mcp.aitopia.ai/mcp`, OAuth sign-in |

## Verify

Ask your agent: *"Use AITOPIA to generate an image of a red paper boat."* The first run opens the AITOPIA sign-in; after that you get the image, a file link and an **Open in AITOPIA** link.

In Claude Code, `/plugin` lists `aitopia` and `/mcp` shows the `aitopia` server as connected.

## Updating

- Claude Code: `/plugin marketplace update aitopia`
- `npx skills`: run the same `npx skills add AITOPIAai/skills` again

The workflow playbooks and the model choices are served by AITOPIA, so most improvements arrive without updating anything.
