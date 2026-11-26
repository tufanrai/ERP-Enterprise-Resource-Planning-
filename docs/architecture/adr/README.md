# Architecture Decision Records (ADRs)

An ADR records one significant technical decision: the context, the choice and its consequences. ADRs let new team members understand **why** the system looks the way it does without asking the people who were there.

## Rules

- One decision per file, numbered in order: `NNNN-short-title.md`.
- Copy [`0000-template.md`](0000-template.md) to start a new one.
- Status is one of: **Proposed**, **Accepted**, **Deprecated**, **Superseded by ADR-XXXX**.
- Accepted ADRs are not edited. To change a decision, write a new ADR that supersedes the old one.
- Open the ADR as a pull request; the Tech Lead approves.

## Index

| ADR | Title | Status |
|---|---|---|
| [0001](0001-modular-monolith.md) | Start as a modular monolith | Proposed |
| [0002](0002-multi-tenancy-strategy.md) | Shared-schema multi-tenancy with PostgreSQL row-level security | Proposed |
| [0003](0003-technology-stack.md) | TypeScript stack: Next.js, NestJS, PostgreSQL | Proposed |
| [0004](0004-event-driven-integration-with-outbox.md) | Module integration through domain events and a transactional outbox | Proposed |
