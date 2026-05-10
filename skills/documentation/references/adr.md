# ADR Reference

Use an ADR for durable decisions with meaningful consequences. Do not use ADRs for routine implementation details.

## When To Record

Record a decision when it:

- affects architecture, operations, security, data model, or public contracts
- is difficult to reverse later
- introduces or removes an important dependency
- changes boundaries between modules, packages, services, or teams
- explains a tradeoff future maintainers would not infer from code alone

## Template

```md
# Decision: <title>

Date: YYYY-MM-DD
Status: proposed | accepted | deprecated | superseded by [Decision: <title>]

## Context

What problem, constraint, or opportunity led to this decision?

## Decision

What was decided?

## Consequences

What becomes easier?
What becomes harder?
What must future agents or maintainers know?

## Alternatives Considered

What other options were considered?
Why were they not chosen?
```

## Placement

- Use `docs/decisions.md` for a short running log.
- Use `docs/decisions/<date>-<slug>.md` when decisions are numerous or need richer context.
- In monorepos, put workspace-wide decisions at the root and package-local decisions inside the package.
