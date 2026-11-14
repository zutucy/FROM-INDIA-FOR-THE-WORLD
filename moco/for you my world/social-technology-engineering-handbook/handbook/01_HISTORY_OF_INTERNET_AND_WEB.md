# Part 01 — History of the Internet and the World Wide Web

**Research snapshot:** 13 November 2026  
**Purpose:** Understand where the network technologies behind modern digital products came from, which problems they were designed to solve, and how an application built in one country can reach users around the world.

---

## 1. First, distinguish the Internet from the Web

People often use the words *Internet* and *website* as if they mean the same thing. Technically, they are different.

- **The Internet** is a global system of interconnected networks. It relies on fibre-optic cables, routers, mobile networks, Internet service providers (ISPs), data centres, IP addressing and routing protocols.
- **The World Wide Web (WWW or Web)** is one family of services that runs over the Internet. Websites and web applications exchange information through browsers, commonly using HTTP or HTTPS.
- **Email** is another Internet application family. It does not require a web page to operate.
- **VoIP and video calling** use Internet connectivity to carry voice and video.
- **Online games** use Internet networks for real-time communication between players and game services.

A useful analogy is to think of the Internet as a system of roads, interchanges and transport infrastructure. The Web is one type of service that uses those roads. Email, video calls and online games use the same underlying network, but they are not themselves web pages.

This distinction matters for social products. Instagram's website uses Web protocols through a browser. Its mobile application also uses the Internet, but its interface does not have to be a browser page. In both cases, requests travel to remote services.

## 2. Before the Internet: what problem needed solving?

Before the 1960s, computers were large, expensive and often isolated within individual institutions. One organisation's computer could not easily communicate with another organisation's computer. Researchers wanted better ways to share remote computing resources, exchange research and communicate reliably.

Traditional telephone networks commonly used **circuit switching**. During a call, the network reserved a dedicated path or circuit. This worked well for continuous voice communication, but reserving a dedicated circuit for computer data could waste capacity. Computer traffic is often *bursty*: a device sends data for a short time, pauses, and then sends more.

### The idea of packet switching

Packet switching divides a message into smaller units called **packets**. Each packet carries addressing and control information. Network devices forward packets towards their destination. The receiving system can reconstruct the original data; higher-level protocols handle issues such as missing, damaged or out-of-order data when required.

| Circuit switching | Packet switching |
|---|---|
| A dedicated circuit or path may be reserved for a session. | Network links can be shared by packets belonging to different users. |
| Useful for traditional continuous voice-call models. | Well suited to bursty computer communication. |
| Path reservation is central. | Routing and packet forwarding are central. |
| Reserved capacity may remain idle. | Statistical sharing can use link capacity more efficiently. |

Packet switching was not the work of one inventor. Paul Baran in the United States explored resilient distributed communication. Donald Davies and his team at the UK's National Physical Laboratory developed packet-switching concepts and the term *packet*. Leonard Kleinrock contributed important queueing and network-performance theory. ARPA researchers helped turn related ideas into a practical network programme. These were parallel research efforts, not a single-person invention story.

**Why it mattered:** Packet switching made it practical to connect different computers and networks through shared communication infrastructure.

## 3. ARPANET: an important early foundation

The United States Advanced Research Projects Agency (ARPA, later renamed DARPA) supported the ARPANET project to connect research computers at different institutions. BBN (Bolt Beranek and Newman) built Interface Message Processors (IMPs), early packet-switching devices that can be viewed as ancestors of some modern router functions.

### Early timeline

- **1968:** ARPA awarded BBN a contract to build early packet-switching network equipment.
- **September 1969:** The first ARPANET node became active at UCLA.
- **October 1969:** An early host-to-host message attempt took place between UCLA and Stanford Research Institute (SRI). A well-known historical account says the intended word was “LOGIN”, but the system failed after “LO”. Treat this as an anecdotal milestone, not as the single birth moment of the Internet.
- **December 1969:** The network had four initial nodes: UCLA, SRI, the University of California, Santa Barbara (UCSB), and the University of Utah.

ARPANET was not originally built to create Instagram or public social networking. Its purpose was to connect research computing resources and test network communication.

### What did ARPANET demonstrate?

1. Computers at different locations could communicate over a network.
2. Packet-switched infrastructure could work in practice.
3. Useful applications could be developed on top of a network.
4. Shared protocol standards were essential. Without them, different networks could not reliably understand one another.

## 4. Email: an early “killer application”

Once network technology existed, engineers needed useful applications for it. In 1971, Ray Tomlinson implemented network email on ARPANET. He combined local machine messaging with file-transfer capabilities to send a message to a user on another computer.

One lasting design choice was the `@` sign. In an address such as `user@host`, it separates the user from the machine or host. Email helped turn networking from a research experiment into a useful communication environment.

A historical nuance matters: forms of electronic messaging and computer mail already existed on time-sharing systems before ARPANET email. Tomlinson's major contribution was making networked email work between different computers and establishing the familiar address notation.

**Product lesson:** Infrastructure becomes valuable to users when it helps them complete a practical task.

## 5. TCP/IP: connecting separate networks into an Internet

Early ARPANET systems used a host protocol called NCP. A larger challenge emerged: future networks might use different technologies and be operated by different organisations. A common protocol family was needed to connect them.

Work by Vint Cerf and Robert “Bob” Kahn led to the design of the Transmission Control Protocol (TCP) and Internet Protocol (IP). TCP/IP provided a common foundation for a network of networks.

- **IP (Internet Protocol):** Provides addressing and basic packet forwarding between networks.
- **TCP (Transmission Control Protocol):** Provides a reliable, ordered byte stream using mechanisms such as sequencing, acknowledgements, retransmission and flow control.
- **UDP (User Datagram Protocol):** Provides connectionless datagrams. Some real-time applications prefer to implement selected reliability controls at the application layer instead.

On **1 January 1983**, ARPANET made its major transition from NCP to TCP/IP. This “flag day” is an important milestone in Internet history. It also teaches a practical lesson: protocol changes require compatibility planning across connected systems.

### Why TCP/IP matters to social platforms

When a user uploads a post from a phone, the request travels through a network to a backend service. IP provides the basic addressing and routing. TCP or another transport protocol carries the application communication. HTTPS protects HTTP communication with TLS.

A social application developer usually does not implement IP routing. However, developers should understand latency, packet loss, timeouts, TLS, connection reuse and retry behaviour because these affect the reliability of the application.

## 6. DNS: resolving human-friendly names into network destinations

Computers need network addresses, but people find names such as `example.com` easier to remember. The **Domain Name System (DNS)** maps domain names to IP addresses and other service information through records.

A simplified lookup works like this:

1. A user enters `example.com` in a browser.
2. The browser or device checks its DNS cache.
3. If no usable answer is cached, a resolver queries DNS infrastructure.
4. DNS records return an appropriate IP address or service target.
5. The client establishes a network connection to the destination.

DNS is not merely a “website-to-IP” directory. Different record types support email routing, service discovery, domain verification and other tasks. Caching improves performance, but stale records and propagation timing can affect deployment planning.

## 7. The Internet expands from research networks to a global network

During the 1980s and 1990s, academic, government, research and commercial networks expanded. Backbone initiatives such as NSFNET supported wider research connectivity. Universities, organisations and commercial providers built additional connections.

The Internet does not run on one company's server. It is a system of interconnected autonomous networks, including ISPs, transit providers, content networks and research networks.

### Three important terms

- **ISP (Internet Service Provider):** A company or organisation that provides Internet connectivity to users or other networks.
- **ASN (Autonomous System Number):** A number identifying a network that operates under a defined routing policy.
- **BGP (Border Gateway Protocol):** A routing protocol used to exchange reachability information between autonomous systems.

The global nature of the Internet comes from interconnection, common protocols and routing arrangements—not from a single central computer.

## 8. The World Wide Web: the breakthrough of 1989–1993

Tim Berners-Lee proposed the World Wide Web at CERN in 1989. He developed the core ideas and early implementation of a system that connected documents through hypertext links. The first website and server appeared around 1990. CERN made the Web software available freely in 1993, helping its adoption spread.

The early Web used three important building blocks:

- **HTML (HyperText Markup Language):** Describes the structure of a web document.
- **HTTP (HyperText Transfer Protocol):** Defines how a client and server request and exchange Web resources.
- **URL (Uniform Resource Locator):** Identifies where a resource can be found.

A browser could request a document from a server, display it and let the user follow links to other documents. This made information easier to publish, discover and connect.

### What problem did the Web solve?

Before the Web, information systems often used separate formats and tools. The Web provided a simple, link-based publishing and navigation model that could work across different computers and operating systems.

### Internet versus Web: a practical example

A phone connects to the Internet through Wi-Fi or a mobile network. The user opens a website. DNS helps locate the destination, IP routing carries packets, TLS protects the connection and HTTP requests the page. The Internet carries the traffic; the Web provides the document and application model.

## 9. The browser and search era

Early browsers made the Web more accessible to people who were not network specialists. Mosaic, released in 1993, helped popularise graphical Web browsing. Netscape Navigator and Internet Explorer contributed to the browser market's growth. Later, Firefox, Safari, Chrome and other browsers developed different security, rendering and performance approaches.

As the number of websites grew, finding information became harder. Web directories and search engines evolved. Search systems moved from relatively simple indexing and link analysis towards large-scale crawling, ranking, spam detection, semantic systems and machine-learning-assisted relevance.

**Important distinction:** A search engine is not the Internet and is not the Web itself. It is a service that discovers, indexes and ranks content accessible through supported methods.

## 10. From static pages to dynamic web applications

Early websites often served mostly static documents. Over time, browsers gained more scripting, styling and application capabilities. Servers began generating pages from databases and user state. This enabled accounts, shopping carts, dashboards, feeds, comments and personalised experiences.

A modern web application commonly includes:

- A browser interface built with HTML, CSS and JavaScript.
- A backend service that enforces business logic and permissions.
- A database that stores structured records.
- Object storage for large files such as images and videos.
- Caching, queues and background workers for performance and reliability.

### A simplified modern Web request flow

```text
User
  -> Browser
  -> DNS resolution
  -> Network connection and TLS
  -> CDN / edge layer (where applicable)
  -> Load balancer or application entry point
  -> Backend API
  -> Authentication and authorization
  -> Database / cache / other services
  -> Response returned to browser
```

A page may require many separate requests for HTML, JavaScript, CSS, images, fonts and API data. Browser developer tools help inspect these requests, response codes, timing and failures.

## 11. Web 2.0 and user-generated content

The term **Web 2.0** became popular in the mid-2000s. It describes a shift in which users increasingly created, commented on, rated, uploaded and shared content rather than only consuming publisher-created pages.

Examples include blogs, wikis, photo-sharing websites, video-sharing services, social networks and collaborative tools.

This shift changed system requirements. Platforms had to handle:

- User accounts and identity.
- Content upload and storage.
- Comments, likes, sharing and relationships.
- Search and discovery.
- Moderation and abuse reports.
- Privacy controls and permissions.
- Notifications and activity feeds.
- Large and unpredictable traffic patterns.

User-generated content also created risks: spam, harassment, impersonation, copyright complaints, malicious uploads and exposure of personal information. A platform therefore needs trust and safety systems as well as storage and APIs.

## 12. Smartphones, apps and the mobile-first era

Smartphones combined cameras, GPS, sensors, touch screens and mobile Internet access in a device people carried throughout the day. App stores made it easier to discover and install software. Social products could capture and publish photos or video immediately instead of requiring a desktop workflow.

Mobile-first design introduced new constraints:

- Smaller screens and touch-based input.
- Battery and memory limits.
- Different camera and media capabilities.
- Variable mobile network quality.
- Data-plan costs and limited storage.
- Permissions for camera, microphone, location and notifications.
- App-store review and release processes.

A modern product must account for low-end devices, intermittent connectivity, language diversity, accessibility and different data-plan conditions across regions.

## 13. Cloud computing, object storage and CDNs

A startup does not need to build its own physical data centre. Cloud providers offer compute, databases, networking, storage, queues and managed services that can be rented or consumed on demand.

| Infrastructure layer | Example role | Typical application use |
|---|---|---|
| Compute | Virtual machines, containers, serverless functions | APIs and background workers |
| Relational database | Managed PostgreSQL | Users, posts, comments and follows |
| Cache | Redis or another cache | Frequently accessed data, selected session and rate-limit designs |
| Object storage | S3-compatible bucket | Large photo, video and audio files |
| CDN | Distributed edge delivery | Serving media and static assets closer to users |
| Queue | Managed or self-hosted message broker | Processing slow work asynchronously |
| Observability | Logs, metrics and traces | Diagnosing failures and latency |

### Why did CDNs emerge?

If a user is in India and the origin server is in the United States, sending every large image or video directly from that origin can increase latency and network cost. A content delivery network can cache eligible copies at edge locations. A user may receive content from a suitable nearby edge, although the closest location is not always selected: routing, capacity, cache availability and provider policy matter.

A CDN does not automatically make private content safe. Private media may require signed URLs or cookies, short expiry periods, correct cache policies, authorization and cache invalidation procedures.

### The shift to modern video streaming

User-generated video may be encoded into multiple resolutions and bitrates. Segmented delivery formats such as HLS or MPEG-DASH can support adaptive playback. The player chooses an available quality based on network conditions and device capability.

## 14. Global platforms: how can a service built in one country operate elsewhere?

Imagine a company incorporated in the United States, running application servers in a European cloud region, storing some media in Asia and serving users in India, Brazil, Japan and Germany.

Map five different questions separately:

1. **Network map:** User ISP -> transit or peering -> CDN/edge -> application region.
2. **Compute map:** Which cloud regions and availability zones run the APIs and workers?
3. **Data map:** Where are account databases, logs, backups, media and analytics stored or processed?
4. **Vendor map:** Which countries are involved in email, OTP, analytics, payments, crash reports, moderation and support vendors?
5. **Legal map:** How do company establishment, user location, service category, data type, transfers and local law affect the product?

### Data residency, localisation and cross-border transfer

- **Data residency:** The geographic location where data is stored.
- **Data localisation:** A law or regulation may require specific data to be stored or processed within a country.
- **Cross-border data transfer:** Personal data or other regulated information moves from one jurisdiction to another.
- **Remote access:** A support engineer or vendor in another country may access data even when the storage location does not change. This can still require privacy and legal analysis.

Countries do not all use the same rules. Some laws permit transfers when specified mechanisms, adequacy decisions or safeguards exist. Some sectors or data categories may have local storage or processing duties. Others impose separate requirements on particular services. The exact position must be mapped against current official sources for each relevant market.

### Example: a user in India and a company in the United States

A user in India creates an account on a foreign social application. At a high level:

1. The application uses DNS and network routing to reach a suitable entry point.
2. The login request travels over a TLS-protected connection to an API.
3. The backend checks identity and session state.
4. A database query reads the user record.
5. A feed service collects and ranks eligible posts.
6. Images and videos arrive through a CDN or object-storage delivery path.
7. Events may enter analytics and monitoring pipelines, subject to product settings and data-handling rules.

This example does **not** prove that data is automatically stored in the United States or that transfers outside India are always permitted. Actual storage locations, vendors, legal duties and transfer mechanisms depend on the platform's architecture and applicable law.

## 15. What should engineers learn from this history?

| Historical development | Engineering lesson |
|---|---|
| Packet switching | Share infrastructure efficiently. |
| TCP/IP | Use common standards for interoperability. |
| DNS | Human-friendly names depend on distributed infrastructure. |
| WWW, HTML and HTTP | Shared interfaces and linking can support broad adoption. |
| Email | Technology becomes valuable when it solves a clear user problem. |
| Dynamic web applications | Identity, state, databases and permissions become central. |
| Mobile applications | Device constraints and network quality shape user experience. |
| Cloud and CDN | Global products need distributed compute and content delivery. |
| Video streaming | Upload, processing, encoding and delivery are separate stages. |

## 16. Basic glossary

- **ARPANET:** Early packet-switched research network and a major foundation in Internet history.
- **Packet:** A formatted unit of data transmitted across a network.
- **Router:** A device that forwards packets towards another network or destination.
- **Protocol:** Agreed rules for communication between systems.
- **TCP:** Reliable, ordered byte-stream transport protocol.
- **IP:** Core protocol for packet addressing and routing.
- **DNS:** Distributed naming system for resolving domain names and service records.
- **HTTP:** Web client/server request-response protocol.
- **HTTPS:** HTTP communication protected by TLS.
- **HTML:** Markup language used to structure Web documents.
- **URL:** Uniform Resource Locator; identifies where a resource can be found.
- **ISP:** Internet Service Provider.
- **BGP:** Protocol for exchanging routing information between autonomous networks.
- **CDN:** Distributed content delivery and caching network.
- **Object storage:** A storage model/service for large unstructured objects such as photos and videos.
- **Latency:** Delay in a request or response.
- **Throughput:** Amount of data transferred or processed in a period.
- **Availability:** The degree to which a system is usable or reachable.
- **Data residency:** Geographic location where data is stored.

## 17. Self-check questions

1. What is the exact difference between the Internet and the World Wide Web?
2. Why was packet switching useful for bursty computer traffic?
3. What was ARPANET originally designed to do?
4. Explain the responsibilities of TCP and IP in simple terms.
5. Why is DNS needed when IP addresses already exist?
6. What problem did Tim Berners-Lee's Web address?
7. How did user-generated content change server and database requirements?
8. Why is a CDN alone not enough to secure private user media?
9. Why should a platform serving India from a US-based company map network, storage and legal questions separately?
10. If a video is stored on a US origin server and a user is in Mumbai, how could delivery latency be reduced?

## 18. Practical exercise

Draw a simple global application flow on paper or in a diagram tool:

```text
User in India
  -> mobile or Wi-Fi ISP
  -> DNS resolver
  -> CDN edge
  -> application entry point / load balancer
  -> API service
  -> user database + cache
  -> media object storage (controlled access)
```

For every arrow, write:

- Which protocol or service may be involved?
- In which direction does data travel?
- Does the step contain personal data?
- What retry or fallback is available if it fails?
- How would you secure the step?

---

## Sources and further reading

1. [DARPA — ARPANET history](https://www.darpa.mil/news/features/arpanet) — early ARPANET nodes and the TCP/IP transition.
2. [Internet Society — A Brief History of the Internet](https://www.internetsociety.org/internet/history-internet/brief-history-internet/) — packet networking, early nodes and the NCP-to-TCP/IP transition.
3. [Computer History Museum — Networking & the Web timeline](https://www.computerhistory.org/timeline/networking-the-web/) — packet switching, email, online services, BBSs, Usenet and Web milestones.
4. [Communications Museum Trust — Packet switching](https://www.comms.org.uk/emuseum/packetswitching/) — Donald Davies and packet-switching history.
5. [Lemelson-MIT — Ray Tomlinson](https://lemelson.mit.edu/resources/ray-tomlinson) — 1971 network email and the `@` notation.
6. [CERN — A short history of the Web](https://home.cern/science/computing/the-birth-of-the-web/short-history-web/) — Tim Berners-Lee, the early Web and CERN's 1993 release.
7. [CERN — The birth of the Web](https://home.cern/science/computing/the-birth-of-the-web) — institutional history and the first website.
8. [W3C — History timeline description](https://www.w3.org/2005/01/timelines/description) — early Internet, TCP/IP, DNS and Web dates.
9. [ITU — Overview of ITU history](https://www.itu.int/en/history/pages/ITUsHistory-page-6.aspx) — global telecommunications and Internet context.

*Dates are simplified into a learning timeline. Many technologies developed over several years through the work of multiple teams rather than being invented in one instant.*
