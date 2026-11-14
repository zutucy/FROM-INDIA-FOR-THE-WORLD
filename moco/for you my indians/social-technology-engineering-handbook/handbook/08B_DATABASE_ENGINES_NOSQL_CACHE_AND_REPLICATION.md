# 08B — Database Engines, NoSQL, Cache and Replication

## 1. A database is not just a file

A database engine manages pages, indexes, query execution, transactions, locks, logs, memory, background maintenance, replication and recovery. Choosing a database means choosing operational behaviour as well as a query language.

## 2. Relational vs non-relational systems

### Relational (SQL)

Best when relationships, constraints and transactions are central. Examples include PostgreSQL, MySQL and SQL Server. SQL is a declarative language: describe the result, and the query planner chooses an execution strategy.

### Document databases

Store records as documents, often JSON-like. They can suit flexible document-shaped records, but flexible schema does not remove the need for modelling, indexes, validation or consistency decisions. MongoDB is a common example.

### Key-value stores

Map keys to values and often support very fast lookups. Redis is widely used for caching, ephemeral state, rate counters, queues (with caveats) and coordination primitives. Do not treat cache data as the sole durable source unless the design and persistence configuration explicitly support that role.

### Wide-column and distributed databases

Designed for particular high-scale access patterns and distribution needs. Examples include Cassandra and cloud-managed equivalents. They can require query-first data modelling and different consistency trade-offs.

### Time-series and analytical stores

Time-series engines optimise timestamped measurements; columnar analytical warehouses support scans and aggregations over large datasets. An operational database and analytics warehouse usually serve different workloads.

## 3. CAP and consistency—avoid slogans

CAP is about trade-offs during network partitions in distributed systems. It is often misused as a simplistic label saying a database “chooses only two.” Real systems expose consistency models and availability behaviour with more nuance. Learn linearizability, serializability, eventual consistency, read-your-writes and causal consistency in context.

For user-facing products, decide where immediate consistency is essential (account security, payment state, ownership changes) and where eventual consistency may be acceptable (some counters, search index freshness, recommendation features).

## 4. Cache design

A cache stores data closer to the consumer to reduce latency and source-system load. Common patterns:

- **Cache-aside:** application reads cache; on miss, loads from source and fills cache.
- **Read-through:** cache layer loads on miss.
- **Write-through:** writes pass through cache and source.
- **Write-behind:** cache acknowledges and writes later; riskier for critical data.

Important questions:

- What is the source of truth?
- How long is data valid?
- How is invalidation triggered?
- Can stale data expose private information?
- What happens on cache outage?
- Are cache keys tenant/user scoped?

Never use a cache key that omits an authorization dimension if the cached response differs by user or permission. Shared-cache leakage is a privacy incident.

## 5. Replication and read replicas

Replication maintains copies of data. It can support availability, disaster recovery and read scaling, but replicas may lag. A user who writes a profile update and immediately reads from a lagging replica may see old data. Route critical read-after-write requests appropriately or use a consistency mechanism.

Replication is not a complete backup. Accidental deletes or corrupted writes may replicate too. Keep independent backups and practice restore.

## 6. Partitioning and sharding

Partitioning divides a large table into manageable pieces, often by date or key ranges. Sharding distributes data across separate database nodes. Sharding complicates joins, transactions, uniqueness, rebalancing, backups and operations. It should be driven by measured scaling limits and access patterns, not anticipated fame.

## 7. Connection pools

Each database connection consumes resources. If every application request opens a new connection, the database may be overwhelmed. Use controlled connection pools, sensible timeouts, limits per service and load testing. Serverless deployments can create connection spikes; use supported pooling/proxy options when appropriate.

## 8. Redis practical uses and risks

Redis is useful for:

- frequently accessed cached records;
- rate-limit counters;
- short-lived verification state;
- online presence with expiry;
- ephemeral fan-out queues where data loss is acceptable;
- distributed locks only when the design carefully handles lease expiry and failure.

Do not store irreversible business truth only in an ephemeral key. Locks do not magically guarantee correctness; fencing tokens or stronger coordination may be needed for high-risk writes.

## 9. Search vs database lookup

A relational query can support exact filters and joins. A search engine such as OpenSearch or Elasticsearch is designed for full-text retrieval, relevance ranking, facets and search analytics. Search indexes are usually derived data and may lag behind the primary database. Enforce permissions before returning results, and ensure deletion/block/privacy changes propagate to indexes.

## 10. Practical lab

Create a PostgreSQL-backed app and a Redis cache. Measure repeated profile reads. Add cache-aside behaviour, expiry and invalidation on profile update. Then simulate Redis outage and confirm the application degrades safely without returning another user's cached data.

## Further reading

- PostgreSQL: https://www.postgresql.org/docs/current/
- Redis documentation: https://redis.io/docs/latest/
- MongoDB data modelling: https://www.mongodb.com/docs/manual/data-modeling/
- Apache Cassandra: https://cassandra.apache.org/doc/latest/
- OpenSearch: https://opensearch.org/docs/latest/
