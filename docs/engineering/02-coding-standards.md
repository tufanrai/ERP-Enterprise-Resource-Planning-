# Coding Standards

> **Status:** Draft · **Owner:** Tech Lead · **Audience:** All engineers

Automate what you can (ESLint, Prettier, type checks in CI). This page covers what tools can't.

## General

- TypeScript `strict` mode. No `any` without a comment explaining why.
- Prefer small, pure functions. Name things after the business concept (`postInvoice`, not `updateStatus`).
- Use the **ubiquitous language** from the [glossary](../onboarding/02-glossary.md) in code, UI and docs.
- No dead code or commented-out code in `main`.
- Every public function in a module's `index.ts` has a doc comment.

## Module boundaries

- Import another module **only** through its `index.ts`.
- Never read or write another module's tables.
- Enforced by `eslint-plugin-boundaries` (or `dependency-cruiser`) in CI.

## Backend

- Controllers are thin: validate, call a use case, map the response.
- Business rules live in `domain/`; they must not depend on NestJS, HTTP or the database.
- Every use case that changes data runs in one transaction and writes audit entries and outbox events in it.
- Money and quantities use the shared `Money` / `Decimal` types. **Never** `number` for money.
- All dates in UTC; convert at the edges.
- Validate all input with shared schemas from `packages/contracts`.
- Log with the shared logger; never log secrets, tokens, passwords or full personal data.

## Frontend

- Server state through TanStack Query; avoid duplicating it in global state.
- Forms with React Hook Form + shared zod schemas.
- Use components from `packages/ui`; add to the design system rather than one-off styling.
- Every page must work with keyboard only and pass axe accessibility checks.
- All user-facing text through the i18n layer.

## Database

- Every change is a migration; never edit a merged migration.
- Every tenant table has `tenant_id`, an index on it and an RLS policy (checked in CI).
- Migrations must be backward compatible (expand, migrate data, contract in a later release).
- Add an index for every foreign key and common filter.

## Naming

| Thing | Convention | Example |
|---|---|---|
| Files | kebab-case | `post-invoice.use-case.ts` |
| Classes / types | PascalCase | `SalesOrder` |
| Functions / variables | camelCase | `calculateTax` |
| Constants | UPPER_SNAKE | `MAX_LINES_PER_INVOICE` |
| DB tables / columns | snake_case | `sales_order_lines.unit_price` |
| Permissions | `module.resource.action` | `inventory.stock.adjust` |
| Events | `module.PastTenseVerb` | `sales.OrderConfirmed` |
