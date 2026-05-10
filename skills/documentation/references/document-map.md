# Documentation Map

Use this reference when choosing where documentation belongs. Preserve an existing project structure when it is clear and useful.

Do not create every layer by default. Choose the smallest destination that keeps the current change discoverable without scattering the same information across many files.

## Common Layers

| Layer | Purpose |
|---|---|
| `README.md` | Project entry point, status, quick setup, common usage, links to deeper docs |
| `docs/getting-started.md` | Step-by-step setup and first working example |
| `docs/overview.md` | Problem, audience, scope, and high-level project shape |
| `docs/usage.md` | Common workflows and examples |
| `docs/reference.md` | APIs, CLI commands, config, env vars, schemas, file formats, errors |
| `docs/architecture.md` | System structure, module boundaries, data/control flow, key dependencies |
| `docs/development.md` | Contributor setup, scripts, testing, local workflows |
| `docs/operations.md` | Deployment, monitoring, backups, secrets, incident procedures |
| `docs/decisions.md` or `docs/decisions/*.md` | Durable decisions and tradeoffs |
| `docs/playbooks/*.md` | Repeatable operational or maintenance procedures |
| `CHANGELOG.md` | User-visible changes by version or release |
| `AGENTS.md` | Repository-specific agent rules when the project uses agent guidance |

## Small Projects

Prefer:

```txt
README.md
docs/
├── usage.md
├── reference.md
└── architecture.md
```

Only create files that contain real project information. Combine `usage.md` and `reference.md` when the public surface is small.

## Tiny Scripts

Prefer:

```txt
README.md
```

Include purpose, prerequisites, usage, examples, and caveats. Add agent guidance only if requested or already present.

## Monorepos

Prefer:

```txt
README.md
docs/
├── overview.md
├── architecture.md
└── decisions.md
packages/
└── <pkg>/
    ├── README.md
    └── CHANGELOG.md
```

Rules:

- Root README explains the workspace, shared setup, and package index.
- Root architecture docs explain cross-package relationships and shared infrastructure.
- Package READMEs explain package-specific public APIs, commands, and examples.
- Put workspace-wide decisions in root docs.
- Put package-local decisions in that package when they do not affect the whole workspace.
- Keep changelogs per package when packages are versioned independently.

## Choosing The Smallest Good Edit

- Put quick-start changes in README.
- Put exhaustive public surface details in reference docs.
- Put why and tradeoffs in architecture or decisions docs.
- Put repeatable procedures in playbooks.
- Put future work in roadmap, `docs/known-issues.md`, or an existing planning file.
- Link instead of duplicating long explanations across files.
- Avoid moving content between layers unless the current location is misleading or overloaded.
