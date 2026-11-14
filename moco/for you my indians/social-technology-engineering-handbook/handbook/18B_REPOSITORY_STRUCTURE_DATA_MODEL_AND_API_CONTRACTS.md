# 18B — Repository Structure, Data Model, API Contracts and Code Ownership

**Edition:** 13 November 2026  
**Prepared with:** ChatGPT (GPT-6)  
**Purpose:** Provide a concrete, maintainable example repository, relational data model, API conventions, validation rules and ownership map. Examples are intentionally small enough to understand and should be reviewed before real deployment.

## 1. Repository structure

Use a structure that separates the user interface, backend modules, background workers, shared contracts, infrastructure and tests. Avoid putting the entire product into one giant file or mixing production secrets with source code.

```text
commonground/
├── apps/
│   ├── web/                       # Next.js web app
│   │   └── src/
│   │       ├── app/               # Routes and layouts
│   │       ├── features/          # Feed, profile, upload, settings
│   │       ├── components/        # Reusable UI components
│   │       ├── lib/               # Client helpers and typed API client
│   │       └── styles/
│   ├── api/                       # NestJS modular monolith
│   │   └── src/
│   │       ├── modules/
│   │       │   ├── identity/
│   │       │   ├── users/
│   │       │   ├── profiles/
│   │       │   ├── social-graph/
│   │       │   ├── posts/
│   │       │   ├── media/
│   │       │   ├── feed/
│   │       │   ├── comments/
│   │       │   ├── notifications/
│   │       │   ├── reports/
│   │       │   └── admin/
│   │       ├── common/             # Error types, guards, request IDs
│   │       ├── config/             # Validated config loader
│   │       └── main.ts
│   └── worker/                     # Background job consumers
├── packages/
│   ├── contracts/                 # Shared schemas/types
│   ├── validation/                # Reusable input validation
│   ├── ui/                        # Shared design system (if needed)
│   └── config/                    # Lint/format/TS configuration
├── database/
│   ├── migrations/                # Versioned schema changes
│   ├── seeds/                     # Non-production demo data
│   └── diagrams/
├── infra/
│   ├── local/                     # Compose and local dependencies
│   ├── deployment/                # IaC and environment deployment
│   ├── monitoring/
│   └── policies/                  # IAM/security policy templates
├── docs/
│   ├── architecture/              # ADRs and diagrams
│   ├── api/                       # API reference
│   ├── security/                  # Threat model and controls
│   ├── privacy/                   # Data map and retention schedule
│   ├── operations/                # Runbooks and incident plan
│   └── product/                   # PRD and user journeys
├── tests/
│   ├── contract/
│   ├── load/
│   ├── security/
│   └── e2e/
├── .github/workflows/             # CI pipelines
├── .env.example                   # Names/placeholders only, never real secrets
├── .gitignore
├── package.json
├── README.md
└── SECURITY.md
```

## 2. Feature module structure

```text
modules/posts/
├── posts.controller.ts       # HTTP boundary
├── posts.service.ts          # Business rules
├── posts.repository.ts       # Persistence operations
├── posts.schemas.ts          # Request/response validation
├── posts.policy.ts           # Authorization and visibility rules
├── posts.events.ts           # Domain event definitions
├── posts.module.ts           # Dependency wiring
└── posts.service.spec.ts     # Tests
```

Keep controllers thin. Services implement business operations. Repositories isolate persistence. Policy code makes access decisions explicit. Tests cover both allowed and denied cases.

## 3. Core data model

A starting relational model might contain:

| Table | Key fields | Important constraints |
|---|---|---|
| users | id, email_normalized, username_normalized, status, created_at | unique normalized email/username; status enum/check |
| profiles | user_id, display_name, bio, avatar_media_id | user_id primary/foreign key |
| sessions | id, user_id, token_hash, created_at, expires_at, revoked_at | store hashed opaque tokens; expiry and revocation indexes |
| follows | follower_id, followed_id, created_at | composite unique; no self-follow |
| blocks | blocker_id, blocked_id, created_at | composite unique; no self-block |
| posts | id, author_id, body, visibility, status, created_at, deleted_at | visibility/status constraints; author/time index |
| media_assets | id, owner_id, storage_key, media_type, size_bytes, checksum, processing_status | private storage key; size/type/status constraints |
| post_media | post_id, media_id, position | uniqueness for post/media and ordering rules |
| comments | id, post_id, author_id, parent_id, body, status, created_at | parent belongs to valid post; indexes by post/time |
| likes | user_id, post_id, created_at | composite primary/unique key |
| reports | id, reporter_id, target_type, target_id, reason, status, created_at | restricted access; state transitions audited |
| notifications | id, recipient_id, actor_id, type, object_ref, read_at, created_at | recipient/time index; avoid leaking restricted object content |
| audit_events | id, actor_id, action, object_type, object_id, occurred_at, request_id | append-only application permissions; sensitive payload minimized |
| outbox_events | id, event_type, aggregate_id, payload_version, payload, occurred_at, published_at | durable publish state and retry index |

Store UTC timestamps and render in the viewer's chosen locale/time zone. Define deletion semantics for each relationship. Decide whether deletion means hard delete, soft delete, anonymisation, tombstone, retention under legal hold or a mix; do not let developers guess.

### Illustrative PostgreSQL DDL

This is a learning excerpt, not a complete migration. Add extension choices, ownership, grants, partitioning, backup and migration strategy only after design review.

```sql
CREATE TABLE users (
  id UUID PRIMARY KEY,
  email_normalized TEXT NOT NULL UNIQUE,
  username_normalized TEXT NOT NULL UNIQUE,
  status TEXT NOT NULL CHECK (status IN ('active','suspended','pending_deletion')),
  created_at TIMESTAMPTZ NOT NULL DEFAULT now()
);

CREATE TABLE follows (
  follower_id UUID NOT NULL REFERENCES users(id),
  followed_id UUID NOT NULL REFERENCES users(id),
  created_at TIMESTAMPTZ NOT NULL DEFAULT now(),
  PRIMARY KEY (follower_id, followed_id),
  CHECK (follower_id <> followed_id)
);
CREATE INDEX follows_by_followed ON follows (followed_id, created_at DESC);

CREATE TABLE posts (
  id UUID PRIMARY KEY,
  author_id UUID NOT NULL REFERENCES users(id),
  body TEXT,
  visibility TEXT NOT NULL CHECK (visibility IN ('public','followers','private')),
  status TEXT NOT NULL CHECK (status IN ('draft','processing','published','removed')),
  created_at TIMESTAMPTZ NOT NULL DEFAULT now(),
  deleted_at TIMESTAMPTZ
);
CREATE INDEX posts_author_time ON posts (author_id, created_at DESC)
  WHERE deleted_at IS NULL;
```

Key lessons:

- Constraints protect data integrity even if application code contains a bug.
- Indexes speed reads but increase write/storage cost. Use `EXPLAIN (ANALYZE, BUFFERS)` on representative safe test data before adding indexes.
- A `CHECK` constraint is not a substitute for full authorization.
- Never expose sequential internal IDs as a security boundary.
- Use parameterized queries or a safe ORM query API; never concatenate untrusted input into SQL.

## 4. API design conventions

Choose one consistent style (REST, GraphQL or RPC) based on client and domain needs. The example uses REST over HTTPS with JSON.

| Method | Path | Purpose | Authorization note |
|---|---|---|---|
| POST | `/v1/auth/register` | Start account registration | Abuse controls and verification |
| POST | `/v1/auth/login` | Create session | Rate limit; generic failure messages |
| POST | `/v1/auth/logout` | Revoke current session | Must identify current session |
| GET | `/v1/me` | Current account/profile | Own account only |
| PATCH | `/v1/me/profile` | Update profile | Field-level validation |
| POST | `/v1/posts` | Create post | Active account, quota, visibility validation |
| GET | `/v1/feed?cursor=...` | Fetch feed page | Filter every item under current access rules |
| GET | `/v1/posts/{id}` | Fetch one post | Object-level authorization every time |
| POST | `/v1/posts/{id}/likes` | Like post | Idempotent behaviour |
| DELETE | `/v1/posts/{id}/likes` | Unlike post | Own like only |
| POST | `/v1/posts/{id}/reports` | Report post | Reporter identity protected |
| POST | `/v1/media/upload-intents` | Request a signed upload | Validate size/type/quota first |
| POST | `/v1/account/deletion-requests` | Start deletion workflow | Re-authentication and confirmation |

### Example request and response

Request:

```http
POST /v1/posts HTTP/1.1
Content-Type: application/json
Authorization: Bearer <short-lived-access-token>
Idempotency-Key: 0fc3f4e7-...
```

```json
{
  "body": "A short public update.",
  "visibility": "public",
  "mediaIds": []
}
```

Response:

```json
{
  "data": {
    "id": "a-generated-uuid",
    "status": "published",
    "createdAt": "2026-11-13T12:00:00Z"
  },
  "requestId": "req-generated-id"
}
```

This example omits implementation-specific token format and real secrets. A production API should not return internal database errors, stack traces, storage credentials or private moderation notes.

## 5. API rules that prevent avoidable incidents

- Validate type, size, format, range and allowed fields at the server boundary.
- Reject unknown sensitive fields rather than trusting client-provided `role`, `ownerId`, `isAdmin` or `visibilityOverride` values.
- Implement object-level and function-level authorization on every request.
- Use cursor pagination for feeds and large collections; define stable ordering and cursor integrity.
- Apply timeouts, per-user/per-IP quotas and request-body limits.
- Use idempotency keys for retryable operations that could create duplicate payments, posts, jobs or actions.
- Define retryable vs non-retryable errors. Do not retry a non-idempotent write blindly.
- Use versioned schemas/contracts and a deprecation policy for mobile clients and integrations.
- Sign and verify webhooks; protect against replay and duplicate delivery.
- Return consistent error envelopes with a safe code, human-readable message and request ID.
- Do not put secrets or personal data in URLs, analytics parameters or logs.

## 6. Environment and secret handling

`.env.example` may contain names and safe placeholders only:

```dotenv
NODE_ENV=development
DATABASE_URL=postgresql://local-user:local-password@localhost:5432/commonground_dev
REDIS_URL=redis://localhost:6379
OBJECT_STORAGE_BUCKET=local-media
SESSION_SIGNING_KEY=REPLACE_WITH_LOCAL_RANDOM_SECRET
PUBLIC_APP_ORIGIN=http://localhost:3000
```

Never commit real credentials. Production secrets belong in a secrets manager or platform-provided secret store. Use separate credentials per environment and service, short-lived workload identity where available, least privilege, rotation and access logs. Local demo credentials must never be reused in production.

## 7. Data lifecycle rules to decide

For each data category document: purpose, collection point, lawful basis/consent where applicable, systems receiving it, access roles, storage region, retention rule, deletion method, backup expiry and user-facing rights workflow. Include telemetry, support tickets, moderation evidence, payment records, device/session data and vendor logs—not only the primary user table.

## 8. Code review checklist

- Does the change alter the threat model, data map, permissions or retention?
- Does it have validation for malformed and oversized inputs?
- Are both authorised and unauthorised paths tested?
- Does it create background events safely and idempotently?
- Are migration and rollback/forward-fix paths documented?
- Are logs useful without leaking data?
- Does the UI communicate loading, failure and retry state?
- Is the code accessible, maintainable and covered by tests?
- Is documentation updated?

## References

- PostgreSQL constraints and indexes: https://www.postgresql.org/docs/current/ddl-constraints.html and https://www.postgresql.org/docs/current/indexes.html
- OpenAPI Specification: https://spec.openapis.org/oas/latest.html
- OWASP API Security: https://owasp.org/www-project-api-security/
- Git documentation: https://git-scm.com/doc
