# CLAUDE.md — AITOPIA Skills

## What this is

Agent skills and plugin manifests for AITOPIA — image, video, voice and music creation and media editing on a user's AITOPIA account. The skills are thin: all work goes through the AITOPIA MCP server (`https://mcp.aitopia.ai/mcp`), and the detailed production playbooks are served by AITOPIA at run time (`search_skills` / `get_skill`), not stored here.

## Repository structure

```
.claude-plugin/     plugin.json + marketplace.json (Claude Code)
.codex-plugin/      plugin.json (Codex) → skills/ and .mcp.json
.cursor-plugin/     plugin.json (Cursor) → skills/ and .mcp.json
.mcp.json           the AITOPIA MCP server (shared by all three)
skills/aitopia-*/   one SKILL.md per skill
assets/             logo.png (400×400), icon.png (128×128)
evals/              scenarios to run before a release
VERSION             single source of the version
```

## API conventions

- Tools come from the AITOPIA MCP server; never hard-code tool name prefixes (`mcp__…`) — they differ per client.
- Local files: `create_upload_link`, then `curl -T` to the returned URL. Never base64 a real file into a tool call.
- Long runs: `run_model` returns a `runToken`; poll `get_run_status`.
- Models: follow the playbook or `list_models`; models outside AITOPIA's recommended set need `allowAnyModel: true`, only when the user named that model.

## Self-contained skills

Every `SKILL.md` carries the shared **How AITOPIA works here** section, so a skill installed alone (e.g. with `npx skills --skill`) still works.

## Version sync

Bump `VERSION` and the same number in the three plugin manifests, `marketplace.json` and every `SKILL.md`.

## Adding a new skill

See [CONTRIBUTING.md](./CONTRIBUTING.md#adding-a-new-skill).

## Eval discipline

Before a release, run the scenarios in [`evals/scenarios.md`](./evals/scenarios.md) on a real AITOPIA test account and record the result in the round log (see [`evals/README.md`](./evals/README.md)).

## Never commit

Credentials, tokens, user data, internal hostnames or IP addresses.
