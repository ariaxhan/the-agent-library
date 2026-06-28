# HTTP conventions — lookup tables for `design-api-contracts`

The exhaustive enumerations the skill points to. The SKILL body carries the decisions; this
file carries the full lookups so they stay copy-pasteable without bloating the workflow.

## Status codes

Use semantic status codes. Never return `200` for errors.

| Code | Meaning |
|---|---|
| `200` | success |
| `201` | created |
| `204` | no content |
| `400` | malformed request |
| `401` | unauthenticated |
| `403` | forbidden |
| `404` | not found |
| `409` | conflict |
| `422` | validation failure |
| `429` | rate limited |
| `500` / `502` / `503` | server or dependency failure |

## Response envelopes

Prefer a consistent success envelope:

```json
{ "data": {}, "meta": {}, "links": {} }
```

Errors should include stable, machine-readable codes — never a bare string:

```json
{ "error": { "code": "invalid_email", "message": "Invalid email", "details": [] } }
```

## Review checklist

Before implementation or merge:

- [ ] No verbs in normal resource URLs
- [ ] No unbounded list endpoints
- [ ] No bare string errors
- [ ] No `200` error responses
- [ ] Validation happens before processing
- [ ] Auth and authorization requirements are named
- [ ] Breaking changes are versioned
- [ ] Agent-facing endpoints document retry safety
