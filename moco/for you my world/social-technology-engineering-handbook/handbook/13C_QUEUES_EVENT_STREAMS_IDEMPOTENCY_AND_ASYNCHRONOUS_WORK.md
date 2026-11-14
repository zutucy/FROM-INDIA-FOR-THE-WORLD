# 13C — Queues, event streams, idempotency and asynchronous work

## 1. Why asynchronous processing exists

A user request should not wait for every secondary task. Publishing a video may require storing metadata immediately while transcoding, thumbnail generation, notifications, search indexing and analytics happen later. A queue or event stream separates producers from consumers, improves responsiveness and absorbs bursts, but introduces delay, retries, duplicates, ordering and monitoring work.

## 2. Work queue versus event stream

A work queue distributes jobs to workers; a job may be acknowledged when complete. An event stream stores an ordered sequence of events that multiple consumer groups can read independently and sometimes replay. Products may combine these patterns, but their semantics differ.

| Concern | Work queue | Event stream |
|---|---|---|
| Main purpose | Perform a task | Record and distribute events |
| Consumers | Often competing workers | Independent consumer groups |
| Replay | May expire after acknowledgement | Retained according to policy |
| Ordering | Depends on broker/partition | Often per partition/key |
| Example | Generate thumbnail | `video_published` event |

## 3. Delivery semantics

- **At-most-once:** May lose a message but does not redeliver under the defined guarantee.
- **At-least-once:** Retries until acknowledged; duplicates are possible.
- **Exactly-once within a boundary:** A bounded processing guarantee, not an automatic guarantee for external side effects.

Design consumers as if duplicates will happen. Use durable event IDs and idempotent handlers. For a notification worker, a unique processed-event record can prevent duplicate notification creation; the insert and side effect need careful transaction design.

## 4. Retries and dead letters

Use bounded retries with exponential backoff and jitter for transient failures. Do not endlessly retry permanent validation errors. Send exhausted jobs to a dead-letter queue with enough metadata to diagnose but no unnecessary personal content. Give the queue an owner and replay procedure.

A poison message repeatedly crashes a consumer. Isolate it, alert the owner and prevent it blocking unrelated work. Replaying dead letters may duplicate effects, so idempotency remains necessary.

## 5. Backpressure and overload

If producers outpace workers, backlog grows. Monitor queue depth, oldest-message age, processing duration, retry count and worker saturation. Backpressure can reject/defer low-priority work, reduce ingestion, scale workers within limits or degrade gracefully. A queue moves load in time; it does not create infinite capacity. Retention, storage and maximum acceptable delay still matter.

## 6. Ordering and partition keys

Many brokers preserve order only inside one partition or key. Chat order may be keyed by conversation ID or handled with explicit sequence numbers. One global key may create a bottleneck. Global ordering across partitions adds coordination and cost.

## 7. Transactional outbox and CDC

The dual-write problem occurs when an app updates a database and separately publishes an event: either may succeed while the other fails. A transactional outbox writes business state and an outbox event in one DB transaction; a publisher forwards it later. Consumers still need deduplication.

Change Data Capture (CDC) reads database log changes. It is useful for replication/integration, but a row update such as `status=3` may be less meaningful than a domain event like `subscription_cancelled`.

## 8. Real-time systems

WebSockets are bidirectional; Server-Sent Events are one-way server-to-client; mobile push is best-effort delivery and not necessarily immediate. Design reconnect, duplicate delivery, offline state and synchronization.

For messaging, store the authoritative message first, then send a live notification. On reconnect the client fetches missing records using a cursor/sequence. A socket event is a delivery hint, not the only copy of a message.

## 9. Exercise

Build a local thumbnail queue. Simulate a worker crash after processing but before acknowledgement; observe duplicate work; add idempotency and a dead-letter path; throttle workers and watch oldest-message age. Use only systems you own.

## Sources

- Apache Kafka documentation: https://kafka.apache.org/documentation/
- RabbitMQ reliability guide: https://www.rabbitmq.com/docs/reliability
- AWS retry/backoff guidance: https://aws.amazon.com/builders-library/timeouts-retries-and-backoff-with-jitter/
- Transactional outbox pattern: https://microservices.io/patterns/data/transactional-outbox.html
