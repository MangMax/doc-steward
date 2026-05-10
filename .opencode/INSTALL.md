# Installing Documentation Skill for OpenCode

## Prerequisites

- OpenCode installed
- Git available on your PATH

## Installation

Add this repository to the `plugin` array in your global or project-level `opencode.json`:

```json
{
  "plugin": ["documentation-skill@git+https://github.com/<owner>/documentation-skill.git"]
}
```

Restart OpenCode after installation. OpenCode installs the plugin through its plugin manager and registers the `skills/` directory.

## Local Development

Use the local repository path while testing:

```json
{
  "plugin": ["F:/Users/Mang/Downloads/Compressed/documentation-skill"]
}
```

After loading, use OpenCode's native skill tool to confirm the `documentation` skill is available.
