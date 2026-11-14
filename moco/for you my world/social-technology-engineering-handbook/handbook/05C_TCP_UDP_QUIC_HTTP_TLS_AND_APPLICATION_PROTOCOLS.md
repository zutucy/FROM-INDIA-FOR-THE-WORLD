# 05C — TCP, UDP, QUIC, HTTP, TLS and Application Protocols

**Series:** Technology Foundations  
**Edition:** English 1.0  
**Purpose:** Understand how network data is delivered to the correct application, how common transport and application protocols work, and how modern Web communication is protected.

---

## 1. Chapter goal

Part 05B explained IP addresses and routing. This chapter moves one layer higher: once a packet reaches a device, how does the operating system know which application should receive the data? Why do TCP, UDP and QUIC exist? How do HTTP and HTTPS work? When should an application use WebSocket, Server-Sent Events or WebRTC?

## 2. An IP address is not enough: which application should receive the data?

A computer may run a browser, email client, game, database, video call and many other programs at the same time. IP addresses identify network interfaces, but transport-layer port numbers help direct traffic to the appropriate service or process.

A network endpoint is often described as an IP address plus a transport protocol and port. For example:

```text
203.0.113.20:443 over TCP
```

This is a documentation address and an example only. The port is not a security boundary by itself. Firewalls and application permissions determine whether traffic is allowed.

Common ports include:

| Port | Common service | Note |
|---:|---|---|
| 22 | SSH | Secure remote administration; restrict access |
| 25 | SMTP | Server-to-server mail transfer in common deployments |
| 53 | DNS | Traditional DNS over UDP or TCP |
| 80 | HTTP | Unencrypted Web traffic; commonly redirected to HTTPS |
| 123 | NTP | Network time synchronisation |
| 443 | HTTPS | HTTP protected by TLS; HTTP/3 uses QUIC over UDP |
| 587 | Mail submission | Common authenticated email submission port |
| 993 | IMAPS | IMAP over TLS |

Port assignments and actual deployments can differ. Do not assume that a service always runs on its default port.

## 3. TCP: reliable, ordered byte-stream transport

Transmission Control Protocol (TCP) provides a connection-oriented byte stream between endpoints. It handles sequencing, acknowledgements, retransmission, flow control and congestion control. TCP does not understand application messages by itself; applications must define their own framing or message format.

### TCP three-way handshake (simplified)

A common TCP connection setup uses:

1. **SYN:** Client requests a connection and proposes initial sequence information.
2. **SYN-ACK:** Server acknowledges and sends its own SYN information.
3. **ACK:** Client acknowledges the server's response.

After the handshake, application data can be exchanged. Connection closure and recovery have additional state transitions.

### How does TCP provide reliability?

- **Sequence numbers:** Identify byte positions in the stream.
- **Acknowledgements:** Confirm received data ranges.
- **Retransmission:** Missing data may be sent again.
- **Flow control:** Receiver-advertised windows help prevent overwhelming the receiver.
- **Congestion control:** The sender adapts to network congestion signals.
- **In-order delivery:** The application receives an ordered byte stream, even if packets arrive out of order.

### TCP limitations and trade-offs

- Connection setup and retransmission add delay.
- Packet loss can delay delivery of later bytes in the same stream.
- Head-of-line blocking can affect data within a TCP stream.
- NATs, firewalls and middleboxes may influence connection behaviour.
- TCP reliability does not mean the application operation is safe to retry. An application still needs idempotency and clear transaction semantics.

## 4. UDP: lightweight datagram transport

User Datagram Protocol (UDP) sends independent datagrams with minimal transport-layer features. It does not establish a TCP-style connection or guarantee delivery, ordering or duplicate protection.

### When is UDP useful?

UDP can be useful when:

- The application needs low-latency communication and can tolerate some loss.
- The application implements its own reliability or congestion behaviour.
- A protocol needs datagrams or multicast support.
- Real-time voice, video, games or discovery protocols have specific timing needs.

UDP is not automatically faster or better than TCP. A poorly designed UDP application can create congestion, waste bandwidth or behave unreliably. Applications using UDP over the public Internet still need responsible congestion control.

## 5. TCP versus UDP: avoid simplistic myths

| Question | TCP | UDP |
|---|---|---|
| Connection setup | Connection-oriented | No TCP-style connection setup |
| Delivery guarantee | Reliable ordered stream semantics | Best-effort datagrams |
| Message boundaries | Stream; application must frame messages | Datagram boundaries preserved |
| Built-in flow/congestion control | Yes | No general TCP-equivalent service; application/protocol design matters |
| Common uses | Web connections, database connections, file transfer | DNS, real-time media, games, QUIC transport |

The correct protocol depends on the application and the protocol built on top of it. QUIC, for example, uses UDP as a base while implementing reliability and security features above it.

## 6. QUIC and HTTP/3

QUIC is a modern transport protocol commonly implemented over UDP. It integrates TLS 1.3 security and provides streams, loss recovery, congestion control and connection migration features. HTTP/3 maps HTTP semantics onto QUIC.

Potential advantages include:

- Faster connection establishment in suitable conditions.
- Independent streams that can reduce some forms of head-of-line blocking compared with multiple HTTP streams sharing one TCP connection.
- Connection migration when a client changes networks, such as moving between Wi-Fi and cellular, subject to implementation and network conditions.
- Integrated cryptographic protection.

QUIC does not eliminate all network delay or packet loss. Performance depends on the application, implementation, device, network and server.

## 7. What is HTTP?

Hypertext Transfer Protocol (HTTP) is a request-response protocol used by the Web and many APIs. A client sends a request to a server; the server returns a response.

### Simplified request example

```http
GET /articles/42 HTTP/1.1
Host: example.com
Accept: application/json
Authorization: Bearer <access-token>
```

A real application must protect credentials and tokens, use TLS, apply authorisation and avoid exposing secrets in logs or URLs.

### HTTP methods

| Method | Common purpose | Important consideration |
|---|---|---|
| GET | Retrieve a representation | Should not perform a state-changing action |
| HEAD | Retrieve headers without the response body | Useful for metadata checks |
| POST | Submit data or request processing | Not generally idempotent by default |
| PUT | Create/replace a resource representation | Designed to be idempotent when implemented correctly |
| PATCH | Partially modify a resource | Semantics depend on the patch format/API contract |
| DELETE | Request removal of a resource | Often designed to be idempotent, but outcome and retention rules matter |
| OPTIONS | Discover communication options | Used in CORS preflight and other contexts |

### HTTP status codes

- **2xx:** Request succeeded, for example `200 OK`, `201 Created`, `204 No Content`.
- **3xx:** Redirection, for example `301`, `302`, `304`.
- **4xx:** Client/request issue, for example `400`, `401`, `403`, `404`, `409`, `429`.
- **5xx:** Server or upstream failure, for example `500`, `502`, `503`, `504`.

`401` usually means valid authentication is missing or required; `403` generally means the server refuses the request. Exact API semantics should be documented.

## 8. HTTP caching

Caching stores a reusable response so that future requests can be served faster or with less origin work. HTTP caching uses headers such as:

- `Cache-Control`
- `ETag`
- `Last-Modified`
- `Expires`
- `Vary`

Example:

```http
Cache-Control: public, max-age=3600
ETag: "version-123"
```

Public static assets may be cached for long periods when versioned filenames are used. Private user data needs careful caching rules. A response that contains personal or account-specific data should not accidentally be stored in a shared cache. `Cache-Control: no-store` may be appropriate for especially sensitive responses, depending on the threat model and requirements.

Caching creates a correctness trade-off: stale data may be served until expiry or invalidation. Teams must design cache keys, permissions, invalidation and versioning deliberately.

## 9. HTTPS and TLS

HTTPS is HTTP carried through a protected TLS connection. TLS provides confidentiality, integrity and server authentication when certificate validation and configuration are correct. Client certificates can also support client authentication in some systems.

### What is a TLS certificate?

A TLS certificate binds a public key to a domain or identity under a certificate authority's validation process. A client checks the certificate chain, validity, name and trust rules. A valid certificate does not prove that the website is honest or free of vulnerabilities; it helps authenticate the endpoint and protect the connection.

### TLS handshake: conceptual flow

A simplified TLS 1.3 handshake includes:

1. Client sends supported versions, cipher suites and key-share information.
2. Server selects parameters and sends its key-share and certificate-related messages.
3. Client validates the server certificate and identity.
4. Both parties derive session keys.
5. Protected application data can be exchanged.

The actual handshake contains details such as extensions, transcript hashes, certificate validation and encrypted handshake messages. Do not treat this simplified list as an implementation specification.

### TLS implementation checks

- Use supported protocol versions and secure configurations.
- Validate certificates and hostnames; do not disable validation to “fix” errors.
- Protect private keys and renew certificates before expiry.
- Use secure cookie attributes for browser sessions.
- Avoid mixed content and insecure redirects.
- Do not place passwords or tokens in query strings.
- Monitor certificate and TLS configuration changes.

## 10. WebSocket, Server-Sent Events and WebRTC

### WebSocket

WebSocket starts with an HTTP-based handshake and then provides a persistent, bidirectional communication channel. It is useful for chat, live dashboards, collaborative editing and real-time events.

Important engineering concerns include authentication, connection limits, heartbeat/ping handling, message size, rate limits, backpressure, reconnect behaviour and horizontal scaling.

### Server-Sent Events (SSE)

SSE provides a server-to-client event stream over HTTP. It is useful when the server needs to push updates to the browser, but the client does not need the same persistent bidirectional channel. The browser's EventSource API supports reconnection behaviour, subject to implementation and server details.

### WebRTC

Web Real-Time Communication (WebRTC) supports real-time audio, video and data channels between browsers or compatible devices. It commonly uses ICE, STUN and TURN concepts to establish connectivity across NATs and firewalls.

WebRTC does not guarantee that every network path will allow direct peer-to-peer connectivity. TURN relay servers may be needed. Signalling is required for peers to exchange connection information, but WebRTC itself does not define one mandatory signalling system.

## 11. Other protocols you should recognise

| Protocol | Purpose or common use |
|---|---|
| DNS | Name and service resolution |
| SMTP | Email transfer/submission in relevant configurations |
| IMAP | Accessing and synchronising email mailboxes |
| SSH | Secure remote shell and tunnelling |
| SFTP | File transfer over SSH |
| NTP | Network time synchronisation |
| SNMP | Network-device monitoring/management in suitable deployments |
| MQTT | Lightweight publish/subscribe messaging, often for IoT |
| AMQP | Message-messaging protocol family |
| RTP/SRTP | Real-time media transport and protection |
| SIP | Session signalling in communication systems |
| ICMP | Network-layer control and diagnostic messages |

Protocol names do not imply that a service is secure by default. Secure configuration, authentication and network policy are still required.

## 12. Real application examples

### E-commerce checkout

A browser uses HTTPS to call APIs. The backend authenticates the user, checks inventory and price, creates an order and communicates with a payment provider. Payment webhooks may arrive asynchronously. Idempotency keys and signature validation help prevent duplicate or forged processing.

### Online game

A game may use reliable transport for account and inventory operations, and latency-sensitive transport for gameplay updates. Server authority, anti-cheat design, congestion behaviour and regional placement affect user experience.

### Video streaming

The application may use HTTPS APIs for account and catalogue data, HLS or DASH manifests and media segments for playback, and CDN delivery for scale. Adaptive bitrate logic selects a suitable stream based on available bandwidth and device capability.

### AI application

A browser or mobile client sends a request over HTTPS to an API. The backend authenticates and authorises it, applies rate and cost controls, sends work to a model service and streams or returns the response. Sensitive prompts and outputs require data-retention and logging controls.

## 13. Safe practical labs

### Lab A — Inspect HTTP headers

Use a public documentation site or a server you control:

```bash
curl -I https://example.com
```

Review status, caching and security headers. Do not use this command to scan random targets.

### Lab B — Inspect an HTTPS certificate

```bash
openssl s_client -connect example.com:443 -servername example.com
```

This establishes a TLS connection and displays certificate/handshake information. Replace the hostname with a service you are authorised to test.

### Lab C — Browser developer tools

1. Open your own website or a public documentation page.
2. Open Developer Tools -> Network.
3. Reload the page.
4. Inspect request method, status, response headers and timing.
5. Do not copy or publish authentication cookies, private tokens or personal data.

### Lab D — Basic API request

```bash
curl -i https://api.github.com
```

This is an example of inspecting a public API response. Respect provider usage policies and rate limits.

### Lab E — Capture packets safely

Use Wireshark only on your own lab network or with explicit permission. Start with DNS queries to a test domain and basic TCP handshakes. Avoid capturing other people's traffic. Captures may expose credentials or personal data if traffic is not encrypted.

## 14. Self-check

1. Why are IP addresses and ports both useful?
2. What does TCP guarantee that UDP does not?
3. Why is UDP not automatically faster or better?
4. What does QUIC provide above UDP?
5. What is the difference between an HTTP method and a status code?
6. Why must private responses use careful cache policies?
7. What does TLS certificate validation prove—and what does it not prove?
8. When is WebSocket more suitable than SSE?
9. Why might WebRTC require a TURN server?
10. Why is application-level idempotency important even when TCP is reliable?

## References

1. [RFC 9293 — Transmission Control Protocol](https://www.rfc-editor.org/rfc/rfc9293)
2. [RFC 768 — User Datagram Protocol](https://www.rfc-editor.org/rfc/rfc768)
3. [RFC 9000 — QUIC: A UDP-Based Multiplexed and Secure Transport](https://www.rfc-editor.org/rfc/rfc9000)
4. [RFC 9110 — HTTP Semantics](https://www.rfc-editor.org/rfc/rfc9110)
5. [RFC 9112 — HTTP/1.1](https://www.rfc-editor.org/rfc/rfc9112)
6. [RFC 9113 — HTTP/2](https://www.rfc-editor.org/rfc/rfc9113)
7. [RFC 9114 — HTTP/3](https://www.rfc-editor.org/rfc/rfc9114)
8. [RFC 9846 — TLS 1.3](https://www.rfc-editor.org/rfc/rfc9846)
9. [MDN — HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP)
10. [MDN — WebSocket API](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API)
11. [MDN — Server-sent events](https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events)
12. [W3C — WebRTC](https://www.w3.org/TR/webrtc/)

**Study rule:** You understand this chapter when you can explain how a browser request uses DNS, IP, a transport protocol, TLS and HTTP—and can inspect a request safely using developer tools.
