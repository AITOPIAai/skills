# Contributing to AITOPIA Skills

## Git workflow

1. Branch from `main` — `feat/<short-name>`, `fix/<short-name>` or `docs/<short-name>`.
2. Keep commits focused, with a clear one-line message.
3. Open a pull request against `main`.

## PR checklist

- [ ] `claude plugin validate .` passes.
- [ ] `npx skills add ./ --list` lists every skill.
- [ ] `VERSION`, `.claude-plugin/plugin.json`, `.claude-plugin/marketplace.json`, `.codex-plugin/plugin.json`, `.cursor-plugin/plugin.json` and each `SKILL.md` `version` carry the same version.
- [ ] README skill table and INSTALL list match the `skills/` folder.
- [ ] No credentials, tokens, internal hostnames or IP addresses anywhere.
- [ ] Relevant scenarios in [`evals/scenarios.md`](./evals/scenarios.md) were run.

## Adding a new skill

1. Create `skills/aitopia-<name>/SKILL.md`. The name always starts with `aitopia-` so it never collides with other skills.
2. Frontmatter: `version`, `name`, a quoted `description` that says what it does and when to use it, and `argument-hint`.
3. Body: a short task section, then the shared **How AITOPIA works here** section (copy it from an existing skill).
4. Workflow skills stay thin: they load the matching playbook with `get_skill`. The playbook itself lives on AITOPIA, not in this repo.
5. Add the skill to the README table, the INSTALL list and a scenario in `evals/scenarios.md`.

## Updating model and workflow knowledge

Model choices and production steps belong in the AITOPIA playbooks on the server, not in these skills. Change them there; clients pick them up on the next run without a new release.

## License

By contributing you agree that your contributions are licensed under the [MIT License](./LICENSE).
