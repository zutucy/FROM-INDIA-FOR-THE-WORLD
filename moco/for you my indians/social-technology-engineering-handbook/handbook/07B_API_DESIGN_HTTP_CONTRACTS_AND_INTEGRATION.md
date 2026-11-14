# 07B — API Design, HTTP Contracts and Integration

## 1. What is an API?

An Application Programming Interface defines how one software component can request functionality or data from another. A web API may use HTTP, but APIs also exist inside a process, an operating system, a database driver, a mobile SDK or a hardware interface.

Good APIs are predictable, secure, documented, version-aware and stable enough for clients to depend on.

## 2. HTTP basics for API designers

A request usually includes method, URL, headers and optional body. A response includes status, headers and optional body.

Common methods:

- `GET`: retrieve a representation; should not change server state.
- `POST`: submit data or trigger an operation; commonly creates a resource.
- `PUT`: replace a resource representation or perform idempotent update semantics.
- `PATCH`: partially modify a resource.
- `DELETE`: request deletion.

Common status groups: `2xx` success, `3xx` redirect, `4xx` client/request issue, `5xx` server issue. Use specific codes consistently: `201` created, `202` accepted for asynchronous processing, `400` malformed request, `401` unauthenticated, `403` forbidden, `404` not found, `409` conflict, `422` semantically invalid input where used by the API, `429` rate limited, `500` unexpected server failure.

## 3. Resource-oriented design

Example:

```text
GET    /v1/posts/{postId}
POST   /v1/posts
PATCH  /v1/posts/{postId}
DELETE /v1/posts/{postId}
POST   /v1/posts/{postId}/likes
DELETE /v1/posts/{postId}/likes
GET    /v1/users/{userId}/posts?limit=20&cursor=...
```

A route name is not a permission check. Every endpoint must verify the caller may perform the requested action on the specific resource.

## 4. Pagination

Do not return millions of records at once. Options:

- **Offset pagination:** `?limit=20&offset=40`; easy to understand, but can become slow and unstable when rows are inserted/deleted between pages.
- **Cursor/keyset pagination:** next page uses a stable ordered key such as `(created_at, id)`; often better for large/changing feeds.

Return a documented next cursor. Treat cursors as untrusted input and validate them. A cursor should not expose secrets or grant access.

## 5. Idempotency and retries

Networks fail. A client may send a request, the server may complete it, and the response may be lost. Retrying a payment, post creation or upload completion can create duplicates unless the operation is designed for it.

For operations that need safe retry, use an idempotency key scoped to the authenticated principal and operation. Store the key, request fingerprint and resulting outcome for a defined retention period. Reject reuse with a different payload. Idempotency is not a substitute for database uniqueness constraints or transaction design.

## 6. API contracts and schemas

Use OpenAPI for HTTP API documentation where appropriate. Define:

- operation name and route;
- authentication method;
- request schema and validation;
- response schema;
- error formats;
- pagination behaviour;
- rate-limit expectations;
- deprecation/version policy;
- permission requirements.

Generate clients where useful, but review generated types and runtime validation boundaries. A TypeScript interface does not validate a request sent over the network.

## 7. Versioning and backward compatibility

A mobile app may remain installed long after a backend deployment. A web frontend may be cached in a CDN. Third-party partners may deploy only occasionally. Therefore, avoid breaking old clients casually.

Options include URL versioning (`/v1/`), header/media-type versioning or additive evolution. The best choice depends on product and governance. A safe change typically adds optional fields first, allows old and new clients to coexist, measures usage and removes an old contract only after a documented deprecation period.

## 8. Rate limiting and quotas

Limit requests by identity, IP, endpoint, resource cost and abuse risk as appropriate. A login endpoint, public search endpoint, video upload and messaging endpoint need different policies. Apply limits consistently across multiple application instances using a shared counter/coordination mechanism where required.

Return `429` with documented retry information when appropriate. Avoid using IP address as the only identity signal; NAT, mobile carriers and shared networks can group many legitimate users together.

## 9. Webhooks and external integrations

A webhook sends an event to another system. Build for:

- signature verification;
- replay protection and timestamp checks;
- delivery retries;
- duplicate events;
- ordering uncertainty;
- timeout and backoff;
- endpoint ownership/SSRF safeguards;
- event schema versioning;
- secret rotation.

Never assume an incoming webhook is authentic merely because it came from an IP address that looks familiar. Verify cryptographic signatures according to provider documentation.

## 10. gRPC, GraphQL and REST

- **REST-style HTTP APIs:** straightforward resource-oriented interfaces, easy browser/tool integration.
- **GraphQL:** clients request a graph-shaped selection of fields; needs query cost limits, resolver efficiency, authorization and caching strategy.
- **gRPC:** strongly defined service contracts, often uses Protocol Buffers and HTTP/2; useful for service-to-service communication and streaming patterns.

These approaches can coexist. Do not choose GraphQL or microservices just because a large company uses them.

## 11. API abuse and security

Protect against broken object-level authorization, broken authentication, excessive data exposure, unrestricted resource consumption, server-side request forgery and unsafe third-party API consumption. Validate input, enforce per-object permissions, limit expensive queries and maintain an inventory of public/internal APIs.

## 12. Practical lab

Design a posts API with create/read/update/delete, cursor pagination, request validation, stable error schema, idempotent create and an OpenAPI document. Write tests proving one user cannot read/update another user's private content by changing an ID.

## Further reading

- HTTP Semantics, RFC 9110: https://www.rfc-editor.org/rfc/rfc9110
- OpenAPI Specification: https://spec.openapis.org/oas/latest.html
- OWASP API Security: https://owasp.org/www-project-api-security/
- OAuth 2.0 Security BCP: https://www.rfc-editor.org/rfc/rfc9700
- gRPC documentation: https://grpc.io/docs/
- GraphQL documentation: https://graphql.org/learn/
