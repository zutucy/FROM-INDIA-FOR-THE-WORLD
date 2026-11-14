# 07A — Backend Fundamentals, Servers and Runtime

## 1. What is a backend?

A backend is the server-side part of a system. It applies business rules, authenticates and authorises requests, accesses data, coordinates external services and returns results. It may run as one process or as many services. The user interface is only a client; important rules must be enforced on the server because clients are under the user's control.

## 2. Server, process and service

- A **server** is a program or machine that provides a service; the word can mean software or hardware depending on context.
- A **process** is a running program with its own address space and resources.
- A **thread** is an execution path within a process.
- A **service** is a logical capability exposed to other components/users.
- A **runtime** provides the execution environment for a language.

Node.js, Python, Java, Go, .NET and Ruby are common backend ecosystems. They differ in runtime model, libraries, deployment patterns, concurrency tools and team familiarity. There is no universally fastest language for every application.

## 3. Request lifecycle

A typical request passes through:

1. Network edge, CDN or load balancer.
2. TLS termination (depending on architecture).
3. Routing to an application instance.
4. Request parsing and size limits.
5. Authentication.
6. Authorization.
7. Validation and business logic.
8. Database/cache or downstream calls.
9. Response mapping and safe error handling.
10. Metrics, traces and logs.

A request may also publish an event or enqueue work to happen later. Keep the synchronous path short enough to meet user expectations.

## 4. API, controller, service and repository

A common layered arrangement:

- **Route/controller:** maps HTTP endpoint to application operation.
- **Middleware/guards:** cross-cutting checks such as authentication and rate limiting.
- **Service/use case:** applies business rules.
- **Repository/data access:** reads/writes persistence.
- **DTO/schema:** defines expected request and response data.
- **Adapter/client:** communicates with an external provider.

These are boundaries, not mandatory classes. A small project can use fewer layers; the point is to avoid mixing HTTP parsing, permission checks, business logic and SQL into one untestable function.

## 5. Authentication vs authorisation

- **Authentication:** who is making the request?
- **Authorisation:** what is that identity allowed to do on this resource, in this context?

A logged-in user is not automatically allowed to access every record. Check object ownership, relationship state, privacy, organisation membership, moderation status and action-specific permission at the server boundary.

## 6. Sessions and tokens

Session cookies let the server maintain a server-side session referenced by a hard-to-guess identifier. Cookies can use `Secure`, `HttpOnly` and suitable `SameSite` attributes. Tokens (including JWTs) can carry claims but require careful expiration, audience/issuer validation, signing-key rotation and revocation strategy. JWT is not inherently more secure than a session cookie.

For browsers, secure server-managed sessions are often simpler than inventing a long-lived token scheme. For mobile or third-party API clients, an appropriate OAuth 2.0 / OpenID Connect flow may be required. Do not design your own cryptographic protocol.

## 7. Synchronous vs asynchronous work

Synchronous work returns a result before the request completes. Suitable: checking credentials, creating a post record, returning a page.

Asynchronous/background work: video transcoding, sending email, generating thumbnails, notifications, search indexing, analytics aggregation and cleanup.

Use a durable queue when a job must survive process restarts and retries. Design workers to tolerate duplicate delivery (idempotency), transient failure, poison messages, retry storms and queue backlogs.

## 8. Error handling

Return consistent, useful, non-sensitive errors. Do not leak stack traces, SQL, internal hostnames, secrets or account existence unnecessarily. Distinguish validation errors, authentication errors, permission errors, missing resources, conflicts, rate limits and server failures.

Log the detailed diagnostic context securely on the server and return a safe correlation/request ID to the client. Never log passwords, full authentication tokens or private message contents without a justified, controlled policy.

## 9. Backend frameworks: how to choose

- **Express/Fastify:** lightweight Node.js HTTP frameworks; more architectural decisions remain with your team.
- **NestJS:** structured TypeScript framework with modules, dependency injection and conventions.
- **Django/FastAPI:** Python ecosystems with different strengths; Django includes many batteries, FastAPI focuses on API development and type hints.
- **Spring Boot:** mature Java ecosystem for enterprise services.
- **ASP.NET Core:** mature cross-platform .NET web framework.
- **Go standard library/frameworks:** common for compact services and infrastructure-oriented work.

Choose based on project needs, team skill, library maturity, observability, security maintenance and operational support—not popularity alone.

## 10. Example project layout

```text
api/
  src/
    modules/
      accounts/
      profiles/
      posts/
      media/
      search/
    common/
      errors/
      auth/
      validation/
      logging/
    infrastructure/
      database/
      queue/
      storage/
    config/
    main.ts
  test/
  migrations/
  Dockerfile
```

Keep secrets out of source control. Validate environment variables at startup and fail fast when a required secret/configuration is missing.

## 11. Practical lab

Build an API with endpoints to create and read a profile. Add:

- schema validation;
- authentication/session handling;
- owner-only update permission;
- structured error responses;
- request IDs and basic logs;
- tests for unauthenticated and unauthorised requests;
- rate limiting for sensitive endpoints.

Then simulate a client tampering with the profile ID. Confirm the server rejects the access.

## Further reading

- Node.js documentation: https://nodejs.org/en/learn
- NestJS documentation: https://docs.nestjs.com/
- Express documentation: https://expressjs.com/
- Fastify documentation: https://fastify.dev/docs/latest/
- OAuth 2.0 Security Best Current Practice: https://www.rfc-editor.org/rfc/rfc9700
