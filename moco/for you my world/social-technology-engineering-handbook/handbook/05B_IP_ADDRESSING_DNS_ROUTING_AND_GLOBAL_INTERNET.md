# 05B — IP Addressing, Subnets, DNS, Routing and the Global Internet

**Series:** Technology Foundations  
**Edition:** English 1.0  
**Purpose:** Understand how devices and networks are identified, how traffic finds its destination and how networks around the world exchange data.

---

## 1. What you will learn

This chapter covers MAC and IP addresses, IPv4 and IPv6, subnets and CIDR, gateways and routing tables, DHCP, NAT, DNS, DNS security, autonomous systems, BGP, ISPs, peering, transit, Internet Exchange Points, submarine cables, anycast and CDN delivery. It also includes safe labs for inspecting your own network.

## 2. MAC address versus IP address

### MAC address

A Media Access Control (MAC) address is used for link-layer delivery on a local network. Ethernet and Wi-Fi interfaces have link-layer addressing rules. A MAC address is commonly represented as six hexadecimal octets, such as `00:1A:2B:3C:4D:5E`, although modern interfaces and protocols have additional details.

A MAC address is not a reliable global identity. Devices can use locally administered or randomised addresses, and routers do not normally forward the original Ethernet frame unchanged across the entire Internet. Each link may have its own link-layer frame.

### IP address

An Internet Protocol (IP) address identifies a network-layer interface/address for routing. IPv4 addresses are 32 bits; IPv6 addresses are 128 bits. Routers use destination IP information and routing tables to forward packets between networks.

| MAC address | IP address |
|---|---|
| Link-layer delivery | Network-layer addressing and routing |
| Used on a local link | Used across interconnected IP networks |
| Commonly represented in hexadecimal | IPv4 dotted decimal; IPv6 hexadecimal groups |
| May be randomised or changed | May be assigned dynamically or statically |

## 3. IPv4

IPv4 uses 32-bit addresses, commonly written as four decimal octets, for example `192.0.2.10`. The theoretical address space is about 4.3 billion values, but reserved ranges and allocation structure reduce the number available for ordinary public use.

### Public versus private IPv4

Private IPv4 ranges defined by RFC 1918 are commonly used inside homes and organisations:

- `10.0.0.0/8`
- `172.16.0.0/12`
- `192.168.0.0/16`

These ranges are not globally routed on the public Internet. A router commonly uses Network Address Translation (NAT) so multiple private-address devices can share one or more public addresses.

### Special-purpose IPv4 examples

- `127.0.0.0/8`: loopback range; `127.0.0.1` is commonly used to refer to the local host.
- `169.254.0.0/16`: link-local range, commonly seen when normal address configuration is unavailable.
- `0.0.0.0`: context-dependent unspecified address, often used in binding or routing contexts.
- `255.255.255.255`: limited broadcast address.
- `192.0.2.0/24`, `198.51.100.0/24` and `203.0.113.0/24`: documentation ranges; examples should use these rather than real public addresses.

Address use is defined by standards and registries. Do not assume every address outside RFC 1918 is safe to probe or use.

## 4. Why was IPv6 developed?

The growth of Internet-connected devices created pressure on the limited IPv4 address space. IPv6 provides a much larger address space and includes design changes for modern IP networking.

### IPv6 basics

An IPv6 address is 128 bits and is written in hexadecimal groups separated by colons, for example:

```text
2001:db8:1234:0000:0000:0000:0000:0001
```

Leading zeroes in a group can be omitted, and one continuous sequence of zero groups can be compressed using `::` once:

```text
2001:db8:1234::1
```

`2001:db8::/32` is within the documentation prefix used for examples. IPv6 includes global unicast, link-local, unique-local, multicast and other address types. IPv6 does not use broadcast in the same way as IPv4; multicast and anycast are used for related communication patterns.

IPv6 adoption does not mean IPv4 disappears immediately. Many networks operate dual-stack or use transition mechanisms. Application developers should test IPv4 and IPv6 connectivity where relevant.

## 5. Subnets, prefixes and CIDR

A subnet divides an IP address space into network and host portions. CIDR notation expresses a prefix length, such as `/24` for a 24-bit network prefix.

Example: `192.168.10.0/24` has 24 network bits and 8 remaining bits. In a conventional IPv4 subnet, that range contains 256 addresses, with the first and last traditionally used for the network and broadcast addresses. Special-purpose and point-to-point configurations can differ, so do not apply the “usable host count” shortcut to every prefix.

### Example: splitting an office network

An office may use separate VLANs/subnets for staff devices, guest Wi-Fi, servers, printers and management. Segmentation can reduce unnecessary access and limit the impact of a compromised device.

A subnet plan should document:

- Network prefix and gateway.
- VLAN or network purpose.
- DHCP scope and reserved addresses.
- Allowed routes and firewall rules.
- DNS configuration.
- Ownership and change history.

## 6. Default gateway and routing table

A **default gateway** is the next-hop router a host uses when it does not have a more specific route for a destination. A routing table contains destination prefixes, next hops, interfaces and metrics or policy information.

### Example

A laptop has an address such as `192.168.1.25/24` and a default gateway such as `192.168.1.1`. Traffic for another device on the same subnet may be sent directly on the local link. Traffic for a public Internet address is normally sent to the default gateway.

A route is not a guarantee that the destination application is available. Routing only provides a path at the network layer; firewalls, servers, DNS, TLS and application logic can still fail.

## 7. DHCP: how does a device receive network configuration?

Dynamic Host Configuration Protocol (DHCP) can provide clients with network settings such as an IP address, subnet mask/prefix, default gateway, DNS resolver and lease time.

A simplified DHCPv4 exchange is often described as DORA:

1. **Discover:** Client searches for a DHCP server.
2. **Offer:** A server offers configuration.
3. **Request:** Client requests the offered configuration.
4. **Acknowledge:** Server confirms the lease.

Real deployments may use relays, reservations, multiple servers and additional options. A DHCP lease is time-bound; clients renew it according to protocol behaviour.

If a Windows device receives a `169.254.x.x` address unexpectedly, it may indicate that normal DHCP configuration failed. This is a clue, not a complete diagnosis.

## 8. What is NAT?

Network Address Translation changes address and sometimes port information as traffic passes through a network device. Home routers often use NAT so several private-address devices can share a public IPv4 address. Port Address Translation (PAT), sometimes called NAT overload, maps multiple private flows to different external ports.

### Benefits and trade-offs of NAT

Benefits:

- Helps conserve public IPv4 addresses.
- Allows use of private addressing inside a network.
- Can simplify some internal addressing plans.

Trade-offs:

- Inbound connectivity can require explicit port mapping or relay mechanisms.
- Some protocols need NAT traversal support.
- Troubleshooting becomes more complex because one public address may represent many internal devices.
- NAT is not a replacement for a firewall or application security.

IPv6 can provide globally routable addresses, but firewall policy and access control are still essential. Do not assume that a globally routable address means a device should be publicly reachable.

## 9. DNS: from human-readable names to network destinations

DNS is a distributed hierarchical naming system. It lets users and applications refer to names such as `example.com` rather than memorising IP addresses.

### DNS hierarchy

A simplified hierarchy:

```text
Root DNS servers
      |
Top-level domain servers (.com, .org, .in, etc.)
      |
Authoritative DNS servers for example.com
      |
Records such as A, AAAA, MX, TXT, CNAME
```

A recursive resolver performs lookups on behalf of a client. It may cache answers so later requests can be faster.

### DNS query flow

1. The application asks the operating system or configured resolver for a name.
2. Local caches are checked.
3. If necessary, a recursive resolver queries the DNS hierarchy.
4. The resolver obtains the answer from authoritative DNS, directly or through referrals.
5. The answer is returned and cached according to its TTL and policy.
6. The client uses the returned address or service information.

The exact flow can be affected by caches, encrypted DNS, split-horizon DNS, enterprise resolvers, VPNs and local network configuration.

### Common DNS record types

| Record | Purpose |
|---|---|
| A | Maps a name to an IPv4 address |
| AAAA | Maps a name to an IPv6 address |
| CNAME | Aliases one name to another name |
| MX | Specifies mail exchangers |
| TXT | Stores text used for verification and policy records, among other uses |
| NS | Identifies authoritative name servers |
| SOA | Provides zone authority and serial/timing information |
| SRV | Describes a service endpoint and related parameters |
| PTR | Reverse lookup mapping, commonly address to name |

### TTL and the propagation misconception

DNS records include a Time To Live (TTL), which guides how long a resolver may cache an answer. People often say “DNS propagation” as if every DNS server updates at the same moment. In reality, caches expire at different times, authoritative servers may be updated separately and resolver behaviour varies. A TTL does not force every cache to refresh immediately.

## 10. DNS security and privacy

DNS can be attacked or misconfigured. Risks include cache poisoning, domain-account compromise, registrar takeover, malicious record changes and leakage of browsing metadata.

### DNSSEC versus encrypted DNS

- **DNSSEC:** Adds cryptographic authentication to DNS data, helping resolvers validate that signed records have not been altered. It does not encrypt DNS queries and does not hide the queried domain.
- **DoT (DNS over TLS):** Encrypts DNS communication between a client and resolver using TLS.
- **DoH (DNS over HTTPS):** Carries DNS queries over HTTPS.

Encrypted DNS protects the connection to the resolver but does not guarantee that the resolver is trustworthy or that all metadata is hidden. DNSSEC and encrypted DNS solve different problems and can be used together.

Protect domain registrar accounts with MFA, restricted access and change alerts. Use registrar locks where appropriate. Keep DNS changes reviewed and recorded.

## 11. Routing: how does a packet reach a destination network?

A router compares a destination IP address with its routing table and forwards the packet to an appropriate next hop. Routers may use static routes, internal routing protocols and external routing protocols.

### Autonomous System (AS)

An Autonomous System is a network or group of networks operated under a common routing policy. It is identified by an Autonomous System Number (ASN). Large ISPs, cloud providers, content networks and universities may operate one or more ASNs.

### BGP

Border Gateway Protocol (BGP) exchanges reachability information between autonomous systems. It helps networks decide which paths can reach destination prefixes. BGP path selection involves policy and attributes; it is not simply “choose the geographically shortest route”.

BGP misconfiguration, route leaks and route hijacks can affect reachability. Route-origin validation, filtering, monitoring and coordination with upstream providers help reduce risk, but no single control removes every routing risk.

## 12. ISPs, peering, transit and Internet Exchange Points

- **ISP:** Provides Internet connectivity to consumers or organisations.
- **Transit provider:** Sells access to routes across other networks/the wider Internet.
- **Peering:** Two networks exchange traffic directly under an agreed arrangement, often to reduce cost or improve performance.
- **Internet Exchange Point (IXP):** A physical or logical interconnection facility where multiple networks exchange traffic.
- **Content network:** A network operated by a content or cloud provider to deliver its services.

A network may buy transit, peer with other networks, connect to an IXP or use a combination. Commercial agreements, capacity and traffic patterns influence the design.

## 13. Undersea cables, terrestrial fibre and satellite links

The global Internet depends heavily on fibre-optic infrastructure, including submarine cables crossing oceans. Terrestrial fibre connects cities, data centres and network exchange sites. Satellites provide connectivity where terrestrial deployment is difficult or as an alternative path.

Different satellite orbits have different latency and capacity characteristics. Geostationary satellite links commonly have higher round-trip latency than low-Earth-orbit systems because of orbital distance, although real service performance depends on the full network path.

Cable routes, landing stations, terrestrial backhaul, power, physical protection and repair capacity are important parts of global Internet resilience.

## 14. Anycast and CDN: one service from multiple locations

**Anycast** allows the same IP address to be announced from multiple network locations. Routing directs a client towards one suitable announcement according to network routing decisions. Anycast is commonly used in DNS and some edge-service designs.

A **Content Delivery Network (CDN)** distributes or caches content across edge locations. It can reduce latency and origin load. CDN performance depends on routing, cache hit ratio, content rules, capacity and origin health.

Anycast and CDN are related in some deployments but are not identical concepts. Anycast is a routing technique; a CDN is a content-delivery architecture/service.

## 15. A real-world country-to-country data-path example

Imagine a user in Mumbai opens an application whose API origin is in Europe and whose CDN has an edge in India.

A possible flow:

1. The device resolves the application hostname using its configured DNS resolver.
2. The browser or mobile app connects to an appropriate CDN or application entry point.
3. Routing across the ISP, peering/transit and provider networks carries packets.
4. The CDN may serve cached public content locally.
5. Dynamic API requests may be forwarded to the origin region.
6. The backend may query a database, cache or other internal service.
7. Responses return through the delivery path.

This is only a conceptual example. The real path depends on the provider, ISP, routing, CDN configuration, data placement, application design and user location. The physical route is not necessarily the shortest geographic path.

Also separate **network path** from **data governance**. A packet travelling through a country does not by itself prove that the service stores or processes personal data there. Storage, access, processing and cross-border transfer need separate mapping and legal analysis.

## 16. Safe practical labs

### Lab A — Inspect your IP configuration

Windows:

```powershell
ipconfig /all
```

Linux:

```bash
ip address
ip route
```

macOS:

```bash
ifconfig
route -n get default
```

Read the output; do not change settings unless you understand the impact.

### Lab B — DNS lookup

```bash
nslookup example.com
```

or:

```bash
dig example.com A
dig example.com AAAA
```

### Lab C — View a route path

```bash
traceroute example.com
```

Windows:

```powershell
tracert example.com
```

Results may be incomplete because routers and firewalls can filter or deprioritise diagnostic packets. A missing hop does not necessarily mean the network is broken.

### Lab D — Router and DNS troubleshooting

1. Confirm the device has an address and default gateway.
2. Test access to the local gateway.
3. Test a known IP destination you are authorised to access.
4. Test DNS resolution.
5. Compare with another device or network.
6. Record the time, output and recent configuration changes.

## 17. Self-check

1. What is the difference between a MAC address and an IP address?
2. Why are private IPv4 ranges not routed on the public Internet?
3. What problem does IPv6 address?
4. What does `/24` mean in CIDR notation?
5. What does DHCP provide?
6. Why does NAT not replace a firewall?
7. What is the role of a recursive DNS resolver?
8. How do DNSSEC and DoH differ?
9. What is an ASN and why does BGP use it?
10. What is the difference between peering and transit?
11. Why is an Anycast address not the same thing as a CDN?
12. Why should network paths and data-residency questions be analysed separately?

## References

1. [RFC 1918 — Address Allocation for Private Internets](https://www.rfc-editor.org/rfc/rfc1918)
2. [RFC 4291 — IPv6 Addressing Architecture](https://www.rfc-editor.org/rfc/rfc4291)
3. [RFC 4632 — Classless Inter-domain Routing (CIDR)](https://www.rfc-editor.org/rfc/rfc4632)
4. [RFC 2131 — Dynamic Host Configuration Protocol](https://www.rfc-editor.org/rfc/rfc2131)
5. [RFC 3022 — Traditional IP Network Address Translator](https://www.rfc-editor.org/rfc/rfc3022)
6. [RFC 1034 — Domain Names: Concepts and Facilities](https://www.rfc-editor.org/rfc/rfc1034)
7. [RFC 4033 — DNS Security Introduction and Requirements](https://www.rfc-editor.org/rfc/rfc4033)
8. [RFC 8484 — DNS Queries over HTTPS](https://www.rfc-editor.org/rfc/rfc8484)
9. [RFC 7858 — DNS over TLS](https://www.rfc-editor.org/rfc/rfc7858)
10. [RFC 4271 — Border Gateway Protocol 4](https://www.rfc-editor.org/rfc/rfc4271)
11. [Internet Society — Internet Exchange Points](https://www.internetsociety.org/issues/ixps/)

**Study rule:** You understand this chapter when you can read your device's IP configuration, explain how DNS resolves a name and describe how an ISP and BGP help connect networks.
