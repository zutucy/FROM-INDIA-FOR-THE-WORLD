# Gap-Fill Supplement — Parts 00–10

**Edition:** 13 November 2026  
**Purpose:** This supplement deepens important implementation topics that were only introduced briefly in some early chapters. It is not a replacement for the numbered chapters. Read the matching chapter first, then use this supplement as the practical engineering layer.

> **How to read this:** Treat every example as a learning pattern. Exact implementation depends on workload, threat model, provider, jurisdiction and team capability. Do not copy production settings without testing them.

---

## 1. Computing history: the missing bridge from machines to modern software

The history of computing is not a straight line where one inventor created the modern computer. It is a chain of ideas solving different constraints: reliable calculation, programmability, storage, interactivity, networking, affordable hardware and global distribution.

### 1.1 From calculation to programmable machines

- **Mechanical calculators** made arithmetic repeatable, but they were not general-purpose electronic computers.
- **Programmable-machine concepts** introduced the idea that instructions and data could be represented in a form a machine could execute. Charles Babbage designed the Analytical Engine; Ada Lovelace wrote notes describing how a general machine might manipulate symbols, not just numbers.
- **Electromechanical and early electronic computers** were developed for scientific, military, codebreaking and administrative needs. Designs differed significantly; “the first computer” depends on whether the definition means electronic, programmable, general-purpose, stored-program or commercially produced.
- **Stored-program architecture** made it practical to keep instructions in memory alongside data. This became a foundational model for general-purpose computers.

### 1.2 Transistors, integrated circuits and microprocessors

Vacuum tubes enabled early electronic computation but consumed substantial power, generated heat and were physically large. Transistors made switching components smaller and more efficient. Integrated circuits placed multiple components on a semiconductor substrate; later advances increased transistor density and manufacturing capability. Microprocessors integrated a CPU onto a chip, helping make personal computers and embedded systems economical.

A simplified hierarchy is:

`transistor → logic gate → arithmetic/control circuit → CPU core → processor package → computer system`

This is simplified because modern processors contain caches, memory controllers, interconnects, accelerators and multiple cores, and not every function is a simple single-level composition.

### 1.3 Mainframes, minicomputers, PCs, phones and cloud

- **Mainframes** centralised expensive computation and storage for institutions.
- **Time-sharing** let multiple people interact with one central machine through terminals.
- **Minicomputers and workstations** made some computing more accessible to departments and engineering teams.
- **Personal computers** moved interactive computing onto desks and into homes.
- **The graphical user interface** made pointing, windows, icons and direct manipulation familiar to non-specialists.
- **Smartphones** combined general-purpose computing, mobile networking, sensors, cameras and app distribution in a pocket-sized device.
- **Cloud computing** made remote compute, storage and managed services available on demand, changing how companies purchase and operate infrastructure.
- **Edge computing** places selected processing closer to users or devices when latency, bandwidth, autonomy or privacy requirements justify it.

Why this history matters: current platforms are built on decades of trade-offs. A cloud virtual machine is still a process running on physical hardware. A mobile app is still software scheduled by an operating system. A “serverless” function still runs on servers managed by a provider.

---

## 2. Hardware and OS: practical internal concepts

### 2.1 Bits, bytes and binary

A **bit** has a value of 0 or 1. A **byte** is conventionally 8 bits. Computers represent numbers, text, images and instructions using encoded bit patterns. Binary is not magic; it is a representation suited to circuits that distinguish physical states reliably.

For storage, distinguish:

- **bit (b)** and **byte (B)**: 8 bits = 1 byte.
- **decimal units**: 1 kB = 1,000 bytes; 1 MB = 1,000,000 bytes.
- **binary units**: 1 KiB = 1,024 bytes; 1 MiB = 1,048,576 bytes.

Network bandwidth is commonly stated in bits per second, while file sizes are usually shown in bytes. A 100 Mb/s link does not mean a 100 MB/s download; the theoretical conversion is 12.5 MB/s before protocol overhead and real-world constraints.

### 2.2 CPU, cache, RAM and storage

A program's data may travel through several levels:

`CPU registers → L1/L2/L3 cache → RAM → SSD/HDD → remote storage`

Generally, smaller and closer memory is faster and more expensive per byte. The hierarchy exists because a processor can execute instructions far faster than large, inexpensive storage can supply arbitrary data.

- **Registers** hold values directly used by CPU instructions.
- **Caches** keep recently or predictably used data near the CPU.
- **RAM** holds active program code and data but is normally volatile.
- **SSD** stores data persistently using flash memory; latency and throughput vary by device and workload.
- **HDD** stores data magnetically on rotating platters; it can be economical for large capacity but has mechanical latency.

A program can be CPU-bound, memory-bound, I/O-bound or network-bound. Adding CPU cores will not fix a slow database query waiting on disk, and a faster SSD will not fix an inefficient algorithm dominated by CPU work.

### 2.3 Boot path and firmware

A simplified machine startup sequence:

1. Power is applied and the processor begins from a platform-defined reset state.
2. Firmware (commonly UEFI on modern PCs) initialises hardware and performs checks.
3. Firmware selects a boot device according to configuration and security policy.
4. A boot manager/loader loads an operating-system kernel and supporting files.
5. The kernel initialises memory management, drivers, scheduling and core services.
6. The init/system manager starts user-space services and login/session processes.

Real devices have architecture-specific details. Secure Boot can verify that early boot components are signed by trusted keys; it reduces certain boot-chain risks but does not guarantee that the whole operating system or application is secure.

### 2.4 Process, thread, file descriptor and socket

- A **process** is an operating-system execution and resource-protection context.
- A **thread** is a schedulable execution path within a process; threads often share process memory.
- A **file descriptor/handle** is a process-visible reference to an open resource, such as a file or socket.
- A **socket** is an OS abstraction for network communication.

A backend that opens a new database connection per request can exhaust database connection limits. Production applications typically use a bounded connection pool, timeouts and backpressure.

---

## 3. Browser and frontend: what actually happens after a page opens

### 3.1 Navigation and rendering lifecycle

A simplified browser navigation:

1. User enters a URL or follows a link.
2. Browser parses the URL and checks relevant caches, policies and service-worker interception.
3. DNS resolution finds an address when needed.
4. A transport connection is established (TCP + TLS, or QUIC with TLS in HTTP/3).
5. Browser sends an HTTP request and receives response headers/body.
6. HTML is parsed into the **DOM** (Document Object Model).
7. CSS is parsed into the **CSSOM** (CSS Object Model).
8. Browser calculates styles, builds layout information, paints and composites layers.
9. JavaScript may modify the DOM, styles and application state, causing more work.

This is a simplified model. Browsers stream responses, preload resources, execute scripts at different times, use multiple processes and optimise rendering. Some tasks happen concurrently.

### 3.2 Critical rendering concepts

- **DOM:** structured representation of document nodes.
- **CSSOM:** parsed style rules and computed styling inputs.
- **Layout/reflow:** calculation of element geometry and positions.
- **Paint:** drawing visual properties into rendering surfaces.
- **Compositing:** combining layers, sometimes with GPU acceleration.
- **Long task:** work that blocks the main thread long enough to harm responsiveness.

Changing `transform` or `opacity` can sometimes be handled more cheaply than changing layout-affecting properties such as width or height, but this is not a universal guarantee. Measure with browser developer tools rather than relying on slogans.

### 3.3 JavaScript event loop

JavaScript in a browser usually runs application code on a main thread, although workers and browser internals add concurrency. The event loop coordinates tasks and microtasks.

- **Tasks** include events such as timers, user input and message events.
- **Microtasks** include Promise reactions and `queueMicrotask` callbacks; they are generally drained after the current task before the browser proceeds to the next rendering opportunity.
- **Rendering** can occur between tasks when the browser determines it should update the screen.

A long synchronous loop blocks input and painting. Use asynchronous I/O, chunk expensive work, Web Workers for suitable CPU-heavy tasks, and cancellation when the user navigates away.

### 3.4 React rendering is not the same as DOM painting

React components describe UI from state and props. When relevant state changes, React renders components to calculate the next UI representation, then commits necessary updates. The browser still performs style, layout, paint and compositing work.

Practical rules:

- Keep state as local as sensible; avoid making every keystroke re-render an enormous tree.
- Use stable keys for list items so reconciliation can identify elements.
- Avoid storing derived values in state when they can be calculated from existing state.
- Use memoisation only after identifying a real performance issue; unnecessary memoisation adds complexity.
- Treat effects as synchronisation with external systems, not as a default place for every calculation.
- Abort or ignore stale network responses when a user changes a search query quickly.

### 3.5 Frontend security and browser storage

- `localStorage` persists data per origin and is readable by JavaScript. A successful XSS attack can read it.
- `sessionStorage` is scoped to a tab/session but remains JavaScript-accessible.
- Cookies can be configured with `HttpOnly`, `Secure` and `SameSite`; these flags reduce specific risks but must be paired with correct CSRF and session design.
- IndexedDB stores structured client-side data; it is not a trusted server database.
- Service workers can intercept requests and support offline experiences, but they introduce lifecycle, cache invalidation and security considerations.

Do not store long-lived sensitive credentials in JavaScript-readable storage without a deliberate threat-model decision. The correct session architecture depends on the app type, origin model, API design and browser/native clients.

### 3.6 Frontend internationalisation and accessibility

A global application needs more than translated strings. Consider language negotiation, right-to-left layout, date/time formats, number/currency formats, pluralisation, text expansion, font coverage, input methods and local content policy. Accessibility needs semantic HTML, keyboard access, visible focus, contrast, captions/transcripts, accessible names and screen-reader testing. A visually polished UI can still be inaccessible.

---

## 4. Backend and API: robust request handling

### 4.1 Request lifecycle

A typical API request passes through:

`network listener → reverse proxy/load balancer → routing → request ID → size/rate limits → authentication → authorization → input validation → business logic → database/services → response serialization → logs/metrics`

The order varies. For example, some cheap request-size or IP-based controls should run before expensive authentication. Authorization must occur before returning protected data. Never rely on the frontend to enforce a permission.

### 4.2 Timeouts, retries and idempotency

Networks fail in ambiguous ways. A client may send a payment or post-creation request; the server may commit the action but the response may be lost. The client sees a timeout but cannot know whether the operation succeeded.

**Idempotency** means repeating the same operation with the same key produces one logical result, rather than duplicating side effects. Typical design:

1. Client generates a high-entropy idempotency key for one intended operation.
2. Server stores key, user/account scope, request fingerprint and result/operation state.
3. A repeated request with the same key and same logical payload returns the saved result or current state.
4. Reusing the key with a different payload is rejected.
5. Keys expire according to a documented retention policy.

Retries should be limited, use backoff with jitter, respect `Retry-After` where relevant and only be used where the operation is safe or idempotent. Retrying every failure immediately can amplify an outage.

### 4.3 API design essentials

- Define request and response schemas.
- Validate types, ranges, lengths, formats and allowed enum values server-side.
- Use consistent error shapes with stable machine-readable codes.
- Distinguish authentication failure, permission failure, missing resource, invalid input, conflict, rate limiting and server failure.
- Paginate list endpoints; enforce maximum page sizes.
- Define sorting/filtering allowlists to prevent arbitrary expensive queries.
- Version APIs only when compatibility requires it; prefer additive changes where possible.
- Document deprecation and sunset timelines.
- Avoid leaking stack traces, SQL messages, secret values or internal hostnames in production errors.

### 4.4 Webhooks

A webhook is an outbound HTTP event sent to another system. A reliable webhook design needs:

- Signed payloads and timestamp validation.
- Secret rotation.
- Replay protection.
- Delivery IDs and idempotent receivers.
- Retries with backoff and a maximum retention window.
- Dead-letter state and operator visibility.
- A way to inspect/replay a failed event safely.
- Clear ordering guarantees—or explicit disclosure that delivery may be out of order.

A webhook endpoint must not trust the request simply because it came from a familiar-looking IP address.

### 4.5 Rate limiting and abuse controls

Rate limits can be applied by account, IP, API key, device signal or resource. Each has limitations: NAT can group many legitimate users behind one IP; attackers can rotate IPs; attackers can create accounts. Use layered signals, adaptive thresholds, per-operation cost, abuse review and user-friendly recovery paths. Avoid exposing enough detail for attackers to tune around the control.

---

## 5. Databases: query plans, locks and safe change management

### 5.1 Indexes are data structures with costs

An index can make reads faster by allowing the database to locate rows without scanning every row. But indexes consume storage and add work to inserts, updates and deletes.

Common index families include B-tree, hash, GIN/GiST and full-text indexes, but availability and behaviour vary by database engine. Composite index column order matters. An index on `(tenant_id, created_at)` can serve patterns that constrain `tenant_id` and sort/filter by `created_at`, but may not be ideal for a query that only constrains `created_at`.

Use the database's query-plan tool (for PostgreSQL, `EXPLAIN` and optionally `EXPLAIN ANALYZE`) to inspect scans, join strategies, estimated/actual row counts and costs. `EXPLAIN ANALYZE` executes the query, so use care with expensive or mutating statements.

### 5.2 Transactions and isolation anomalies

ACID is a useful foundation:

- Atomicity: all-or-nothing transaction behaviour.
- Consistency: constraints remain satisfied when operations succeed.
- Isolation: concurrent transactions behave according to the isolation level.
- Durability: committed changes survive failures within the database's guarantees.

Isolation levels matter. Concurrent transactions can produce anomalies such as non-repeatable reads, phantom reads or write skew, depending on engine and isolation level. Serializable isolation aims to make concurrent execution equivalent to some serial order, but can abort transactions and require application retry logic.

A transaction should be as short as practical. Do not hold database locks while calling a slow external API. Use an outbox or state machine for cross-system workflows rather than assuming a database transaction can atomically commit a remote payment, email or object-storage write.

### 5.3 Deadlocks and connection pools

A deadlock can occur when transactions wait for locks held by one another. Keep transactions short, acquire rows/resources in a consistent order where possible, and handle retryable deadlock/serialization errors. Connection pools should be bounded and sized across all application instances; if every instance has a large pool, total connections can exceed the database capacity.

### 5.4 Schema migrations

Use version-controlled, repeatable migrations. For zero/low downtime changes, favour expand-and-contract:

1. Add a new nullable or default-compatible field/table.
2. Deploy code that can read old and new representations.
3. Backfill data in controlled batches, measuring load.
4. Switch writes/reads to the new representation.
5. Validate data and remove old paths only after all old application versions are gone.

A migration that locks a huge table or rewrites every row can create an outage. Test against realistic data volume and engine version.

### 5.5 Backups, point-in-time recovery and restore drills

A backup is not proven until a restore has succeeded. Define:

- RPO: acceptable amount of recent data loss.
- RTO: acceptable recovery duration.
- Backup frequency and retention.
- Encryption and separate credentials.
- Geographic/account isolation where required.
- Restore test schedule.
- Dependency restore order (database, object storage, keys, configuration, search indexes).

Replication is not a backup: accidental deletion or corruption can replicate too. Object storage and database backups need coordinated retention and deletion policies.

---

## 6. Media, streaming, search and real-time systems

### 6.1 Direct-to-object-storage upload

A robust upload flow often looks like:

1. Client asks the API for an upload session.
2. API authenticates/authorises, checks quota and creates a pending asset record.
3. API returns a short-lived, narrowly scoped signed upload URL or multipart upload instructions.
4. Client uploads directly to object storage.
5. Storage event or client completion signal triggers server-side verification.
6. Worker checks file signature, size, integrity and policy; scans or quarantines as appropriate.
7. Media processor generates safe derivatives/thumbnails/transcodes.
8. Database changes state to ready only after required outputs are verified.
9. Application exposes an authorised playback/download route or token.

Never assume a filename extension or browser-supplied content type proves the file's true type. Apply quotas, decompression limits, timeouts and isolated processing.

### 6.2 HLS and MPEG-DASH overview

Adaptive bitrate streaming splits media into small segments and provides a manifest describing available renditions. The player measures network/buffer conditions and chooses an appropriate rendition.

- **HLS** uses playlists and media segments; it is widely supported across Apple ecosystems and other modern players.
- **MPEG-DASH** is a related adaptive streaming standard.
- **CMAF** can allow compatible fragmented MP4 media to be reused across streaming ecosystems, depending on packaging and player support.

Adaptive bitrate is not merely “make 1080p and 720p files.” It includes segment duration, keyframe alignment, manifests, codecs, player selection, startup delay, buffering and CDN cache behaviour.

### 6.3 CDN design and invalidation

A CDN caches content at edge locations. Cache keys may include hostname, path, query parameters and selected headers. Incorrect cache-key design can cause one user's private response to be served to another user. Private content should not be placed in a shared cache unless the authorisation design explicitly makes it safe.

Versioned immutable asset URLs simplify cache management. For mutable content, use appropriate cache-control headers, revalidation and purge strategy. Signed URLs/tokens must expire appropriately and must not be logged carelessly.

### 6.4 Real-time messaging and WebRTC

WebSockets provide a persistent, two-way application channel, but they need authentication, heartbeat/timeouts, reconnect handling, backpressure, per-connection limits and multi-instance routing. Do not treat a WebSocket connection as proof that a user still has permission to receive every event; permissions can change after connection.

WebRTC supports real-time media/data communication. STUN helps peers discover network address mappings; TURN relays traffic when direct connectivity fails. TURN bandwidth can be significant. Signalling (offer/answer and ICE candidates) is usually handled by a separate application channel. Secure calling also requires identity, permissions, abuse controls and metadata privacy decisions.

### 6.5 Search indexing is eventually consistent

A database commit and search-index update are often separate systems. A post may appear in the database before it appears in search. Model this as an explicit lifecycle: committed → event/outbox → indexing job → indexed. Provide retry and reconciliation. Deletion and privacy changes must propagate to caches and indexes, not just the primary database.

---

## 7. Cloud, deployment and operations: avoid fragile releases

### 7.1 Cloud shared responsibility

Cloud providers secure parts of the underlying infrastructure; customers remain responsible for what they configure and deploy. The boundary differs for IaaS, PaaS and SaaS. A managed database does not automatically make application-level access control, credentials, backups, data retention or query design safe.

### 7.2 Identity and least privilege in cloud

Use separate roles for deployment, runtime applications, humans and emergency access. Prefer short-lived workload identity/roles over long-lived static keys. Restrict permissions to the resources and actions required. Separate production from development accounts/projects where practical. Log privileged actions and test emergency-access procedures.

### 7.3 Infrastructure as Code

Infrastructure as Code describes resources in version-controlled configuration. It makes review and repeatability possible, but a faulty change can destroy or expose resources at scale. Use state protection, plan/review steps, policy checks, environment separation, secret handling and controlled approvals. Never commit credentials into IaC files or state artifacts without appropriate protection.

### 7.4 Deployment strategies

- **Rolling deployment:** gradually replaces old instances.
- **Blue/green:** keeps two environments and switches traffic after validation.
- **Canary:** sends a small traffic percentage to the new version and increases gradually if metrics stay healthy.
- **Feature flag:** deploys code while controlling exposure separately.

A rollback is not always as simple as switching code. Database migrations, emitted events, external side effects and mobile clients can make rollback unsafe. Prefer backward-compatible changes and define forward-fix or data-repair plans.

### 7.5 SLI, SLO and error budgets

- **SLI:** measured indicator of service behaviour, such as successful request ratio or latency.
- **SLO:** target for that indicator over a time window.
- **SLA:** external commitment with business/legal consequences, often including remedies.
- **Error budget:** allowable unreliability implied by an SLO.

Example: if a monthly availability target is 99.9%, the theoretical error budget is roughly 0.1% of the measurement window. Define exactly what counts as a valid request, what is excluded and how partial failures are measured. An SLO is a decision tool, not a decorative badge.

### 7.6 Capacity and cost modelling

Estimate cost from workload drivers, not registered-user counts alone:

`monthly cost ≈ compute + database + storage + requests + egress + media processing + observability + support + backups`

Model average and peak load separately. Video platforms may spend heavily on egress; a messaging app may spend more on persistent connections and event throughput; an analytics product may spend heavily on scans and retention. Set budget alerts and per-user/per-feature cost attribution where possible.

---

## 8. Cross-cutting design reviews before a public launch

Use this review for any product, not only social networks.

### 8.1 Data-flow review

For every data type, document:

- Source and purpose.
- Sensitivity and user expectation.
- Collection and legal basis/consent where applicable.
- Systems, regions, backups and vendors that receive it.
- Access roles and audit controls.
- Retention, deletion and legal hold rules.
- Whether it is used for analytics, advertising, AI training or personalisation.
- How a user request or incident propagates through derived systems.

### 8.2 Threat-model review

Identify assets, trust boundaries, actors, entry points, abuse cases, impact and mitigations. Threat models change as a product adds file uploads, payments, private messaging, federation, AI agents or third-party integrations.

### 8.3 Failure-mode review

Ask what happens when:

- Database is unavailable.
- Cache returns stale data.
- Queue backlog grows.
- Object storage upload partially completes.
- CDN serves stale content.
- Email/OTP provider is down.
- A third-party API times out.
- A release contains a breaking migration.
- An admin account is compromised.
- A data deletion job fails halfway.

For each failure, define detection, containment, recovery, user communication and evidence retention.

### 8.4 Product-quality review

Review accessibility, localisation, performance on low-end devices, slow networks, browser differences, account recovery, data export/deletion, parental/child-safety scope where relevant, abuse reporting and customer support capacity.

---

## 9. Practical mini-labs

Perform these only on your own machine, own cloud project or explicitly authorised test systems.

1. **Browser lifecycle:** Open developer tools, use the Network panel and inspect document, CSS, JS, image and API requests. Compare cold-cache and warm-cache navigation.
2. **Rendering:** Use Performance profiling to identify a long task. Refactor it into chunks or move suitable computation to a Web Worker. Compare responsiveness before/after.
3. **API reliability:** Build a toy create-order endpoint with an idempotency key. Simulate a response timeout and repeat the same request. Confirm there is only one logical order.
4. **Database plan:** Create a sample table with realistic rows. Compare a query before and after an appropriate index using the database's query-plan tool. Record read improvement and write/storage cost.
5. **Migration:** Add a nullable column, backfill in batches and then make the application use it. Practise the expand-and-contract pattern.
6. **Upload validation:** Upload a file with a misleading extension to a local test service. Confirm server-side file-signature validation rejects or quarantines it.
7. **Cache safety:** Create a public endpoint and a private user endpoint. Verify that private responses are never shared across users by cache configuration.
8. **Deployment:** Use a staging environment and a feature flag. Deploy a small UI/backend change, observe metrics and disable the flag to practise rollback of exposure.
9. **Recovery:** Back up a disposable local database, delete it and restore it. Measure actual recovery time; do not assume the backup works.
10. **Cost model:** Estimate monthly cost for 1,000, 10,000 and 100,000 active users using explicit requests/user, bytes/user, media minutes and retention assumptions. Label assumptions rather than presenting estimates as facts.

---

## 10. Quick-reference design rules

- A frontend check is not backend authorisation.
- A successful upload request is not proof that the file is safe or ready to publish.
- A cache is not the source of truth.
- A replica is not a backup.
- A timeout does not prove an operation failed.
- A successful database write does not mean search, analytics and CDN caches have updated.
- A deployment rollback may not undo a database migration or external side effect.
- Encryption does not fix excessive access privileges.
- A privacy policy does not implement a deletion workflow.
- A load test without representative traffic assumptions does not prove scale.
- A high user count does not automatically mean high revenue.
- A managed cloud service reduces some operational work, not all responsibility.
- Measure bottlenecks before scaling infrastructure.
- Prefer the simplest architecture that meets measured requirements and has a credible growth path.

## Further primary references

- WHATWG HTML Living Standard: https://html.spec.whatwg.org/
- W3C WAI resources: https://www.w3.org/WAI/
- MDN Web Docs: https://developer.mozilla.org/
- React documentation: https://react.dev/learn
- PostgreSQL documentation: https://www.postgresql.org/docs/current/
- HTTP Semantics, RFC 9110: https://www.rfc-editor.org/rfc/rfc9110
- HTTP/3, RFC 9114: https://www.rfc-editor.org/rfc/rfc9114
- WebRTC standards overview: https://www.w3.org/TR/webrtc/
- HLS specification resources: https://developer.apple.com/streaming/
- NIST Secure Software Development Framework, SP 800-218: https://csrc.nist.gov/pubs/sp/800/218/final
- NIST Cybersecurity Framework 2.0: https://www.nist.gov/cyberframework
- Google SRE books: https://sre.google/books/
- OpenTelemetry documentation: https://opentelemetry.io/docs/
