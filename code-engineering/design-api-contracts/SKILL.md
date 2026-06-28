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

Pick the semantically correct code for every outcome: `2xx` success, `4xx` caller error,
`5xx` server/dependency failure. Never return `200` for errors. Full code table:
[`reference/http-conventions.md`](./reference/http-conventions.md).

## 3. Validate request and response shape

Define request params, request body schema, success response, error response, and the
pagination shape for list endpoints. Use a consistent success envelope and stable,
machine-readable error codes, never a bare string error. The envelope and error templates
live in [`reference/http-conventions.md`](./reference/http-conventions.md).

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

Before implementation or merge, walk the contract against the review checklist in
[`reference/http-conventions.md`](./reference/http-conventions.md): no verbs in resource
URLs, no unbounded list endpoints, no bare-string or `200` errors, validation before
processing, auth named, breaking changes versioned, agent endpoints document retry safety.
