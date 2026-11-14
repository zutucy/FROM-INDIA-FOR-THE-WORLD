# 05A — Networking Foundations and the History of Computer Networks

**Series:** Technology Foundations  
**Edition:** English 1.0  
**Purpose:** Understand how devices communicate, how data moves through physical networks, why networking protocols exist and how computer networks evolved into the global Internet.

---

## 1. Chapter goal

This chapter introduces the foundation of networking. You will learn:

- How two or more computers communicate.
- Why the Internet is a network of interconnected networks rather than one company's network.
- The roles of packet switching, protocols, routers, switches, ISPs, autonomous systems and Internet Exchange Points.
- Major historical contributions from ARPANET, TCP/IP, Ethernet, NSFNET, DNS and the commercial Internet.
- How the OSI and TCP/IP models help with practical troubleshooting.
- The differences between latency, bandwidth, throughput, packet loss, jitter and availability.

Networking is not only relevant to social media. Banking, hospitals, games, video streaming, factories, cloud computing, AI services, online education, logistics, government systems and almost every connected technology depend on it.

## 2. What is a network?

A **computer network** is a system of two or more computing devices that exchange data through defined communication rules. Devices may include computers, phones, servers, printers, cameras, sensors, routers or industrial machines.

Example: a laptop, phone and smart TV connected to home Wi-Fi form a local network. When the phone requests a public website, traffic may travel from the local network through an ISP and several other networks before reaching the destination.

### Basic parts of a network

| Part | Simple meaning | Why it is needed |
|---|---|---|
| End device/host | Phone, laptop, server or camera | Creates or consumes data |
| Network interface | Ethernet port or Wi-Fi adapter | Connects the device to a network medium |
| Medium | Copper cable, fibre or radio waves | Carries signals |
| Switch | Connects devices on the same local network | Forwards local frames to the correct port |
| Router | Connects different IP networks | Forwards packets towards another network |
| Access point | Connects Wi-Fi devices to a wired network | Provides wireless access |
| Firewall | Enforces traffic rules | Restricts unwanted or unauthorised communication |
| Server | A system providing a service | Serves websites, databases, email, files or APIs |
| Client | A system requesting a service | Sends requests through a browser, app or device |

Client/server is a common pattern, but the Internet also supports peer-to-peer communication, distributed systems and device-to-device protocols.

## 3. How does data physically travel?

Digital data consists of bits (0 and 1), but a network medium represents those bits as physical signals:

- Electrical signals in copper cables.
- Light pulses in fibre-optic cables.
- Radio-frequency electromagnetic signals in Wi-Fi and cellular systems.
- Radio signals, long-distance paths and ground stations in satellite links.

Each medium has different speed, capacity, distance, interference tolerance, cost and deployment complexity.

### Copper, fibre and wireless

| Medium | Strengths | Limitations | Common uses |
|---|---|---|---|
| Twisted-pair copper Ethernet | Affordable and practical for local networks | Distance and interference limits | PCs, switches and access points |
| Coaxial cable | Useful in cable-broadband systems | Depends on provider architecture | Cable Internet and TV networks |
| Fibre optic | High capacity and long-distance transmission | Installation and repair can be specialised | Data centres, ISP backbones and submarine links |
| Wi-Fi | Convenient wireless access | Shared radio medium, interference and range limits | Homes, offices and public access |
| Cellular | Wide-area mobile connectivity | Coverage, spectrum and congestion vary | Phones, IoT and mobile routers |
| Satellite | Reaches remote locations | Latency and capacity depend on orbit and service | Remote connectivity and backup paths |

Advertised link speed and an application's real download speed are not the same. Protocol overhead, congestion, server capacity, Wi-Fi interference, distance, packet loss and shared bandwidth affect actual throughput.

## 4. Packet switching: a fundamental Internet idea

Some older communication systems established a dedicated path or circuit. Packet-switched networking divides data into smaller units—**packets**—that share network resources with other traffic.

Example: a user uploads a 5 MB image. Application data moves through the transport layer; the network stack organises it into packets or segments. Routers forward IP packets towards the destination. Packets may take different paths depending on routing and network conditions. The destination's higher layers reconstruct the original data.

Advantages:

1. Network links can be statistically shared among many users.
2. Different networks can interconnect through common protocols.
3. Alternative routes may be available when a link fails, depending on topology and routing convergence.
4. Bursty application traffic can use shared capacity efficiently.

Trade-offs:

- Delay can vary.
- Packets can be dropped, duplicated or delivered out of order.
- Congestion control and retransmission may be necessary.
- Real-time applications must manage latency and jitter.

IP offers a **best-effort** delivery service. IP alone does not guarantee that a packet will arrive, remain in order or avoid duplication. Higher-level protocols or the application provide additional reliability where needed. See [RFC 791](https://www.rfc-editor.org/rfc/rfc791) for the original IPv4 protocol specification.

## 5. What is a network protocol?

A protocol is an agreed set of rules for communication. A protocol may specify:

- Message format and field meanings.
- How a sender identifies a receiver.
- How a connection or session starts and ends.
- How errors are detected or reported.
- How data is sequenced, acknowledged or retransmitted.
- What security properties are provided.

Examples include Ethernet, Wi-Fi, IP, TCP, UDP, DNS, HTTP, TLS and BGP. Different protocols operate at different layers and solve different problems. No single protocol handles every part of communication.

## 6. Networking history: from isolated computers to the Internet

### 1950s–1960s: computers were expensive and isolated

Large computers were operated by institutions, research laboratories and governments. Remote access and resource sharing were difficult. Researchers began exploring how computers at different locations could communicate and how network resources could be shared.

### 1969: early ARPANET nodes

The first ARPANET nodes connected UCLA, Stanford Research Institute, UC Santa Barbara and the University of Utah by the end of 1969. The project demonstrated packet-switched communication between research computers.

### 1970s: the larger internetworking challenge

Researchers wanted different packet networks to communicate, even if they used different underlying technologies. This required an internetworking architecture and common protocols.

### 1974: an early TCP design paper

Vint Cerf and Robert Kahn published influential work on a protocol for interconnecting packet networks. The design evolved over time into the TCP/IP architecture.

### 1970s–1980s: Ethernet and local-area networks

Ethernet, developed at Xerox PARC and later standardised, became a major technology for connecting devices inside buildings and campuses. Local-area networks (LANs) made it practical for offices and universities to share printers, files and servers.

### 1 January 1983: ARPANET's TCP/IP transition

ARPANET's transition from NCP to TCP/IP was an important interoperability milestone. It helped establish the protocol foundation of the modern Internet.

### 1983–1987: DNS emerges

As network use grew, maintaining a manually distributed host-name file became difficult. The Domain Name System introduced a distributed naming hierarchy. Paul Mockapetris published the original DNS specifications in 1983; later RFCs refined them.

### 1986 onward: NSFNET

The US National Science Foundation's NSFNET supported research and academic networking and became an important backbone initiative. Additional networks and commercial providers expanded connectivity.

### 1990s: Web and commercial Internet growth

The World Wide Web made publishing and browsing linked documents easier. Commercial ISPs, browsers, search services, websites and online businesses helped Internet access spread beyond research institutions.

### 2000s–2020s: broadband, mobile, cloud and edge

Fibre, cable broadband, Wi-Fi, 3G/4G/5G, data centres, public cloud, CDNs and edge services changed how applications are deployed and consumed. Modern networking must support cloud APIs, video, real-time communication, connected devices and large distributed systems.

## 7. Internet versus Web versus Wi-Fi versus mobile network

- **Internet:** The global system of interconnected IP networks.
- **World Wide Web:** A system of linked resources and applications, commonly accessed using HTTP/HTTPS.
- **Wi-Fi:** A family of wireless local-area networking standards. Wi-Fi can connect a device to a local network; it is not itself the global Internet.
- **Mobile network:** Cellular access infrastructure such as 4G or 5G. It may provide a path to the Internet, but it can also support provider-managed services.

A phone can use Wi-Fi without Internet access if the local router is not connected to an ISP. Similarly, a device can reach local network resources while public Internet access is unavailable.

## 8. The OSI model and TCP/IP model

Layered models help engineers separate responsibilities. They are conceptual tools, not a perfect description of every modern implementation.

### OSI model (seven layers)

| Layer | Name | Example responsibility/protocol |
|---|---|---|
| 7 | Application | HTTP, DNS, SMTP application behaviour |
| 6 | Presentation | Data representation, encoding and transformations |
| 5 | Session | Session/dialogue coordination concepts |
| 4 | Transport | TCP, UDP; process-to-process delivery |
| 3 | Network | IP addressing and routing |
| 2 | Data Link | Ethernet/Wi-Fi frames and local-link delivery |
| 1 | Physical | Electrical, optical and radio signalling |

### Simplified TCP/IP model

| TCP/IP layer | Roughly covers | Examples |
|---|---|---|
| Application | OSI 5–7 | HTTP, DNS, SMTP, SSH |
| Transport | OSI 4 | TCP, UDP, QUIC's transport model over UDP |
| Internet | OSI 3 | IPv4, IPv6, ICMP |
| Link | OSI 1–2 | Ethernet, Wi-Fi, physical media |

Do not force every protocol into a perfect one-to-one mapping. Use the models to ask where a failure might occur.

## 9. Network performance: more than Mbps

- **Bandwidth:** A link's maximum or provisioned data-transfer capacity in a defined context.
- **Throughput:** The data actually transferred per unit of time.
- **Latency:** The time delay for a packet or request to travel and receive a response.
- **Round-trip time (RTT):** Time for a signal or request to travel to a destination and back.
- **Packet loss:** Packets that fail to reach the destination or are discarded.
- **Jitter:** Variation in packet delay, important for real-time audio/video.
- **Availability:** The proportion of time a service or path is usable.
- **Congestion:** Demand exceeds available network resources, increasing delay or loss.

A video call may work poorly even when the advertised bandwidth is high if jitter and packet loss are significant. A database API may be slow because of server processing or database locks even when the network is healthy.

## 10. Core vocabulary

- **LAN:** Local Area Network.
- **WAN:** Wide Area Network.
- **VLAN:** Virtual LAN, a logical segmentation mechanism.
- **NIC:** Network Interface Controller.
- **Router:** Device that forwards packets between IP networks.
- **Switch:** Device that forwards frames within a local network.
- **ISP:** Internet Service Provider.
- **PoP:** Point of Presence, a provider's network location.
- **IXP:** Internet Exchange Point where networks interconnect and exchange traffic.
- **ASN:** Autonomous System Number.
- **BGP:** Border Gateway Protocol.
- **MTU:** Maximum Transmission Unit for a link or path context.
- **QoS:** Quality of Service mechanisms for traffic treatment.

## 11. Short practical exercise

Draw a simple home network: phone, laptop, Wi-Fi access point/router, ISP modem/ONT and Internet. Label which components are on the local network and which belong to the provider network. Then draw the path for a browser request to a remote website.

## 12. Self-check questions

1. What makes a network different from two devices merely sharing the same room?
2. Why did packet switching suit bursty computer traffic?
3. What is the difference between a router and a switch?
4. How do Wi-Fi and the Internet differ?
5. Why are protocols needed?
6. What did ARPANET demonstrate?
7. Why was the TCP/IP transition important?
8. What problem did DNS address?
9. How are latency and throughput different?
10. Why can a video call perform poorly even when a speed test reports high bandwidth?

## References and further reading

1. [Internet Society — A Brief History of the Internet](https://www.internetsociety.org/internet/history-internet/brief-history-internet/)
2. [DARPA — ARPANET history](https://www.darpa.mil/news/features/arpanet)
3. [RFC 791 — Internet Protocol](https://www.rfc-editor.org/rfc/rfc791)
4. [RFC 8200 — Internet Protocol, Version 6](https://www.rfc-editor.org/rfc/rfc8200)
5. [RFC 9293 — Transmission Control Protocol](https://www.rfc-editor.org/rfc/rfc9293)
6. [IEEE 802.3 Ethernet Working Group](https://www.ieee802.org/3/)
7. [IEEE 802.11 Wireless LAN Working Group](https://www.ieee802.org/11/)
8. [RFC 1034 — Domain Names: Concepts and Facilities](https://www.rfc-editor.org/rfc/rfc1034)
9. [RFC 1035 — Domain Names: Implementation and Specification](https://www.rfc-editor.org/rfc/rfc1035)

**Study rule:** You understand this chapter when you can sketch how a packet moves from a laptop through a home router and ISP to a remote service, and explain where each layer contributes.
