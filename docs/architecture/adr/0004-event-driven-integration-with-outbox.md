# ADR-0004: Module integration through domain events and a transactional outbox

- **Status:** Proposed
- **Date:** 2026-11-26
- **Deciders:** Tech Lead

## Context

Modules must react to each other's changes (an invoice posting creates a journal entry; a goods receipt increases stock) without importing each other's internals. Events must never be lost if the process crashes after the database commit.

## Decision

- Modules publish **domain events** (e.g. `sales.InvoicePosted`).
- Events are written to an **outbox table in the same transaction** as the business change.
- An **outbox relay** worker reads unpublished rows and dispatches them to in-process handlers and to queues (webhooks, notifications, reporting).
- Handlers must be **idempotent**; each event has a unique ID and handlers record processed IDs.

## Consequences

- ✅ No lost events; loose coupling between modules.
- ✅ Same mechanism powers webhooks and audit-friendly integration.
- ⚠️ Some flows become eventually consistent (seconds). Where the user must see the result immediately, use a synchronous call to the other module's public interface inside the same transaction instead.
