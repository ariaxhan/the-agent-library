---
name: design-api-contracts
description: Design or review API contracts for HTTP/REST services and agent-facing endpoints. Use when creating routes, endpoints, status codes, pagination, error responses, versioning, OpenAPI specs, idempotency, or API behavior for AI clients. Produces a clear API contract and review checklist.
---

# Design API Contracts

APIs are contracts. Resources are nouns, methods are verbs, and errors must be machine-readable.

## 1. Define resources and operations

Name resources as plural nouns:

- `/users`
- `/team-members`
- `/orders/{id}/items`

Use HTTP methods for actions:

- `GET` read
- `POST` create or trigger a deliberate action
- `PUT` replace
- `PATCH` partial update
- `DELETE` remove

Use action endpoints sparingly, like `POST /orders/{id}/cancel`.

## 2. Specify status codes

Use semantic status codes:

- `200` success
- `201` created
- `204` no content
- `400` malformed request
- `401` unauthenticated
- `403` forbidden
- `404` not found
- `409` conflict
- `422` validation failure
- `429` rate limited
- `500/502/503` server or dependency failure

Never return `200` for errors.

## 3. Validate request and response shape

Define:

- Request params
- Request body schema
- Success response
- Error response
- Pagination shape for list endpoints

Prefer consistent envelopes:

```json
{ "data": {}, "meta": {}, "links": {} }
```

Errors should include stable machine-readable codes:

```json
{ "error": { "code": "invalid_email", "message": "Invalid email", "details": [] } }
```

## 4. Add pagination and idempotency

Every list endpoint needs pagination.

Use cursor pagination for feeds or large datasets. Use page/per-page for admin views where jumping matters.

State-changing endpoints that may be retried need idempotency keys, especially payments, orders, imports, and agent-called APIs.

## 5. Version deliberately

Document what is breaking:

- Removing/renaming fields
- Changing types
- Changing URL structure
- Changing required fields

Add a new version for breaking changes. Additive optional fields usually do not require one.

## 6. Make it agent-friendly when needed

For AI/automation clients:

- Publish an OpenAPI or schema-first contract.
- Document retry behavior.
- Use distinct error codes per failure mode.
- Return opaque cursors, not math the agent must derive.
- Make state-changing operations idempotent.

## 7. Review checklist

Before implementation or merge:

- No verbs in normal resource URLs
- No unbounded list endpoints
- No bare string errors
- No `200` error responses
- Validation happens before processing
- Auth and authorization requirements are named
- Breaking changes are versioned
- Agent-facing endpoints document retry safety
