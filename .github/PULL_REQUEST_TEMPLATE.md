# Pull Request

## What changed?

Describe the change in a few concrete sentences.

## Why is this needed?

Explain the real problem or use case this solves. Avoid speculative cleanup unless it has a clear maintenance benefit.

## Validation

List the checks you ran:

- [ ] JSON manifests parse successfully (`python -m json.tool` on each manifest)
- [ ] README and README.zh-CN.md were updated if user-facing behavior, installation, publishing, or host support changed

## Skill impact

- [ ] `SKILL.md` trigger behavior is unchanged
- [ ] If `SKILL.md` changed, the new behavior remains conservative and avoids documentation churn
- [ ] New reference material is only loaded when needed

## Release notes

- [ ] `RELEASE-NOTES.md` updated, or this change does not need release notes
