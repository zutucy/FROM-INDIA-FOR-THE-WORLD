# 13B — Partitioning, replication, consensus and distributed storage

## 1. Scale-up and scale-out

**Vertical scaling** adds CPU, RAM, storage or network capacity to one machine. It is operationally simple until hardware, cost or failure limits are reached. **Horizontal scaling** adds machines and distributes requests/data. It raises potential capacity and resilience but introduces routing, replication, coordination and operations.

Measure first. A missing index, bad query, memory leak or inefficient media path may be cheaper to fix than building a cluster.

## 2. Partitioning and sharding

Partitioning divides a dataset into smaller pieces; sharding usually distributes those pieces across servers.

- **Range partitioning:** Assign key ranges; helpful for range queries but hot ranges can form.
- **Hash partitioning:** Hash a key to spread records; range queries and resharding may be harder.
- **Directory-based:** A lookup maps keys to shards; flexible but the directory becomes important infrastructure.
- **Geographic:** Place data near users/regions while considering cross-border access, latency and legal commitments.

Choose keys based on access patterns, tenancy, write distribution and growth. Poor keys create hot shards. Shard too early and joins, unique constraints, migrations, transactions and operations become harder.

## 3. Replication

Replication copies data to other machines/regions. It can improve read capacity and availability but creates lag and consistency questions. Synchronous replication may reduce loss of acknowledged writes within its defined failure model but increases latency and may reduce write availability. Asynchronous replication is more responsive but can lose recent writes if a primary fails before replication.

A replica is not a backup. Accidental deletion, corruption or malicious changes may replicate. Keep independent, protected backups and test restoration.

## 4. Consensus and leader election

Consensus helps nodes agree on ordered state despite defined failures. Raft is a widely taught understandable algorithm; Paxos is another influential family. Guarantees depend on assumptions such as a functioning quorum and eventual network communication. They do not make the system immune to every failure.

Leader-based designs use terms/epochs, log replication and commit rules so an old leader cannot silently overwrite committed state. Do not implement your own production consensus protocol as a learning exercise; use mature systems with documented guarantees.

## 5. Distributed transactions and sagas

A DB transaction can provide atomicity inside one database. Across independent services, a single ACID transaction may not exist or be desirable. A **saga** breaks a process into steps with compensating actions. Example: reserve inventory → authorize payment → create shipment. If shipment fails, void authorization and release inventory. Compensation is a business-defined recovery action, not always a literal reversal.

A transactional outbox writes the business change and event record in one DB transaction; a publisher forwards the event later. Consumers must still be idempotent. Reconciliation finds stuck/inconsistent workflows.

## 6. Partition choices in products

- Social graph: partition around user/account access patterns.
- Messages: partition by conversation or another access strategy; ordering is conversation-specific.
- Media: object storage for blobs, database for metadata.
- Analytics: partition by time/tenant while planning deletion.
- Search: distributed index shards; indexing may lag the source DB.

These are examples, not universal prescriptions. Popular creators, large tenants and unusually active conversations create hot keys.

## 7. Migration and resharding

A safe migration may include dual-read, backfill, consistency checks, gradual traffic shift and rollback. Dual-write itself can fail partially, so define the source of truth and reconciliation. Rate-limit large backfills so they do not overload production. Monitor lag, duplicates, missing rows and error rates.

## 8. Pick storage by workload

Relational DBs suit transactions/relationships; key-value stores suit specific low-latency lookup patterns; document stores suit suitable flexible documents; wide-column stores suit high-volume partitioned access; search engines suit full-text retrieval; object stores suit large blobs; warehouses/lakehouses suit analytics. None is universally fastest. Match data model and access patterns.

## 9. Exercise

Design a partition plan for a toy discussion app with 100 million messages. Pick a partition key; describe loading one conversation; plan for a viral conversation; define shard failure behaviour; explain user deletion; and compare the complexity with one managed relational DB.

## Sources

- Raft: https://raft.github.io/
- PostgreSQL partitioning: https://www.postgresql.org/docs/current/ddl-partitioning.html
- MongoDB sharding: https://www.mongodb.com/docs/manual/sharding/
- Apache Cassandra architecture: https://cassandra.apache.org/doc/latest/cassandra/architecture/overview.html
- Google Spanner paper: https://research.google/pubs/spanner-googles-globally-distributed-database/
