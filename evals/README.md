# Evals

## Why

The skills are short, so what matters is behaviour: does the agent load the right playbook, choose a sensible model, upload local files the right way, and hand back usable links. These scenarios catch regressions in that behaviour.

## How

Run each scenario in [`scenarios.md`](./scenarios.md) with the plugin installed and a real AITOPIA test account. Check every **Expect** line. Log the round below.

## Round vs scenario

- A **scenario** is one request with its expectations.
- A **round** is one pass over all scenarios for a given version and client (Claude Code, Codex, Cursor, Claude web).

## When to add new scenarios

Whenever a skill is added, a bug is fixed, or a client behaves differently from the others.

## Round template

```
Version: 0.1.0   Client: Claude Code 2.x   Date: YYYY-MM-DD   Account: test
S1 ✅  S2 ✅  S3 ❌ (note)  …
```
