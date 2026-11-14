# 09C — Search, Messaging, Notifications and Real-time Systems

## 1. Search is more than a text box

A search product has ingestion, indexing, query parsing, ranking, filtering, suggestions, typo handling, access control, analytics and deletion propagation. Start by identifying what people need to find: exact usernames, titles, hashtags, places, documents, public posts or private workspace content. Each search type has different relevance and privacy requirements.

## 2. Indexing and ranking

An index is a derived structure optimised for retrieval. A typical content indexing flow:

1. A database transaction stores or updates a record.
2. A reliable event/outbox signals an indexing job.
3. Worker extracts allowed searchable fields.
4. Text is normalised/tokenised and indexed.
5. Query engine retrieves candidates.
6. Application applies visibility and permission filters.
7. Ranking sorts eligible results.
8. Results are paginated and returned.

The search index should not become an accidental authority for access rights. Re-check permissions against a trusted source or design a robust permission filter. Deleted, private or blocked content must stop appearing within documented propagation time.

## 3. Search engines

PostgreSQL full-text search may be enough for early products. OpenSearch/Elasticsearch-style engines support more sophisticated text search, facets, analyzers and distributed indexing. Hosted search services reduce operations but introduce provider dependency, data-transfer considerations and cost. Choose based on relevance requirements and scale.

## 4. Real-time communication

### Polling

Client periodically asks for new data. Simple, but can waste requests and adds delay.

### Long polling

Client opens a request that the server holds until data is available or timeout occurs. It can reduce polling overhead but requires connection/resource management.

### Server-Sent Events (SSE)

Server streams one-way events to the browser over HTTP. Useful for notifications/status updates when client-to-server messaging can use normal HTTP.

### WebSocket

Provides a persistent, bidirectional connection. Useful for chat, presence and collaborative interaction. It adds connection lifecycle, authentication, fan-out, heartbeat, reconnect, backpressure and multi-instance coordination concerns.

### WebRTC

Supports real-time audio/video/data communication, usually with signalling and network traversal components. It is a separate technical challenge from normal chat.

## 5. Messaging model

A basic messaging system may include conversations, members, messages, attachments, receipts, per-user read state, moderation/report state and retention rules. Define message ordering scope (usually within a conversation), duplicate handling, edit/delete semantics, blocked-user behaviour, group membership changes and export/deletion policy.

Messages should be persisted durably before the sender is told that delivery is safely accepted. Delivery to another device can happen asynchronously. Presence (online/typing) is ephemeral and should not be treated as durable truth.

## 6. Real-time scaling

For many connections, manage connection limits, keepalive/heartbeat, reconnect with jitter, authentication expiry, per-user fan-out and backpressure. A message broker or pub/sub layer may distribute events among instances. Do not broadcast every event to every connection. Partition by conversation/tenant/topic and enforce privacy at subscription and publish time.

## 7. Notifications

Separate **notification events** from **delivery channels**:

- in-app notification record;
- email;
- mobile push;
- SMS only when justified.

User preferences, quiet hours, rate limits, deduplication and abuse controls matter. A like notification storm should be grouped or throttled. Do not reveal sensitive text on lock screens by default without a deliberate privacy choice.

Push providers include Apple Push Notification service and Firebase Cloud Messaging. Device tokens can change, expire or be invalidated; manage them as sensitive identifiers and remove invalid registrations.

## 8. Email and account messages

Use a reputable transactional email provider, configure SPF, DKIM and DMARC for domain authentication, monitor bounce/complaint rates and separate transactional from marketing messages. Do not send passwords in email. Password-reset and verification links should be short-lived, one-time where practical and protected from referrer leakage.

## 9. Practical lab

Build a small search endpoint with access filters. Then implement one-way SSE for job status. Next, build WebSocket chat with durable database writes, duplicate event IDs, reconnection, membership permission checks and rate limits. Test with two app instances to expose assumptions hidden by a single-process demo.

## Further reading

- OpenSearch docs: https://opensearch.org/docs/latest/
- MDN WebSocket API: https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API
- MDN Server-sent events: https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events
- WebRTC: https://webrtc.org/getting-started/overview
- Apple Push Notifications: https://developer.apple.com/documentation/usernotifications
- Firebase Cloud Messaging: https://firebase.google.com/docs/cloud-messaging
