# Documentation Skill

[中文说明](README.zh-CN.md)

Documentation Skill is a focused Agent Skill for keeping project documentation accurate after meaningful code, API, setup, architecture, and operations changes.

It is designed for coding agents that already work inside a repository and need a lightweight, production-friendly way to decide when docs should change, which docs should change, and when leaving docs alone is the right call.

## Quickstart

Install the plugin or copy the skill into your agent's skills directory, then add this instruction to your project-level agent guidance:

```md
Use the documentation skill before completing tasks that may change public behavior, APIs, CLI commands, configuration, setup, architecture, deployment, operations, or durable project decisions.
```

The skill will not try to rewrite your whole documentation set. It checks whether the current task affects documentation, updates only the relevant files, and explicitly reports when no documentation changes were needed.

## How It Works

The skill asks three questions before a task is finished:

1. Did an interface change? Public behavior, APIs, routes, CLI commands, config, env vars, schemas, file formats, installation, or usage.
2. Did structure change? Architecture, module responsibilities, dependency boundaries, deployment, operations, or contributor workflow.
3. Did project knowledge change? Durable decisions, tradeoffs, limitations, or technical debt that future maintainers should know.

If the answer is yes, the agent updates the smallest relevant documentation surface. If the answer is no, the agent leaves docs alone and says so.

## Installation

Installation differs by agent host. If you use more than one host, install the plugin separately for each one.

### Codex

This repository includes Codex plugin metadata at `.codex-plugin/plugin.json`.

After publishing the repository, install it through your Codex plugin workflow or copy the skill directly:

```txt
$CODEX_HOME/skills/documentation/
```

If `CODEX_HOME` is not set, use the default Codex skills directory for your system.

### Claude Code

This repository includes Claude plugin metadata at `.claude-plugin/plugin.json`.

Install from your GitHub repository when your Claude Code environment supports repository plugins, or copy `skills/documentation/` into your Claude skills directory.

### Cursor

This repository includes Cursor plugin metadata at `.cursor-plugin/plugin.json`.

The manifest points Cursor at:

```txt
./skills/
```

### Gemini CLI

This repository includes:

```txt
gemini-extension.json
GEMINI.md
```

`GEMINI.md` loads the documentation skill directly:

```md
@./skills/documentation/SKILL.md
```

### OpenCode

This repository includes an OpenCode plugin entrypoint:

```txt
package.json
.opencode/plugins/documentation-skill.js
.opencode/INSTALL.md
```

For a published repository, add this to your `opencode.json`:

```json
{
  "plugin": ["documentation-skill@git+https://github.com/<owner>/documentation-skill.git"]
}
```

For local testing, point OpenCode at this repository path. See `.opencode/INSTALL.md` for details.

### Project-Local Skill

For any host that supports local skills, copy the skill directory into your project:

```txt
your-project/
└── skills/
    └── documentation/
        ├── SKILL.md
        ├── agents/
        └── references/
```

## What It Updates

The skill is intentionally conservative. It favors surgical edits over broad rewrites and avoids documentation churn for internal-only or mechanical changes.

Typical updates include:

- README quickstart, setup, usage, or documentation index changes
- Reference docs for public APIs, CLI commands, config, env vars, schemas, file formats, and errors
- Architecture docs when module boundaries, dependencies, or data flow change
- Changelog or release notes for user-visible releases, breaking changes, and deprecations
- ADRs only for durable decisions with meaningful tradeoffs
- Playbooks for repeatable operational or maintenance procedures
- Agent guidance when repository-specific agent rules already exist or are explicitly requested

## What's Inside

```txt
.claude-plugin/
└── plugin.json
.codex-plugin/
└── plugin.json
.cursor-plugin/
└── plugin.json
.opencode/
├── INSTALL.md
└── plugins/
    └── documentation-skill.js
gemini-extension.json
GEMINI.md
package.json
skills/documentation/
├── SKILL.md
├── agents/openai.yaml
└── references/
    ├── adr.md
    ├── bootstrap.md
    ├── document-map.md
    └── templates.md
```

`SKILL.md` contains the core workflow and guardrails. The `references/` files are loaded only when the agent needs more detail, keeping the main skill lightweight.

## Design Principles

- Evidence over invention: documentation must come from code, config, tests, examples, release metadata, existing docs, or explicit user instructions.
- Smallest useful edit: update the narrowest documentation surface that keeps the project accurate.
- No empty docs: do not create placeholder files, blank sections, blank tables, or speculative roadmap items.
- Respect existing structure: preserve the project's current documentation style when it is coherent.
- Production safety: do not document secrets, private credentials, internal tokens, or sensitive customer data.

## Validation

Validate the skill metadata before publishing:

```sh
python path/to/skill-creator/scripts/quick_validate.py skills/documentation
```

You can also sanity-check JSON manifests:

```sh
python -m json.tool .codex-plugin/plugin.json
python -m json.tool .claude-plugin/plugin.json
python -m json.tool .cursor-plugin/plugin.json
python -m json.tool gemini-extension.json
python -m json.tool package.json
```

## Publishing Checklist

Before publishing this repository to GitHub:

- Replace `<owner>` in `.opencode/INSTALL.md` with the final GitHub owner or organization.
- Add `homepage`, `repository`, and `interface.websiteURL` to `.codex-plugin/plugin.json` if your distribution flow expects them.
- Choose and add a license before inviting external reuse.
- Install in at least one target host and confirm the `documentation` skill is discovered.
- Run the validation commands above.

## License

No license has been selected yet. Add a license before publishing if other people should be allowed to use, modify, or redistribute this skill.
