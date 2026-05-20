# Doc Steward Contributor Guide

## Project Purpose

This repository packages a single Agent Skill named `documentation` for multiple coding-agent hosts. The skill helps agents keep project documentation accurate after meaningful changes while avoiding documentation churn.

Keep the repository small, dependency-light, and easy to install from GitHub.

## Important Files

- `skills/documentation/SKILL.md` - core skill metadata, workflow, and guardrails.
- `skills/documentation/references/` - optional supporting references loaded only when needed.
- `skills/documentation/agents/openai.yaml` - UI metadata for Codex-style skill listings.
- `.codex-plugin/plugin.json` - Codex plugin manifest.
- `.claude-plugin/plugin.json` - Claude plugin manifest.
- `.cursor-plugin/plugin.json` - Cursor plugin manifest.
- `gemini-extension.json` and `GEMINI.md` - Gemini extension entrypoint.
- `package.json` and `.opencode/plugins/doc-steward.js` - OpenCode plugin entrypoint.
- `README.md` and `README.zh-CN.md` - English and Chinese user-facing documentation.
- `RELEASE-NOTES.md` - release history for published versions.
- `.github/PULL_REQUEST_TEMPLATE.md` - contributor checklist for pull requests.

## Skill Editing Rules

- Keep `SKILL.md` focused on the core workflow. Move detailed templates or reference material into `references/`.
- Preserve the conservative behavior: check documentation impact, update only relevant docs, and avoid churn for internal-only or mechanical changes.
- Do not add empty placeholder docs, speculative claims, or unverified installation instructions.
- Keep the `description` frontmatter trigger-oriented and concise. It should start with `Use when...`.
- Maintain compatibility with the Agent Skills spec: the skill directory name and frontmatter `name` must both be `documentation`.
- Do not add runtime dependencies unless they are required for a host integration and documented clearly.

## Validation

After changing plugin manifests, validate JSON:

```sh
python -m json.tool .codex-plugin/plugin.json
python -m json.tool .claude-plugin/plugin.json
python -m json.tool .cursor-plugin/plugin.json
python -m json.tool gemini-extension.json
python -m json.tool package.json
```

If you change the OpenCode plugin, inspect `.opencode/plugins/doc-steward.js` manually and test plugin discovery in OpenCode when possible.

## Documentation Rules

- Keep English and Chinese READMEs aligned when changing installation, publishing, licensing, or host support.
- Do not duplicate long skill internals in README files. The README should explain value, installation, contents, validation, and publishing.
- Keep `.opencode/INSTALL.md` synchronized with the OpenCode section in the README.
- If the GitHub repository URL changes, update `.opencode/INSTALL.md` and any manifest URL fields that are later added.
- Update `RELEASE-NOTES.md` for user-facing changes, host support changes, publishing changes, or skill behavior changes.

## Publishing Checklist

Before publishing or tagging a release:

- Run the validation commands above.
- Confirm `git status` is clean.
- Confirm the GitHub URL in `.opencode/INSTALL.md`, `.codex-plugin/plugin.json`, and `package.json` is current.
- Confirm `LICENSE` matches manifest license fields.
- Install in at least one target host and verify the `documentation` skill is discoverable.
- Tag the release with the version documented in `RELEASE-NOTES.md`.
