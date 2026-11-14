# 08A — Data Modelling, SQL, Relationships and Transactions

## 1. Data modelling begins with reality

Before choosing a database, identify the real-world concepts, rules and relationships. A data model should represent what the product promises, not just mirror the current UI.

For a collaboration platform, entities may include Account, Profile, Organisation, Membership, Project, Post, Comment, MediaAsset, Message, Report and Subscription. Define identity, ownership, lifecycle, privacy and retention for each.

## 2. Relational databases

A relational database stores data in tables with rows and columns and relates records through keys. PostgreSQL is a widely used open-source relational database with transactions, constraints, indexing, JSON capabilities and extensions.

Example simplified schema:

```sql
CREATE TABLE users (
  id UUID PRIMARY KEY,
  email TEXT NOT NULL UNIQUE,
  username TEXT NOT NULL UNIQUE,
  created_at TIMESTAMPTZ NOT NULL DEFAULT now()
);

CREATE TABLE posts (
  id UUID PRIMARY KEY,
  author_id UUID NOT NULL REFERENCES users(id),
  body TEXT,
  visibility TEXT NOT NULL CHECK (visibility IN ('public','followers','private')),
  created_at TIMESTAMPTZ NOT NULL DEFAULT now()
);

CREATE INDEX posts_author_created_idx
  ON posts (author_id, created_at DESC, id DESC);
```

This is an educational example, not a production-ready schema. Real systems need migrations, constraints, deletion policy, indexes measured against queries and more careful privacy modelling.

## 3. Keys and relationships

- **Primary key:** unique identifier for each row.
- **Foreign key:** enforces a relationship to another row.
- **Unique constraint:** prevents duplicate values or combinations.
- **Check constraint:** enforces a row-level rule.
- **Join table:** models many-to-many relationships.

A follow relationship is often represented as `(follower_id, followed_id, created_at)` with a composite uniqueness constraint. For private accounts, a separate follow-request state may be needed. Blocks, mutes and restrictions should be modelled as explicit relationships because they affect many access decisions.

## 4. Normalisation and denormalisation

Normalisation reduces unnecessary duplication and update anomalies. Denormalisation duplicates calculated or frequently accessed values to improve read performance. Neither is automatically good or bad.

Example: storing `like_count` on a post can make reading counts fast, but then writes must update it safely and reconciliation may be needed. The source of truth may be the individual like records; the count is a derived value. Define how to rebuild derived data if it becomes inconsistent.

## 5. Transactions and ACID

A database transaction groups operations into a unit with ACID properties:

- **Atomicity:** all operations succeed or none do.
- **Consistency:** constraints remain satisfied.
- **Isolation:** concurrent transactions do not produce unacceptable interference.
- **Durability:** committed changes survive failures according to the database's durability configuration.

Example: create an order and reserve inventory. If one operation fails, rollback the transaction so the system does not record an order without the intended reservation. Cross-service workflows are more complicated and may need saga patterns rather than one database transaction.

## 6. Isolation and concurrency

Concurrent requests can race. Two users may try to claim the same username, reserve the last ticket or like a post at the same time. Application-level “check then insert” logic is insufficient without database constraints/locking/transaction design. Use unique constraints and handle conflicts intentionally.

Learn read committed, repeatable read, serializable and database-specific behaviour. Higher isolation can reduce anomalies but may increase contention or cause retries. Understand the database you operate rather than assuming all engines behave identically.

## 7. Query planning and indexes

An index is an additional data structure that helps the database find rows faster. It costs storage and adds work to writes. Use `EXPLAIN`/`EXPLAIN ANALYZE` on representative queries. Index the columns used by real filters, joins and orderings; do not blindly index every column.

A feed query might need an index supporting the author/date ordering. A search query may need full-text or dedicated search. A composite index's column order matters.

## 8. Schema migrations

Use versioned migrations committed with application code. Production changes should be backward-compatible where possible:

1. Add a new nullable/compatible column or table.
2. Deploy code that can read old and new forms.
3. Backfill existing rows in controlled batches.
4. Switch new writes/reads.
5. Verify and monitor.
6. Remove the old field only after no deployed code requires it.

Large table rewrites and index creation can lock or overload production systems depending on engine and method. Read database-specific online migration guidance.

## 9. Data deletion and lifecycle

Deleting an account is not simply deleting one `users` row. Related content, messages, backups, legal holds, abuse evidence, payment records, caches, search indexes and third-party processors may have different retention rules. Design a deletion workflow that states what is deleted, anonymised, retained for a lawful reason, queued, and eventually expired. A deletion request should be auditable without retaining unnecessary personal data.

## 10. Practical lab

Create users, posts, follows, likes and comments. Add foreign keys, uniqueness and check constraints. Simulate two concurrent requests attempting the same unique action. Use `EXPLAIN ANALYZE`, then add or adjust an index and compare performance with realistic test data.

## Further reading

- PostgreSQL Documentation: https://www.postgresql.org/docs/current/
- PostgreSQL constraints: https://www.postgresql.org/docs/current/ddl-constraints.html
- PostgreSQL transactions: https://www.postgresql.org/docs/current/tutorial-transactions.html
- Use The Index, Luke: https://use-the-index-luke.com/
