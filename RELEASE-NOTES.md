# Doc Steward Release Notes

## v0.1.0 (2026-05-10)

Initial public release.

### Added

- `documentation` Agent Skill with conservative documentation-impact checks.
- Reference files for documentation mapping, bootstrap templates, ADR guidance, and reusable document templates.
- Codex, Claude Code, Cursor, Gemini CLI, and OpenCode plugin or extension entrypoints.
- English and Chinese README files.
- MIT license.
- Agent contributor guidance through `CLAUDE.md` and `AGENTS.md`.

### Notes

- The skill intentionally avoids hooks and runtime enforcement. It is designed to guide documentation updates without hidden automation or documentation churn.
- OpenCode installation still requires replacing `<owner>` in `.opencode/INSTALL.md` after the GitHub repository is created.
