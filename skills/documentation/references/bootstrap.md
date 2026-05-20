# Bootstrap Reference

Use this when a project has little or no documentation. Create only files that can be filled with verified project information. Replace every placeholder before finishing; if a section cannot be filled accurately, omit it or mark a specific open question.

## README Template

````md
# <Project Name>

> One-sentence description.

## Status

Current maturity and intended use.

## Installation

```sh
# verified install command
```

## Usage

```sh
# minimal working example
```

## Development

| Command | Purpose |
|---|---|
| `<command>` |  |

## Documentation

List only docs files that already exist. Omit this section if no separate docs files have been created.
````

## Getting Started Template

````md
# Getting Started

## Prerequisites

- Verified runtime or tool version

## Installation

1. Run the verified install command.
2. Configure required settings.

## First Example

```sh
# minimal working command
```

## Next Steps

- `usage.md` - common workflows
- `reference.md` - full public surface
````

## AGENTS.md Template

Create this only when the project is being bootstrapped for agent use, the user asks for it, or the project already has agent guidance.

```md
# Agent Guide

## Project Summary

Describe what this project does in 3-8 sentences.

## Current Status

State the current maturity and intended use.

## Important Commands

- Install:
- Run:
- Test:
- Lint:
- Build:
- Deploy:

## Documentation Rules

Before completing a task, check whether behavior, APIs, architecture, setup, configuration, operations, or durable project assumptions changed. Update the relevant documentation when they did.

## Coding Rules

Add project-specific coding rules.

## Testing Rules

Add project-specific testing expectations.

## Completion Checklist

- [ ] Code works
- [ ] Tests or manual verification completed
- [ ] Documentation impact checked
- [ ] Relevant docs updated
- [ ] Known issues or follow-up tasks recorded
```

## CHANGELOG Template

Create this for libraries, CLIs, packages, and release-driven projects when no changelog exists.

```md
# Changelog

All notable user-visible changes to this project will be documented in this file.

## [Unreleased]

### Added
### Changed
### Deprecated
### Removed
### Fixed
### Security
```
