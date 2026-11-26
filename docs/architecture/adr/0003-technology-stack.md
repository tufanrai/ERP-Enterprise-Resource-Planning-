# ADR-0003: TypeScript stack — Next.js, NestJS, PostgreSQL

- **Status:** Accepted (2026-11-26)
- **Date:** 2026-11-26
- **Deciders:** Tech Lead, engineering team

## Context

We need a stack that a small team can be productive in, that is easy to hire for, and that suits data-heavy business applications.

## Decision

| Layer | Choice | Why |
|---|---|---|
| Language | TypeScript everywhere | One language for frontend and backend, shared types, large talent pool |
| Frontend | Next.js (React), TanStack Query, Tailwind CSS, a component library (e.g. shadcn/ui) | Mature ecosystem, good for complex forms and tables |
| Backend | Node.js LTS + NestJS | Opinionated modular structure that fits ADR-0001, dependency injection, good testing support |
| ORM / queries | Prisma or Drizzle (decide in spike) | Type-safe queries and migrations |
| Database | PostgreSQL 16 | Strong transactions, `numeric` money type, RLS, JSONB |
| Cache / queues | Redis + BullMQ | Simple, reliable background jobs |
| Monorepo | pnpm workspaces + Turborepo | Shared packages, fast cached builds |
| Testing | Vitest/Jest, Supertest, Playwright, Testcontainers | Unit, API, E2E with real PostgreSQL |
| Infra | Docker and Docker Compose; hosting per [ADR-0005](0005-mvp-hosting-without-aws.md) (no AWS for the MVP) | Portable, cheap and simple for a small team |
| CI/CD | GitHub Actions | Close to the code, free tier for start |

## Alternatives considered

- **Java/Spring or .NET:** excellent for enterprise, but slower iteration for a small team and two languages across the stack.
- **Python/Django:** fast to build, but a split language stack and weaker typing across the frontend boundary.
- **Go:** great performance, but less productive for large CRUD and business-rule-heavy domains.

## Consequences

- ✅ Shared types and validation schemas between frontend and backend.
- ⚠️ Node is single-threaded; heavy computation (large reports, payroll) runs in workers.
- ⚠️ Decimal math must use a decimal library (e.g. `decimal.js`), never JavaScript `number`, for money.
