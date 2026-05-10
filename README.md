# Documentation Skill

This repository packages a reusable Agent Skill for project documentation maintenance. It helps coding agents keep documentation accurate after meaningful changes without creating documentation churn.

## Install

### As a Codex plugin

Install from this repository once it is published:

```txt
/plugins
```

Search for `documentation-skill`, or install from your GitHub fork if your Codex environment supports repository plugin installs.

### As a project-local skill

Copy the `skills/documentation/` directory into your project:

```txt
your-project/
└── skills/
    └── documentation/
        └── SKILL.md
```

### As a global skill

Copy `skills/documentation/` into your Codex skills directory:

```txt
$CODEX_HOME/skills/documentation/
```

If `CODEX_HOME` is not set, use the default Codex skills directory for your system.

## Recommended AGENTS.md / CLAUDE.md instruction

Add this line to your project-level agent instructions:

```md
Use the documentation skill before completing tasks that may change public behavior, APIs, CLI commands, configuration, setup, architecture, deployment, operations, or durable project decisions.
```

## Purpose

The skill helps an AI agent:

- bootstrap documentation for empty projects
- keep README and docs synchronized with code
- update docs after features, refactors, API changes, config changes, and deployment changes
- avoid documentation churn for purely internal or mechanical changes
- record architecture decisions
- summarize documentation changes before finishing a task

## Contents

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

## Validation

Validate the skill metadata before publishing:

```sh
python path/to/skill-creator/scripts/quick_validate.py skills/documentation
```

The plugin manifest lives in `.codex-plugin/plugin.json`. After creating the GitHub repository, you can add `homepage`, `repository`, and `interface.websiteURL` fields with the final repository URL.

## Supported Agent Hosts

This repository includes lightweight plugin or extension metadata for:

- Codex: `.codex-plugin/plugin.json`
- Claude Code: `.claude-plugin/plugin.json`
- Cursor: `.cursor-plugin/plugin.json`
- Gemini CLI: `gemini-extension.json` and `GEMINI.md`
- OpenCode: `package.json`, `.opencode/plugins/documentation-skill.js`, and `.opencode/INSTALL.md`

Replace the placeholder GitHub URL in `.opencode/INSTALL.md` after the repository is published.
