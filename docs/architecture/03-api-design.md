# API Design Guidelines

> **Status:** Draft (proposed) · **Owner:** Tech Lead · **Audience:** Backend and frontend engineers, integration partners

The same REST API serves our web app and third-party integrations. It is documented with **OpenAPI 3.1**, generated from code, and published at `/docs/api` per environment.

## 1. Basics

| Topic | Rule |
|---|---|
| Base URL | `https://api.<domain>/v1` |
| Format | JSON, UTF-8. Field names in `camelCase` |
| Versioning | Major version in path (`/v1`). Additive changes do not bump the version. Breaking changes get `/v2` and a 12-month deprecation window |
| Resource naming | Plural nouns, module prefix: `/v1/sales/orders`, `/v1/finance/invoices` |
| IDs | UUID strings |
| Dates | ISO 8601 (`2026-11-26`, `2026-11-26T13:45:00Z`) |
| Money | `{ "amount": "1250.00", "currency": "USD" }` with amount as a string to avoid float errors |

## 2. Methods

| Method | Use | Example |
|---|---|---|
| GET | Read list or item | `GET /v1/inventory/products?search=chair` |
| POST | Create, or run an action | `POST /v1/sales/orders`, `POST /v1/finance/invoices/{id}/post` |
| PATCH | Partial update | `PATCH /v1/sales/customers/{id}` |
| DELETE | Delete or archive (master data only) | `DELETE /v1/sales/customers/{id}` |

State changes on documents (post, approve, cancel) are **action endpoints**, not PATCHes of a `status` field.

## 3. Authentication

- Web app: short-lived JWT access token (15 min) + HTTP-only refresh cookie.
- Integrations: API keys (`Authorization: Bearer <key>`) or OAuth2 client credentials, scoped to one tenant and a set of permissions.

## 4. Pagination, filtering, sorting

- Cursor pagination: `?limit=50&cursor=<opaque>`. Response includes `nextCursor`.
- Filters: `?status=posted&customerId=...&createdAt[gte]=2026-01-01`.
- Sort: `?sort=-createdAt,number`.

```json
{
  "data": [ { "id": "...", "number": "SO-2026-00012" } ],
  "page": { "nextCursor": "eyJpZCI6...", "limit": 50 }
}
```

## 5. Errors

Errors follow RFC 9457 (Problem Details):

```json
{
  "type": "https://docs.<domain>/errors/validation",
  "title": "Validation failed",
  "status": 422,
  "code": "VALIDATION_FAILED",
  "detail": "One or more fields are invalid.",
  "errors": [ { "field": "lines[0].quantity", "message": "Must be greater than 0" } ],
  "requestId": "req_01J..."
}
```

| Status | When |
|---|---|
| 400 | Malformed request |
| 401 | Not authenticated |
| 403 | Authenticated but not permitted |
| 404 | Not found (also used for other tenants' resources, to avoid leaking existence) |
| 409 | Conflict (version mismatch, duplicate) |
| 422 | Validation or business rule failed |
| 429 | Rate limited |
| 5xx | Server error (includes `requestId` for support) |

## 6. Concurrency and idempotency

- Editable resources return an `ETag`; updates send `If-Match` to avoid lost updates.
- POST requests accept `Idempotency-Key`; repeats within 24 hours return the original response.

## 7. Rate limits

Per API key / user, by plan (for example 600 requests per minute). Headers: `RateLimit-Limit`, `RateLimit-Remaining`, `RateLimit-Reset`.

## 8. Webhooks

- Tenants subscribe to events such as `invoice.posted`, `payment.received`, `stock.low`, `order.created`.
- Payload: `{ "id", "type", "createdAt", "tenantId", "data": {...} }`.
- Signed with HMAC-SHA256 in the `Webhook-Signature` header.
- Retried with exponential backoff for up to 24 hours; delivery log visible to the tenant.

## 9. API review checklist

- [ ] Endpoint follows naming and method rules
- [ ] Permission defined and enforced
- [ ] Request validated; errors use Problem Details
- [ ] Paginated if it returns a list
- [ ] OpenAPI annotations complete with examples
- [ ] Tenant isolation test added
- [ ] Backward compatible, or a new version planned
