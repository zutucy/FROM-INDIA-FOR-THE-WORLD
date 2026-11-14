# 13A — Distributed systems foundations, consistency and CAP

## 1. What makes a system distributed?

A distributed system consists of independent computers/processes that communicate over a network to provide a service. They do not share one memory, a perfect clock or a single view of reality. Messages can be delayed, duplicated, reordered or lost; machines can crash; networks can partition; and clocks can drift. Partial failure is normal.

A timeout does not prove a remote operation failed. The server may have completed the action while its reply was lost. This is why retries, idempotency and reconciliation matter.

## 2. Why distributed systems evolved

As applications grew beyond one machine, teams needed more storage, throughput, availability and geographic reach. Clusters, distributed databases, CDNs and service-oriented systems divided work. Cloud made distributed components easier to provision, but did not remove the coordination problems. Adding machines can increase capacity yet introduces network calls, consistency questions, observability and operational complexity. Do not distribute a system merely because it sounds modern.

## 3. Failure modes

- Process, host, disk or entire-zone failure.
- Network latency, packet loss or partition.
- Duplicate or reordered events.
- Clock skew and ambiguous timestamps.
- Slow dependency exhausting threads/connections.
- Partial deployment with mixed software versions.
- Region/provider outage.
- Operator error or configuration mistake replicated widely.

Use bounded timeouts, retries, idempotency, circuit breakers, bulkheads, queues, monitoring and recovery. Retrying all errors forever can worsen an outage.

## 4. Consistency models

- **Linearizability:** Operations appear atomic and ordered in real time, respecting completed operations. Useful for high-integrity state but can cost latency/availability across distance.
- **Sequential consistency:** Operations appear in one consistent order, but not necessarily real-time order.
- **Eventual consistency:** If updates stop, replicas should converge; temporary stale reads are possible.
- **Causal consistency:** Causally related operations preserve order while unrelated concurrent operations may be seen differently.

Consistency is a product decision. A stale like count may be tolerable; exposing another person's private message or charging twice is not.

## 5. CAP theorem — common misunderstanding

During a network partition, a distributed data store cannot guarantee both linearizable consistency and availability for every request under the strict CAP model. It must reject/delay some operations to preserve consistency or accept operations that may temporarily diverge.

CAP does **not** mean “pick any two of C, A and P” as a permanent design menu. Partitions are a failure condition. The practical question is what behaviour to provide during a partition and what trade-offs occur in normal operation. PACELC adds a way to reason about latency/consistency when there is no partition.

## 6. Replication and quorum intuition

Replication stores multiple copies. A system may acknowledge a write after one replica, several replicas or a quorum. Quorum relationships such as R + W > N are useful only under particular assumptions; they do not automatically guarantee every consistency property. Real systems also need membership changes, failure detection, stale-replica repair and conflict resolution.

Leader-based systems route writes through a leader. Multi-leader designs allow writes in multiple places and need conflict handling. Leaderless systems may use quorum and reconciliation. Each has trade-offs.

## 7. Time and ordering

Wall-clock timestamps do not form a perfect global order. Clocks drift and messages cross regions. Use sequence numbers, database transaction order, logical clocks or hybrid clocks where causal ordering matters. Do not infer causality only from timestamps.

For streams distinguish **event time** (when it happened) from **processing time** (when consumed). Late events are normal; define allowed lateness, windows and correction policy.

## 8. Exactly-once is bounded

Messages may be delivered at least once, so consumers should handle duplicates. “Exactly once” usually refers to a particular system boundary/transaction model; it does not automatically cover email, payment providers or other external side effects. Idempotency keys, transactional outbox, deduplication and reconciliation are often required.

## 9. Choose consistency per operation

| Operation | Typical need | Possible approach |
|---|---|---|
| Change password | Immediate integrity | Authoritative write, revoke sessions |
| Charge payment | Strong integrity/idempotency | DB transaction + provider idempotency + reconciliation |
| Like a post | Count may be stale; action must be unique | Unique constraint + async count/cache |
| Feed ranking | Small staleness may be fine | Cached feed + refresh |
| Private message | Correct access and durable delivery | Stored message + ordered conversation handling |
| Analytics | Delayed aggregate acceptable | Batch/stream pipeline |

## 10. Exercise

Create two local application instances. Simulate delayed responses and duplicate events. Show how a retry could duplicate an action. Add an idempotency key and test again. Do not use external systems for this experiment.

## Sources

- Gilbert and Lynch, CAP paper: https://users.ece.cmu.edu/~adrian/731-sp04/readings/GL-cap.pdf
- Raft consensus resources: https://raft.github.io/
- AWS Builders' Library: https://aws.amazon.com/builders-library/
- Apache Kafka docs: https://kafka.apache.org/documentation/
