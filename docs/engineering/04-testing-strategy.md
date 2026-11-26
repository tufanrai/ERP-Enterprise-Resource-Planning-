# Testing Strategy

> **Status:** Draft · **Owner:** QA Lead / Tech Lead · **Audience:** Engineers, QA

## Test pyramid

| Level | What | Tools | Target |
|---|---|---|---|
| Unit | Domain rules, calculations (tax, valuation, payroll) | Vitest/Jest | Fast, most tests here; 80%+ coverage on `domain/` |
| Integration | Use cases with a real PostgreSQL, repositories, RLS | Testcontainers | Every use case |
| API / contract | Endpoints, validation, permissions, error shapes | Supertest, OpenAPI validation | Every endpoint |
| Tenant isolation | Tenant A cannot read or change tenant B data | Custom suite | Every endpoint, required in CI |
| End to end | Critical journeys in a browser (sign up → invoice, order to cash) | Playwright | Top 10–20 journeys |
| Performance | Load on key endpoints and reports | k6 | Before each phase release |
| Security | SAST, dependency, container scans; pen test | CodeQL/Semgrep, Dependabot/Snyk, Trivy | Every PR; pen test yearly |
| Accessibility | WCAG checks | axe + Playwright | Every page |

## Special focus: accounting correctness

- Property-based tests (e.g. fast-check) assert that **every** generated business document produces balanced journal entries.
- Golden-file tests for financial reports against hand-checked spreadsheets.
- An accountant reviews report outputs before each release that touches finance.

## Test data

- Factories in `packages/testing` build valid entities.
- Seed data provides a demo tenant per industry template.
- Never copy production data to lower environments; use synthetic data.

## When tests run

| Trigger | Suites |
|---|---|
| Every push / PR | Lint, types, unit, integration, API, isolation, security scans |
| Merge to `main` | All of the above + E2E on staging |
| Nightly | Full E2E, accessibility, dependency audit |
| Before phase release | Performance tests, manual exploratory testing, UAT with pilot customers |
