# Install for Agents

Paste this file into your coding agent and ask it to set up AITOPIA. The agent should do each step, check it, and stop at the first failure with a short explanation.

## Step 1 — Connect the AITOPIA server

Add the MCP server `https://mcp.aitopia.ai/mcp` (streamable HTTP) with the command for this agent:

- Claude Code: `claude mcp add --transport http aitopia https://mcp.aitopia.ai/mcp`
- Codex: `codex mcp add aitopia --url https://mcp.aitopia.ai/mcp`
- Cursor: add `{"mcpServers": {"aitopia": {"url": "https://mcp.aitopia.ai/mcp"}}}` to `~/.cursor/mcp.json`

If an `aitopia` server already exists and points at `https://mcp.aitopia.ai/mcp` (or `/mcp/stream`), keep it and move on.

## Step 2 — Sign in

- Codex: run `codex mcp login aitopia`.
- Claude Code and Cursor: the sign-in opens in the browser on the first AITOPIA tool call (Claude Code: `/mcp` → aitopia → Authenticate).

Tell the user to finish the AITOPIA sign-in in the browser. Do not ask for their password.

## Step 3 — Install the skills

```bash
npx skills add AITOPIAai/skills --agent <this agent>
```

In Claude Code the plugin is the simpler route: `/plugin marketplace add AITOPIAai/skills` then `/plugin install aitopia@aitopia`.

## Step 4 — Install the AITOPIA CLI

Install the command-line tool too, so AITOPIA also works from the terminal and in scripts:

```bash
npm i -g aitopia
aitopia login
```

`aitopia login` opens the browser; tell the user to finish the sign-in there. Check it with `aitopia --version`. If npm is missing, skip this step and say so.

## Step 5 — Verify

Call the AITOPIA `search_skills` tool with `"product ad video"`. A list of skills means the server and sign-in work. Then confirm the `aitopia-*` skills are listed by the agent.

## Step 6 — Done

Tell the user AITOPIA is ready and suggest a first request, e.g. *"Generate four product photo options of my mug"* or *"Make a 9:16 product ad from ./product.png"*.
