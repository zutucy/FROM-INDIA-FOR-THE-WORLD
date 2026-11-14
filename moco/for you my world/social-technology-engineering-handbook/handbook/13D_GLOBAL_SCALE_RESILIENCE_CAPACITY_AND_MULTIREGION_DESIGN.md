# 13D — Global scale, resilience, capacity and multi-region design

## 1. Scale is a workload, not a vanity number

“Ten million users” is not enough to size infrastructure. Registered accounts, monthly active users, daily active users, peak concurrent sessions, requests/second, database operations, storage growth and video bandwidth are different measures.

Estimate peak requests by endpoint, read/write ratio, p50/p95/p99 latency, payload size, upload/download volume, queue arrival/processing rate, DB demand and user geography. Measure production and run realistic load tests. A benchmark using one cached record may not represent actual traffic.

## 2. Capacity planning

If a service needs to handle 20,000 requests/second and one instance safely handles 500 requests/second at the required latency, arithmetic suggests 40 instances before headroom and failure capacity. Real demand depends on request mix, database limits, autoscaling delay and tail latency; benchmark it.

Plan for N+1 capacity where appropriate: after one node/instance fails, remaining capacity still serves critical functions. Decide what may degrade: recommendations can be disabled while login, privacy settings and essential messaging remain available.

## 3. Caching

Caching reduces repeated work but introduces invalidation, staleness and privacy risks. Cache keys must include user/tenant/permission context when responses differ by identity. Never cache a private response publicly. Set TTLs by freshness requirements and invalidate high-impact changes. Layers include browser, CDN, reverse proxy, app cache, Redis and DB buffer cache; each has different failure modes.

## 4. Multi-region choices

- **Single region with backups:** Simpler early on; failover may take longer and distant users may see higher latency.
- **Active-passive:** One region serves; another is ready. Requires replication, failover tests and clear write authority.
- **Active-active:** Multiple regions serve concurrently. Reduces some latency but makes conflict resolution, identity, data locality, routing and consistency more complex.

Choose based on user geography, latency, legal obligations, recovery objectives and budget—not because “global” sounds impressive.

## 5. Failover and split brain

Avoid two regions both believing they are authoritative for the same writes. Use well-defined leader/lease/fencing or managed-service guarantees. DNS failover alone does not solve data consistency. Test in-flight requests, queues, scheduled jobs and idempotency keys during failover.

## 6. SLI, SLO and SLA

An **SLI** is a measured indicator (successful logins, video-start latency). An **SLO** is an internal target over a period. An **SLA** is a contractual promise, often with remedies. They are related but not interchangeable.

Example SLO: 99.9% of authenticated API requests succeed over a rolling 30-day window, excluding defined client errors. The exact definition matters. A broad uptime number can hide a broken key workflow.

An error budget helps balance reliability and change. If the budget is spent quickly, teams may pause risky releases and focus on stability. Targets should reflect user need and service criticality.

## 7. Graceful degradation and isolation

If recommendations fail, show chronological content. If analytics is unavailable, queue events within a bounded retention budget. Isolate slow noncritical vendors so they cannot exhaust all application resources. Timeouts, bounded retries, circuit breakers, bulkheads, load shedding and backpressure reduce cascading failure, but need tests and tuning.

## 8. CDN and global delivery

CDNs cache eligible content closer to users. Public immutable assets are straightforward; private content needs signed URLs/cookies or authorization-aware delivery. Cache invalidation, key rotation, regional restrictions and deletion propagation matter. CDN logs can contain IP addresses and URL tokens, so apply privacy controls and retention.

## 9. Cost-aware scale

Track unit cost: per active user, video hour watched, upload, transaction or AI request. Storage and bandwidth may grow while compute stays stable. Use budgets, alerts, lifecycle policies and realistic egress estimates before choosing cross-region patterns.

## 10. Game days

Simulate one failure at a time in a controlled environment: database unavailable, queue backlog, expired credentials, CDN origin failure, region unreachable, bad deployment, corrupt cache or exhausted storage quota. Verify alerts, runbooks and recovery objectives. Do not run destructive chaos experiments in production without authorization, containment and rollback.

## Sources

- Google SRE books: https://sre.google/books/
- AWS Well-Architected Reliability Pillar: https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/
- Kubernetes architecture: https://kubernetes.io/docs/concepts/architecture/
- Cloudflare learning center: https://www.cloudflare.com/learning/
