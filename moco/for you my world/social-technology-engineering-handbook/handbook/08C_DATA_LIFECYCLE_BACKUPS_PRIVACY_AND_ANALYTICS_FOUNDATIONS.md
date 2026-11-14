# 08C — Data Lifecycle, Backups, Privacy and Analytics Foundations

## 1. Data lifecycle

A responsible system defines how data is created, validated, stored, used, shared, archived, retained and deleted. Different data classes need different policies: account credentials, public posts, private messages, payment records, security logs, analytics events and backups are not interchangeable.

For each class record:

- owner/controller and service responsibility;
- purpose and lawful basis where relevant;
- sensitivity and access roles;
- source and downstream recipients;
- primary store and replicas/caches/indexes;
- retention and deletion triggers;
- backup and legal-hold behaviour;
- encryption and audit requirements.

## 2. Data classification

A practical classification model might be:

- **Public:** deliberately published and approved for public visibility.
- **Internal:** operational information not intended for public release.
- **Confidential:** customer/business data with restricted access.
- **Restricted:** credentials, authentication secrets, private messages, sensitive identifiers or regulated data.

This is a company policy classification, not a universal legal classification. Map it to applicable laws and contracts.

## 3. Backups

Backups are copies intended for recovery, not just extra replicas. Common methods:

- full backups;
- incremental backups;
- differential backups;
- write-ahead-log / point-in-time recovery where supported;
- snapshots (with consistency guarantees understood).

A backup plan specifies frequency, retention, encryption, access controls, geographic failure domains, immutability where appropriate, restore objectives and verification. The only reliable backup is one you have restored successfully in a test.

## 4. RPO and RTO

- **RPO (Recovery Point Objective):** maximum acceptable data loss measured in time.
- **RTO (Recovery Time Objective):** target time to restore service.

A product with a 15-minute RPO needs a backup/logging/replication design capable of meeting it under realistic failures. RTO must include detection, decision, access, restoration, validation, DNS/routing and user communication—not merely database startup time.

## 5. Analytics event design

An event should represent a meaningful action, not every UI pixel change. Example event schema:

```json
{
  "event_id": "uuid",
  "event_name": "video_playback_started",
  "occurred_at": "2026-11-13T12:00:00Z",
  "actor_id_pseudonymous": "...",
  "object_id": "...",
  "session_id": "...",
  "properties": {"surface": "home_feed"},
  "schema_version": 1
}
```

Do not place passwords, tokens, private message bodies or unnecessary personal data in analytics events. Define event names, units, deduplication and schema versioning. Keep telemetry purpose-limited.

## 6. Data pipeline basics

An event may be collected by an SDK/server, validated, written to a durable event stream, transformed, deduplicated and loaded into an analytical store. Dashboards and experiments then query aggregated data. Operational analytics and product analytics may need different access policies and retention.

Beware of sampling, bot traffic, ad blockers, duplicate retries, time-zone boundaries, late events and changing definitions. “View” must have a written definition. Do not compare two dashboards that count different things as if they measure the same metric.

## 7. Account export and deletion

A user-facing data export should be machine-readable, documented and scoped to data the user has a right to receive. Account deletion should remove or de-identify data in primary systems and propagate to derived systems according to policy and law. Backups may expire on a separate documented cycle; restored backups must reapply deletion tombstones or otherwise ensure previously deleted data is not resurrected.

## 8. Data quality

Set checks for:

- missing/invalid identifiers;
- duplicate events;
- impossible timestamps;
- schema drift;
- orphan references;
- unexpected null rates;
- sudden volume changes;
- delayed pipeline freshness.

Data correctness affects recommendations, billing, safety and product decisions. Treat it as an engineering responsibility.

## 9. Practical lab

Create a data inventory for a small app. Define retention and deletion for accounts, public posts, private messages, logs and analytics. Implement a backup, restore it into a test database, then verify that account-deletion requests remain honoured after restore.

## Further reading

- NIST Privacy Framework: https://www.nist.gov/privacy-framework
- NIST Cybersecurity Framework: https://www.nist.gov/cyberframework
- PostgreSQL backup and restore: https://www.postgresql.org/docs/current/backup.html
- Google Cloud data governance: https://cloud.google.com/architecture/framework/security
