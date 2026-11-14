# 05C — TCP, UDP, QUIC, HTTP, TLS and Application Protocols

**Part:** 05 — Networking and Internet Protocols  
**Language:** Detailed Hinglish  
**Research snapshot:** 13 November 2026

---

## 1. Is chapter ka goal

Yahan hum browser se server tak request ko protocol-level par samjhenge. Topics:

- Ports, sockets and transport layer.
- TCP connection, handshake, reliable delivery, retransmission and congestion control.
- UDP datagrams and application-managed reliability.
- QUIC and HTTP/3.
- HTTP request/response, methods, status codes, headers and caching.
- HTTPS, TLS handshake, certificates and certificate authorities.
- WebSockets, Server-Sent Events and WebRTC.
- APIs, email, SSH and other common protocols.

## 2. IP address mil gaya — ab kis application ko data dena hai?

IP address destination machine/network identify karta hai. Lekin ek machine par web server, database, SSH service, mail service and other processes simultaneously run ho sakte hain.

Transport layer **port numbers** ke through process/service endpoint distinguish karne mein help karti hai.

Common port examples:

| Port | Common service | Note |
|---:|---|---|
| 22 | SSH | Secure remote administration |
| 25 | SMTP | Mail transfer between servers; submission often uses other ports |
| 53 | DNS | DNS commonly UDP/TCP; encrypted DNS has other transports/ports |
| 80 | HTTP | Conventional cleartext HTTP |
| 123 | NTP | Time synchronisation |
| 143 | IMAP | Mail access; secure variants/configs differ |
| 443 | HTTPS | HTTP over TLS; HTTP/3 uses QUIC over UDP, usually port 443 |
| 587 | SMTP submission | Mail client submission with appropriate security |

Port 443 dekhkar assume mat karo ki every 443 traffic HTTP/2/TCP hai. HTTP/3 generally QUIC over UDP use karta hai; same numeric port different transport protocols par exist kar sakta hai.

**Socket** OS programming interface/endpoint abstraction hai. Network connection ko commonly source IP, source port, destination IP, destination port and transport protocol se identify kiya ja sakta hai (implementation and NAT context matter).

## 3. TCP: reliable ordered byte stream

TCP (Transmission Control Protocol) application ko reliable, ordered byte stream provide karta hai. It is connection-oriented.

Applications TCP ko tab use karte hain jab ordered reliable delivery useful ho, e.g. many database connections, SSH, many web connections and email transfer.

### TCP three-way handshake (simplified)

1. Client → Server: SYN
2. Server → Client: SYN-ACK
3. Client → Server: ACK

Is process mein sequence numbers and connection state establish hote hain. Iske baad application data exchange kar sakti hai.

```text
Client                               Server
  | -------- SYN --------------------> |
  | <------- SYN + ACK --------------- |
  | -------- ACK --------------------> |
  |                                    |
  | ===== application data =========> |
```

### TCP reliability kaise deta hai?

- Sequence numbers bytes ko order karne mein help karte hain.
- Acknowledgments receiver ke received data ka indication dete hain.
- Lost data detect ho toh retransmission ho sakti hai.
- Receive window flow control receiver ko overwhelm hone se protect karti hai.
- Congestion control sender ko network congestion ke according transmission adjust karne mein help karta hai.

**Reliable ka matlab unlimited guarantee nahi:** Connection fail ho sakta hai, endpoint crash ho sakta hai, network outage ho sakta hai. TCP data stream ko connection ke within reliable delivery semantics deta hai, business transaction successful hui ya database commit hua—ye application-level concern hai.

### TCP ke limitations/trade-offs

- Connection setup latency.
- Head-of-line blocking within a TCP byte stream: missing earlier bytes later bytes ko application tak deliver hone se rok sakte hain.
- Network path change/mobile handoff handle karne mein traditional TCP connection ko challenge ho sakta hai.
- Per-connection state server resources use karta hai.

Modern TCP stacks congestion control and performance mechanisms implement karte hain; exact behaviour OS/network configuration par depend karta hai.

Primary current consolidated TCP specification: [RFC 9293 (2022)](https://www.rfc-editor.org/rfc/rfc9293). [1]

## 4. UDP: lightweight datagram transport

UDP (User Datagram Protocol) message/datagram boundaries preserve karta hai aur TCP-style connection setup, ordered reliable byte stream or built-in retransmission provide nahi karta.

UDP delivery, order and duplicate protection guarantee nahi karta. Application ko agar reliability chahiye toh woh own protocol logic implement kar sakti hai.

Use cases:

- DNS queries (common traditional mode).
- Real-time voice/video and some game traffic.
- QUIC transport (HTTP/3).
- Telemetry and some discovery protocols.

### UDP kab useful hai?

Suppose multiplayer game har 30 ms player position update bhej raha hai. Agar old position packet late ho gaya, toh use retransmit karna always useful nahi. Fresh position packet zyada important ho sakta hai. Application sequence/timestamps and prediction/interpolation handle karti hai.

But banking transaction ke final record ke liye unreliable delivery semantics directly suitable nahi. Financial application reliable application-level protocol, transaction IDs, idempotency, persistence and reconciliation use karegi.

UDP specification: [RFC 768](https://www.rfc-editor.org/rfc/rfc768). [2]

## 5. TCP vs UDP — simplistic myth avoid karo

| Aspect | TCP | UDP |
|---|---|---|
| Connection | Connection-oriented | Connectionless datagrams |
| Ordering | Ordered byte stream | No built-in ordering |
| Retransmission | Built-in transport reliability | Application may implement |
| Flow control | Yes | No TCP-style built-in flow control |
| Congestion control | TCP implementations provide it | Application/protocol must behave responsibly; QUIC does congestion control |
| Message boundaries | Byte stream, app frames define messages | Datagram boundaries preserved |
| Common examples | SSH, traditional HTTPS over TCP, database connections | DNS, realtime media, QUIC carrier |

TCP “slow” aur UDP “fast” bolna accurate comparison nahi. Performance workload, network, congestion control, protocol design and implementation par depend karta hai.

## 6. QUIC and HTTP/3

QUIC ek modern secure transport protocol hai jo UDP datagrams ke upar operate karta hai. It provides multiple streams, flow control, low-latency connection establishment and path migration features. QUIC integrates TLS-based cryptographic handshake and packet protection.

Why QUIC was developed/useful:

- TCP head-of-line blocking ke effect ko independent streams ke design se reduce karna.
- Transport and cryptographic handshake coordination.
- Connection migration, useful when client network path changes (e.g. Wi-Fi to cellular), subject to implementation and network conditions.
- More transport evolution in user-space implementations without depending entirely on OS TCP stack updates.

**Important:** QUIC is not “UDP with no reliability.” QUIC implements reliability, loss recovery, congestion control and secure connection semantics itself. UDP is the carrier.

HTTP/3 maps HTTP semantics onto QUIC. HTTP/2 commonly runs over TCP with TLS; HTTP/1.1 also commonly runs over TCP, though protocol deployment details vary.

Standards reference: [RFC 9000 — QUIC](https://www.rfc-editor.org/rfc/rfc9000). [3]

## 7. HTTP kya hai?

HTTP = Hypertext Transfer Protocol. It is an application-layer request/response protocol. Browser, mobile app or service client request bhejta hai; server response deta hai.

HTTP is stateless in its core semantics: each request is understood independently at protocol level. Applications cookies, tokens, sessions and server-side state use karke stateful user experience build kar sakti hain.

### Example request (simplified)

```http
GET /posts/123 HTTP/1.1
Host: api.example.com
Accept: application/json
Authorization: Bearer <access-token>
```

Example response:

```http
HTTP/1.1 200 OK
Content-Type: application/json
Cache-Control: private, max-age=0

{"id":"123","caption":"Hello world"}
```

Real requests can include many more headers, compression and different HTTP versions.

### HTTP methods

| Method | Common intent | Caution |
|---|---|---|
| GET | Read/retrieve representation | Should not request destructive action |
| POST | Submit/process/create resource | Often non-idempotent unless designed otherwise |
| PUT | Replace resource representation | Defined as idempotent in HTTP semantics |
| PATCH | Partial modification | Semantics depend on patch format/API contract |
| DELETE | Remove resource relationship/resource | Repeating should be designed predictably |
| HEAD | GET-like metadata without response content | Useful for metadata checks |
| OPTIONS | Communicate supported methods/capabilities | CORS preflight uses it in browsers |

**Idempotency:** Same request repeat karne par intended server effect same rahe. Payment APIs often idempotency keys use karte hain so a retry does not accidentally charge twice. HTTP method semantics help, but payment correctness is application-level.

### HTTP status codes

| Class/code | Meaning | Example |
|---|---|---|
| 1xx | Informational | Protocol progress |
| 2xx | Success | `200 OK`, `201 Created`, `204 No Content` |
| 3xx | Redirection | `301`, `302`, `304 Not Modified` |
| 4xx | Client/request issue | `400`, `401`, `403`, `404`, `429` |
| 5xx | Server-side failure | `500`, `502`, `503`, `504` |

Common misunderstandings:
- 401 means authentication credentials are missing/invalid or not accepted; 403 means server understood request but refuses access (implementation semantics may vary).
- 404 can hide a protected resource's existence in some API designs.
- 429 indicates rate limiting and may include `Retry-After`.
- 500 is not a debugging explanation; logs/traces needed.

Current HTTP core semantics: [RFC 9110](https://www.rfc-editor.org/rfc/rfc9110). HTTP/1.1 messaging, HTTP/2 and HTTP/3 have separate specifications that work with the shared semantics model. [4]

## 8. HTTP caching

Caching performance and cost improve kar sakti hai, but privacy and correctness carefully manage karna hota hai.

Common headers:
- `Cache-Control`
- `ETag`
- `Last-Modified`
- `If-None-Match`
- `Age`
- `Vary`

Example:
- Public logo, versioned CSS and public thumbnails long cache ho sakte hain.
- User profile API private or user-specific ho sakti hai; shared public cache unsafe ho sakta hai.
- `Cache-Control: no-store` sensitive response storage prevent karne ke liye use ho sakta hai, though exact policy security review se design karo.

CDN cache key, cookies, Authorization header and `Vary` handling galat hui toh one user's private content another user ko serve ho sakta hai. Cache configuration is a security boundary.

## 9. HTTPS and TLS

HTTPS = HTTP carried over a TLS-protected channel. TLS secure channel provide karta hai, with confidentiality, integrity and authentication properties depending on configuration and verification.

TLS aims to protect against:
- Eavesdropping (traffic read karna).
- Tampering (data modify karna).
- Message forgery (forged communication).

TLS does not automatically protect a compromised endpoint, malicious browser extension, insecure server database, weak authorization or phishing.

### TLS certificate kya hota hai?

A server certificate public-key identity binding represent karta hai. Certificate Authority (CA) certificate sign karti hai. Browser/OS trusted root store aur certificate chain validate karta hai. Client hostname match, validity period and trust chain checks karta hai. Certificate alone encryption nahi; TLS handshake key agreement and cryptographic algorithms use karta hai.

### TLS handshake: conceptual flow

1. Client supported TLS versions, cipher suites/extensions and key share information propose karta hai.
2. Server compatible parameters select karke certificate and key-exchange response deta hai (exact TLS 1.3 handshake sequence extensions/options ke hisaab se vary kar sakti hai).
3. Client certificate chain and hostname validate karta hai.
4. Both sides shared secrets derive karte hain using key agreement.
5. Finished messages verify handshake transcript/integrity.
6. Application traffic symmetric authenticated encryption se protect hota hai.

TLS 1.3 uses modern handshake design; 0-RTT early data has replay considerations and should not be used blindly for non-idempotent actions. TLS 1.3's updated specification as of this handbook snapshot is **RFC 9846 (July 2026)**, which obsoletes RFC 8446 while retaining TLS version 1.3. [5]

### TLS implementation checks

- Valid certificate and correct hostnames.
- Private keys securely managed, not committed into Git.
- Deprecated protocols/ciphers disabled according to compatibility needs and current guidance.
- Certificate renewal automated and monitored.
- TLS terminated only at trusted edge/proxy and any internal hops protected according to threat model.
- HSTS deployed after careful validation.
- Secrets and session tokens not logged.

## 10. WebSocket, Server-Sent Events and WebRTC

### WebSocket

WebSocket client-server connection establish karke two-way real-time messaging allow karta hai. Chat typing indicators, live collaboration and notifications ke liye useful.

Challenges:
- Many concurrent open connections.
- Heartbeats and idle timeout.
- Reconnect/backoff.
- Authentication refresh and permission checks.
- Multi-server pub/sub or broker coordination.
- Message ordering, duplicates and delivery receipts at application level.

WebSocket connection auth ka alternative nahi. Every message action must be authorized.

### Server-Sent Events (SSE)

SSE browser ko server-to-client event stream provide karta hai over HTTP. One-way updates—progress, feed update notice, dashboard status—ke liye simpler than bidirectional WebSocket in many cases. Client-to-server requests normal HTTP se jaate hain.

### WebRTC

WebRTC browsers/apps ke beech real-time audio/video/data communication enable karta hai. NAT traversal, ICE, STUN and TURN concepts use ho sakte hain. Signalling server peers ko connection setup details exchange karne mein help karta hai. Media may flow peer-to-peer or through relay/SFU depending on topology and product architecture.

WebRTC vs WebSocket:
- WebSocket: app messages over persistent connection.
- WebRTC: real-time media/data transport with NAT traversal and media-specific mechanisms.
- Video call app often both use karti hai: signalling via HTTPS/WebSocket, media via WebRTC.

## 11. Other protocols you should recognise

| Protocol | Purpose | Where you see it |
|---|---|---|
| SMTP | Email transfer/submission | Email infrastructure |
| IMAP | Mailbox access/synchronisation | Email clients |
| POP3 | Mail retrieval model | Legacy/simple mail clients |
| SSH | Encrypted remote shell/admin | Server administration |
| SFTP | File transfer over SSH | Deployments and file exchange |
| NTP | Time synchronisation | Servers, logs, certificates |
| MQTT | Lightweight publish/subscribe messaging | IoT, telemetry |
| AMQP | Message-oriented middleware protocol | Enterprise messaging |
| RTP/SRTP | Real-time media transport / secure RTP | Voice/video systems |
| SIP | Session initiation/signalling | Voice and communication systems |

## 12. Real application examples

### E-commerce checkout

- Browser calls HTTPS API.
- TLS protects transport.
- API authentication verifies user.
- Payment provider interaction may use separate secure API calls.
- Idempotency key prevents accidental duplicate payment operation.
- Server stores transaction state and emits background event.

### Online game

- Login/matchmaking may use HTTPS.
- Game state may use UDP-based protocol or QUIC/WebTransport in suitable designs.
- Server validates critical moves; client is not trusted as final authority.
- Latency, jitter and cheat prevention important.

### Video streaming

- DNS chooses CDN endpoint.
- HTTPS fetches manifest/media segments.
- Adaptive streaming chooses quality based on throughput/buffer/device conditions.
- CDN caches public/shared segments; entitlement checks protect paid/private content.

### AI application

- Client sends prompt/context via HTTPS.
- API authenticates and authorizes request.
- Service invokes model provider or internal model server.
- Streaming response may use SSE or another protocol.
- Sensitive prompt data, provider processing and logs need privacy controls.

## 13. Safe practical labs

### Lab A — HTTP headers inspect

```bash
curl -I https://example.com
```

Observe status code, server response headers, cache hints and redirects. Response headers may differ by region/time/provider.

### Lab B — HTTPS certificate inspect

```bash
openssl s_client -connect example.com:443 -servername example.com
```

This opens a TLS connection for inspection. Do not paste private keys or sensitive output publicly. Certificate chain/verification output varies by OS and trust store.

### Lab C — Browser developer tools

1. Open a site you are allowed to inspect.
2. Developer Tools → Network.
3. Reload page.
4. Inspect request URL, method, status, timing, response headers and transferred size.
5. Check whether HTTP/2 or HTTP/3 is reported by the browser.
6. Never copy/share cookies, bearer tokens, private query strings or personal data.

### Lab D — API request basics

```bash
curl -i https://httpbin.org/get
```

Use only public test endpoints and non-sensitive data. Compare GET vs POST in a test environment.

### Lab E — Packet capture safely

Wireshark can capture traffic on your own device/network. Capture only traffic you own or have explicit permission to analyse. Encrypted HTTPS payloads should not be expected to appear as readable page content. Metadata may still be visible, depending on protocol and encryption features.

## 14. Self-check

1. IP address aur port number different information kyun represent karte hain?
2. TCP three-way handshake mein SYN/SYN-ACK/ACK ka purpose kya hai?
3. TCP reliable byte stream deta hai—application messages ko framing kyun chahiye?
4. UDP har use case mein TCP se faster kyun nahi hota?
5. QUIC UDP use karke bhi reliable and secure kaise ho sakta hai?
6. HTTP stateless hone ka meaning kya hai?
7. PUT and POST semantics mein difference kya hai?
8. 401, 403, 404, 429 and 503 ko troubleshoot kaise karoge?
9. HTTPS kaunsa problem solve karta hai, aur kaunse problems nahi?
10. Certificate Authority par browser trust kaise establish karta hai?
11. WebSocket, SSE and WebRTC use cases alag kaise hain?
12. Why is 0-RTT replay safety important?

## References

1. [RFC 9293 — Transmission Control Protocol](https://www.rfc-editor.org/rfc/rfc9293)
2. [RFC 768 — User Datagram Protocol](https://www.rfc-editor.org/rfc/rfc768)
3. [RFC 9000 — QUIC](https://www.rfc-editor.org/rfc/rfc9000)
4. [RFC 9110 — HTTP Semantics](https://www.rfc-editor.org/rfc/rfc9110)
5. [RFC 9846 — TLS 1.3 (July 2026)](https://www.rfc-editor.org/rfc/rfc9846)
6. [RFC 8446 — Previous TLS 1.3 specification (obsoleted by RFC 9846)](https://www.rfc-editor.org/rfc/rfc8446)
7. [RFC 9525 — Service Identity in TLS](https://www.rfc-editor.org/rfc/rfc9525)
8. [MDN — HTTP Overview](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview)
9. [MDN — WebSocket API](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API)
10. [WebRTC — Getting Started](https://webrtc.org/getting-started/overview)

---

**Next:** 05D — Network Security, Troubleshooting, Architecture Labs and Real-World Failure Cases.
