# 07C — Software Architecture, Modularity, Events and Service Boundaries

## 1. Architecture is about decisions and constraints

Software architecture describes the important structures of a system and the decisions that are expensive to change: deployment boundaries, data ownership, security boundaries, communication patterns, reliability and operational responsibilities. A folder structure is useful, but it is not the architecture by itself.

Start by writing quality attributes: expected traffic, latency, availability, privacy, data durability, geographic reach, cost ceiling, development team size and regulatory constraints. Architecture decisions are trade-offs among these attributes.

## 2. Monolith, modular monolith and microservices

- **Monolith:** one deployable application. It may be well-structured or a tangled codebase.
- **Modular monolith:** one deployable application with explicit internal modules and boundaries.
- **Microservices:** independently deployable services with network communication and more independent ownership.

A modular monolith is often a strong starting point for a new product. It reduces distributed-systems overhead while allowing clean modules. Microservices add network failure, service discovery, observability, deployments, contract compatibility, data consistency and operational cost. Split only when a measured need or team boundary justifies it.

## 3. Domain modelling and bounded contexts

Group code around business capabilities: identity, profiles, content, media, social graph, billing, search, moderation and analytics. Each capability should own its rules. A `User` in identity may have different concerns from a public `CreatorProfile`; do not make one universal model that every module edits freely.

Use a shared language: agree what “account”, “profile”, “post”, “media asset”, “view”, “impression”, “report” and “delete” mean. Ambiguous domain terms become API and data bugs.

## 4. Layering and dependency direction

A useful pattern separates:

- presentation/transport (HTTP, jobs, CLI);
- application use cases;
- domain rules;
- infrastructure adapters (database, email, storage, payment provider).

Domain rules should not depend on a specific cloud provider or web framework where reasonable. This makes testing and provider changes easier. Do not over-engineer abstractions for hypothetical future vendors; isolate only dependencies with meaningful change risk.

## 5. Event-driven architecture

An event is a fact that has happened: `PostPublished`, `UserFollowed`, `VideoTranscodingCompleted`. A command requests an action; an event records an outcome. Events can decouple modules and trigger asynchronous work.

Example after a post is published:

- persist the post;
- publish a post-created event (reliably);
- feed workers update candidate timelines;
- search worker indexes content;
- notification service decides whether to notify followers;
- analytics pipeline records a publish event.

Events require schemas, IDs, timestamps, versioning, privacy review, delivery guarantees and retention rules.

## 6. The dual-write problem and transactional outbox

Suppose a service writes to a database and then sends a queue message. If the database commit succeeds but publishing the message fails, downstream systems never hear about the post. If publishing succeeds but database commit fails, workers process an event for data that does not exist.

A common solution is the **transactional outbox**: write the business record and an outbox event in the same database transaction. A worker publishes the outbox record and marks it delivered. Consumers must still be idempotent because duplicate delivery can occur.

## 7. Sagas and distributed business workflows

A saga is a sequence of local transactions across services, with compensating actions for failure where possible. Example: start subscription, authorise payment, activate plan, send receipt. If activation fails after payment, the system may refund or retry according to a defined policy. A saga is not a distributed ACID transaction; compensation is business logic and must be designed carefully.

## 8. Architecture decision records (ADRs)

For an important choice, record:

- context/problem;
- options considered;
- decision;
- reasons and trade-offs;
- security/privacy impact;
- migration or rollback plan;
- date and owner.

Example: “Use PostgreSQL as the primary source of truth and Redis only as rebuildable cache.” Record why, what failure modes exist and how cache invalidation works.

## 9. Architecture diagrams

Maintain at least:

1. system context diagram (users and external systems);
2. container/deployment diagram (apps, services, databases, queues);
3. important sequence diagrams (signup, upload, messaging, delete account);
4. data-flow diagram with sensitive data boundaries;
5. trust-boundary/threat-model diagram.

Keep them current. A diagram that lies is worse than no diagram.

## 10. Example decision for an early product

A reasonable early design may use one API deployment, one worker deployment, PostgreSQL, Redis, object storage and a CDN. Modules live in one codebase. Video processing is asynchronous. Search can initially use database search or a managed index. Split messaging, feed generation or media processing into separate services only when traffic, reliability or team ownership warrants it.

## 11. Practical lab

Write three ADRs: (a) modular monolith vs microservices; (b) PostgreSQL vs document database as primary store; (c) direct browser-to-object-storage uploads vs server-proxied uploads. For each, document security, cost, operational complexity and migration path.

## Further reading

- Martin Fowler, Microservices: https://martinfowler.com/articles/microservices.html
- Microsoft Cloud Design Patterns: https://learn.microsoft.com/en-us/azure/architecture/patterns/
- AWS Prescriptive Guidance: https://docs.aws.amazon.com/prescriptive-guidance/latest/modernization-architecting-microservices/welcome.html
- Google Cloud Architecture Framework: https://cloud.google.com/architecture/framework
