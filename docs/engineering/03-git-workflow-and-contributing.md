# Git Workflow and Contributing

> **Status:** Draft · **Owner:** Tech Lead · **Audience:** All engineers

## Branching (trunk-based)

- `main` is always deployable and protected.
- Create short-lived branches from `main`: `feat/<ticket>-short-name`, `fix/<ticket>-short-name`, `chore/...`, `docs/...`.
- Keep branches small and merge within 1–3 days. Use feature flags for unfinished work.

## Commits

Use [Conventional Commits](https://www.conventionalcommits.org):

```
feat(sales): allow converting a quote to a sales order
fix(finance): reject journal entries in locked periods
docs(architecture): add ADR-0005 on reporting read models
```

## Pull requests

1. Open a PR early (draft is fine).
2. Fill in the PR template: what, why, how tested, screenshots for UI, migration notes.
3. CI must pass: lint, type check, tests, security scans.
4. At least **one approving review**; **two** for changes to auth, permissions, tenancy, money calculations or migrations.
5. Squash-merge into `main`. The PR title becomes the commit message.

## Code review guidelines

Reviewers check:
- Does it do what the ticket asks? Are edge cases covered?
- Tests present and meaningful?
- Module boundaries respected? Tenant isolation preserved?
- Security: input validation, permissions, no secrets logged.
- Readable naming; docs and ADRs updated if behaviour or architecture changed.

Be kind and specific. Prefix optional comments with **nit:**.

## Definition of done

- [ ] Acceptance criteria met
- [ ] Unit/integration tests added and passing
- [ ] Permissions and audit logging in place for new actions
- [ ] API documented (OpenAPI) if endpoints changed
- [ ] User-facing text translated keys added
- [ ] Docs updated (feature catalog, ADR, runbook) where relevant
- [ ] Deployed to staging and verified
