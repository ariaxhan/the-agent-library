---
name: secure-code-changes
description: Review or implement code changes with security constraints. Use when touching auth, secrets, credentials, permissions, payments, PII, input validation, SQL queries, file uploads, LLM/prompt features, or when the user asks for a security review. Produces a threat-aware checklist, findings, and fixes.
---

# Secure Code Changes

Security is a constraint on the feature, not a cleanup pass later.

## 1. Identify sensitive surfaces

Look for:

- User input
- Authentication and sessions
- Authorization and ownership
- Secrets and credentials
- Payments or billing
- PII or private data
- File uploads
- Database queries
- Webhook handlers
- LLM prompts and tool calls

State which surfaces are in scope.

## 2. Check secrets

Search for hardcoded keys, tokens, passwords, and private material. Secrets belong in environment variables, secure stores, or platform secret managers.

Do not print secrets in logs, tests, fixtures, screenshots, or commit messages.

## 3. Validate inputs

At every boundary:

- Parse with a schema or typed validator.
- Reject invalid input.
- Avoid string concatenation in queries.
- Enforce size limits.
- Treat client-side validation as user experience only, not security.

## 4. Check auth and authorization

Authentication answers "who are you?" Authorization answers "may you do this?"

Every sensitive read/write needs an ownership or role check. Admin-by-default is a bug.

## 5. Review common vulnerability paths

Check:

- SQL or command injection
- XSS / unsafe HTML
- CSRF on cookie-auth state changes
- Rate limits on public or expensive endpoints
- Unsafe redirects
- File upload type/size/path handling
- Stack traces or internals in user responses
- Dependency vulnerabilities
- Prompt injection if LLM output controls tools, data, or code paths

## 6. Fail secure

On uncertain state, deny access or stop the operation. Errors should not grant permissions, skip checks, or continue with partial security context.

## 7. Produce findings or fixes

For each issue:

- Severity
- Attack path
- Affected file/endpoint
- Evidence
- Fix
- Test or check

For high-risk areas, require human review even if automated checks pass.
