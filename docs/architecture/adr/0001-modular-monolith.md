# ADR-0001: Start as a modular monolith

- **Status:** Proposed
- **Date:** 2026-11-26
- **Deciders:** Tech Lead, engineering team

## Context

An ERP has many tightly related domains (finance, inventory, sales). Many business operations touch several of them in one transaction (for example, a delivery updates stock and posts cost of goods sold). The team is small, and speed of delivery matters more than independent scaling at launch.

## Options considered

1. **Microservices from day one.** Independent deploys and scaling, but distributed transactions, more infrastructure, slower development and harder debugging for a small team.
2. **Traditional monolith.** Fast to start, but tends to become tangled and hard to split later.
3. **Modular monolith.** One deployable with strictly separated modules, each owning its data and exposing a public interface.

## Decision

Build a **modular monolith** (option 3). Each module lives in `apps/api/src/modules/<name>`, owns its own database schema and exposes only what is exported from its `index.ts`. Cross-module communication uses public service interfaces or domain events ([ADR-0004](0004-event-driven-integration-with-outbox.md)). Boundaries are enforced with lint rules in CI.

## Consequences

- ✅ Simple deployment, local development and debugging.
- ✅ Real database transactions where they are needed.
- ✅ A clear path to extract a module into a service later.
- ⚠️ Discipline needed to keep boundaries. Lint rules and code review are required.
- ⚠️ The whole backend scales as one unit until modules are extracted.
