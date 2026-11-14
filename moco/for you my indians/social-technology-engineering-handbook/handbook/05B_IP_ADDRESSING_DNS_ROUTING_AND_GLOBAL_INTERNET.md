# 05B — IP Addressing, Subnets, DNS, Routing and the Global Internet

**Part:** 05 — Networking and Internet Protocols  
**Language:** Detailed Hinglish  
**Research snapshot:** 13 November 2026

---

## 1. Is chapter mein kya seekhenge?

- MAC address, IP address, public/private IP, IPv4 and IPv6.
- Subnet, CIDR, subnet mask, default gateway and NAT.
- DHCP and ARP/Neighbor Discovery.
- DNS hierarchy, recursive resolver, authoritative nameserver and record types.
- DNS cache, TTL, DNSSEC, DoH and DoT.
- Routing tables, static/dynamic routing and BGP.
- ISP, transit, peering, IXP, submarine cables and global network paths.
- CDN, anycast, region placement and why a website may feel fast in one country and slow in another.

## 2. MAC address vs IP address

Dono addresses hain, lekin same job nahi karte.

### MAC address

MAC (Media Access Control) address local link technology par network interface ko identify karne ke liye use hota hai. Ethernet/Wi-Fi frame delivery mein MAC addressing important hai. MAC address usually 48-bit hota hai in classic Ethernet/Wi-Fi contexts, though address formats and interface behaviours have nuances.

- Local link par frame next device tak pahunchane mein help karta hai.
- Router ek IP network se next network mein packet forward karte waqt link-layer frame ko next link ke hisaab se rebuild karta hai.
- Device privacy features Wi-Fi par randomized MAC addresses use kar sakte hain.
- MAC address global Internet routing ka replacement nahi hai.

### IP address

IP address network layer par logical addressing provide karta hai. Routers destination IP prefix ke basis par packets forward karte hain.

A useful analogy:
- MAC address: local building/corridor mein next delivery point.
- IP address: broader network mein destination network/host address.

Analogy perfect nahi hai, but difference samajhne mein help karti hai.

## 3. IPv4

IPv4 address 32 bits ka hota hai, generally dotted-decimal form mein show hota hai, e.g. `203.0.113.10`. Har dotted number 0–255 ke beech hota hai because it represents 8 bits.

32-bit address space theoretically 2^32 values provide karta hai, lekin reserved ranges, allocation structure and special purposes ki wajah se sab addresses public hosts ko assign nahi kiye ja sakte.

### Public vs private IPv4

Private IPv4 ranges RFC 1918 mein defined hain:

| Private range | Common home/office example |
|---|---|
| `10.0.0.0/8` | Large private networks |
| `172.16.0.0/12` | Medium private networks |
| `192.168.0.0/16` | Common home routers, e.g. 192.168.1.x |

Private addresses public Internet par globally unique routable destination ke roop mein normally advertise nahi hote. Router Network Address Translation (NAT) use karke private network ke traffic ko public address ke through map kar sakta hai.

**Warning:** Private IP range ko security feature mat samjho. Internal device par malicious app ho sakti hai; compromised device se attack possible hai. Network segmentation and firewall rules phir bhi needed hain.

### Special-purpose IPv4 examples

- `127.0.0.1`: Loopback / local machine testing (127/8 range).
- `169.254.0.0/16`: Link-local auto-addressing context.
- `0.0.0.0`: Context-dependent unspecified address; server bind config mein all local interfaces ka meaning ho sakta hai, but every context mein same use nahi.
- `255.255.255.255`: Limited broadcast.
- `192.0.2.0/24`, `198.51.100.0/24`, `203.0.113.0/24`: Documentation examples ke liye reserved ranges (real production public host address na samjhein).

## 4. IPv6 kyun develop hua?

Internet growth ke saath 32-bit IPv4 address space limited hone laga. NAT ne addresses conserve karne mein help ki, lekin large-scale address sharing, inbound connectivity, peer-to-peer and operational complexity create ki. IPv6 128-bit address space provide karta hai.

Example IPv6 address:

`2001:db8:1234:0000:0000:0000:0000:0001`

Shortened form:

`2001:db8:1234::1`

`2001:db8::/32` documentation examples ke liye reserved prefix hai. Actual public IPv6 address different hoga.

### IPv6 basics

- 128-bit addressing.
- Hexadecimal groups separated by colons.
- `::` ek sequence of zero groups ko shorten kar sakta hai, ek address mein once.
- Link-local IPv6 addresses often `fe80::/10` range se.
- IPv6 networks usually `/64` subnets use karte hain for many ordinary LAN designs, though architecture-specific exceptions exist.
- IPv6 uses Neighbor Discovery Protocol (NDP) over ICMPv6 instead of IPv4 ARP for local neighbor discovery.
- IPv6 does not mean every device automatically has unrestricted public access; firewall and policy still matter.

The main IPv6 specification is [RFC 8200](https://www.rfc-editor.org/rfc/rfc8200). It has later updates/errata; standard status should be checked at the RFC Editor rather than relying on a random tutorial. [1]

## 5. Subnet, prefix and CIDR

Subnetting ek large IP block ko smaller logical networks mein divide karta hai. Isse address allocation, routing, isolation and network management easier hota hai.

**CIDR** notation `address/prefix-length` format use karta hai. Prefix length batata hai kitne leftmost bits network prefix represent karte hain.

Examples:

- `192.168.1.0/24`: first 24 bits network prefix; remaining 8 bits address space.
- `10.20.0.0/16`: first 16 bits prefix.
- `172.20.4.0/22`: first 22 bits prefix.

Simple `/24` IPv4 subnet mein 256 total addresses hote hain. Traditional subnet use mein network and broadcast address reserve hote hain, so 254 host addresses often quoted hain. Modern contexts (point-to-point links, special subnet rules, IPv6) mein assumptions alag ho sakti hain.

### Example: office network split

Suppose an office has:
- Staff laptops.
- Guest Wi-Fi.
- Servers.
- CCTV/IoT devices.

Sabko same flat network par rakhne ke bajay separate VLANs/subnets bana sakte hain. Firewall rules decide karenge ki guest Wi-Fi sirf Internet access kare, staff approved internal apps access kare, aur camera network only required recorder/management endpoints tak communicate kare.

This is **network segmentation**. It limits blast radius; segmentation alone is not complete security.

## 6. Default gateway and routing table

A device apne local subnet ka destination directly local link par reach kar sakta hai. Agar destination local subnet ke bahar ho, packet usually default gateway (router) ko bheja jata hai.

Routing table destination prefixes aur next-hop/interface decisions store karti hai. Router commonly longest-prefix match use karta hai: most specific matching route select hota hai.

### Example

Laptop: `192.168.1.20/24`  
Gateway: `192.168.1.1`  
Website IP: `203.0.113.80`

`203.0.113.80` local `192.168.1.0/24` range mein nahi, isliye laptop gateway ke MAC address tak local Ethernet/Wi-Fi frame bhejta hai. Router IP packet ko aage route karta hai.

## 7. DHCP: device ko network config kaise milti hai?

DHCP (Dynamic Host Configuration Protocol) device ko automatically network configuration lease kar sakta hai:

- IP address.
- Subnet mask/prefix.
- Default gateway.
- DNS resolver.
- Lease duration and other options.

IPv4 DHCP ka common initial flow DORA ke naam se padhaaya jata hai:

1. Discover — client DHCP server discover karta hai.
2. Offer — server configuration offer karta hai.
3. Request — client selected offer request karta hai.
4. Acknowledge — server lease confirm karta hai.

Actual networks relay agents, multiple servers, renewals and other details include kar sakte hain.

**Static IP** manually configured ho sakta hai. Servers/printers/network equipment ke liye static address or DHCP reservation useful ho sakta hai. Mistyped IP, duplicate allocation or wrong gateway connectivity break kar sakte hain.

## 8. NAT kya hai?

Network Address Translation packet headers mein address/port mapping karta hai. Home routers often many private IPv4 devices ko ek public IPv4 address ke through Internet access dete hain. Port Address Translation (PAT/NAPT) multiple flows distinguish karne mein help karta hai.

Example:
- Phone: `192.168.1.10:51000`
- Laptop: `192.168.1.11:52000`
- Router public IPv4: `198.51.100.20`

Router outbound connections ke mappings maintain kar sakta hai aur replies ko correct internal device tak route karta hai.

### NAT ke pros and cons

**Pros:** IPv4 public address conservation, common home/office deployment, internal addressing flexibility.

**Cons:** Inbound connections more complex; peer-to-peer traversal difficult ho sakta hai; logs and identity attribution complex; applications ko NAT traversal techniques chahiye ho sakti hain. NAT is not a firewall substitute, even if stateful NAT behaviour unsolicited inbound traffic ko often block karta hai.

IPv6 architecture globally unique addresses provide kar sakti hai; security phir bhi firewall policies par depend karti hai.

## 9. DNS: human-readable names se network addresses tak

Hum `example.com` ya `openai.com` yaad rakhte hain; network packets ko IP addresses chahiye. DNS (Domain Name System) distributed hierarchical naming system hai.

Paul Mockapetris ke DNS design ko 1983 ke work aur 1987 ke RFC 1034/1035 specifications ke context mein samjha jata hai. RFC 1034 concepts and facilities explain karta hai; RFC 1035 implementation and message format specify karta hai. [2]

### DNS hierarchy

1. Root zone (`.`)
2. Top-Level Domain (TLD), e.g. `.com`, `.org`, `.in`
3. Second-level domain, e.g. `example.com`
4. Subdomain, e.g. `api.example.com`, `media.example.com`

DNS centralized single database nahi hai. Data multiple zones and authoritative servers mein distributed hota hai.

### DNS query flow

Suppose browser `www.example.com` resolve kar raha hai:

1. Browser/OS local caches check kar sakte hain.
2. Device configured recursive resolver ko query bhejta hai (often ISP, public resolver, enterprise resolver).
3. Resolver ke paas cached answer nahi toh root servers se referral maang sakta hai.
4. Root response relevant TLD nameservers ki direction deta hai.
5. Resolver TLD nameserver se domain ke authoritative nameservers ke baare mein puchta hai.
6. Resolver authoritative nameserver se requested record leta hai.
7. Resolver response cache karta hai according to TTL and policy.
8. Client ko answer return hota hai.

Reality mein caching, CNAME chains, DNSSEC validation, delegation, DNS64, split-horizon DNS, encrypted transports and provider-specific optimisation flow ko affect kar sakte hain.

### DNS record types

| Record | Use |
|---|---|
| A | Hostname to IPv4 address |
| AAAA | Hostname to IPv6 address |
| CNAME | Alias to another DNS name |
| MX | Mail exchanger routing |
| TXT | Text data; SPF/DKIM/verification etc. use cases |
| NS | Zone ke authoritative nameservers |
| SOA | Zone authority and serial/timer metadata |
| SRV | Service location records |
| PTR | Reverse DNS mapping |
| CAA | Which certificate authorities may issue certificates for domain |

### TTL and propagation misconception

DNS record TTL cache duration hint karta hai. Record change ke baad sab users ko instant update guarantee nahi hota. Old cached values TTL expire hone tak remain kar sakti hain; registrar/registry delegation, resolver caching and client caches bhi matter karte hain.

Log commonly kehte hain “DNS propagation 24–48 hours,” but ye fixed universal protocol delay nahi hai. Actual result record TTL, previous cache state and DNS hierarchy par depend karta hai. Migration plan mein old TTL reduce karna (pehle se), new records verify karna and rollback plan rakhna sensible hai.

## 10. DNS security and privacy

DNS critical infrastructure hai, isliye attacker or misconfiguration DNS responses change karne ki koshish kar sakte hain.

- **DNS spoofing/cache poisoning:** resolver ko forged response accept karwane ka attempt.
- **Domain hijacking:** registrar or DNS provider account compromise karke records change karna.
- **Typosquatting:** lookalike domain register karke users ko trick karna.
- **DNS tunnelling:** DNS queries/responses misuse karke data transfer/command channel banana; detection challenge ho sakta hai.
- **DNS amplification:** misconfigured/open resolvers ka reflection DDoS mein misuse.

Defensive controls:

- Registrar account par strong MFA and recovery controls.
- DNS provider least-privilege access.
- DNSSEC signing/validation where supported and correctly managed.
- Change alerts and audit logs.
- Restricted recursive resolvers; open resolver expose na karna.
- Domain registration renewal and lock controls.
- Email authentication records (SPF, DKIM, DMARC) as relevant.

### DNSSEC vs encrypted DNS

- **DNSSEC** DNS data authenticity/integrity validate karne ka mechanism hai. It does not encrypt DNS query privacy.
- **DoT (DNS over TLS)** DNS transport ko TLS ke through encrypt karta hai.
- **DoH (DNS over HTTPS)** DNS queries ko HTTPS ke through carry karta hai.
- **DoQ** DNS over QUIC.

Encrypted DNS observer ko local path par queries read karna harder bana sakta hai, but resolver operator still queries see kar sakta hai unless other privacy mechanisms apply. DNSSEC and DoH/DoT different problems solve karte hain.

ICANN ke FAQ mein ek common misunderstanding clarify hai: DNS names map karta hai; routers aur BGP IP prefixes ke basis par packet path decisions handle karte hain. Root servers global traffic ke route controllers nahi hain. [3]

## 11. Routing: packet ko destination network tak kaise le jate hain?

Routing network paths choose karne aur packets forward karne ka process hai.

- Host routing table determine karti hai next hop.
- Router local routing/forwarding table lookup karta hai.
- Internal networks OSPF/IS-IS jaise interior gateway protocols use kar sakte hain.
- Large Internet ke independent networks (Autonomous Systems) ke beech BGP routes exchange karta hai.

### Autonomous System (AS)

Autonomous System ek network ya networks group hai jo common routing policy ke under operate karta hai and ASN use karta hai. ISP, cloud provider, large university network or large enterprise AS operate kar sakte hain.

### BGP

Border Gateway Protocol (BGP) inter-AS routing protocol hai. BGP speakers reachable IP prefixes and path attributes exchange karte hain. Network operators routing policy, business relationships, filtering, traffic engineering and resiliency decisions define karte hain.

BGP is not a simple shortest-distance GPS. Path selection depends on policy and attributes; route reachability ka matlab route safe/trustworthy hai, ye automatically prove nahi hota.

BGP risks:
- Accidental route leak.
- Prefix hijack or route origin misconfiguration.
- Poor filtering.
- Incorrect routing policy.

Defenses and operational practices include prefix filtering, max-prefix limits, route monitoring, RPKI Route Origin Validation, carefully planned peering and incident contacts. RPKI is helpful but doesn't solve every routing security issue.

Primary protocol reference: [RFC 4271 — BGP-4](https://www.rfc-editor.org/rfc/rfc4271), with a number of later updates. [4]

## 12. ISP, peering, transit and IXPs

Internet access ek chain se aa sakta hai:

- Home/office device.
- Wi-Fi router or enterprise switch.
- Access ISP/fibre/mobile operator.
- Regional/national backbone.
- Transit provider or peering partner.
- Internet Exchange Point or private interconnect.
- Destination network/cloud/CDN.

**Peering:** Two networks directly exchange traffic under agreed commercial/technical terms.

**Transit:** One network another network ko broader Internet reachability provide karta hai, typically commercial agreement ke through.

**IXP:** Facility/network where multiple networks interconnect and exchange traffic. IXP itself does not automatically become the Internet or dictate all route paths.

Peering and transit business agreements, traffic ratios, geography, capacity and policy par depend karte hain.

## 13. Undersea cables, terrestrial fibre and satellite links

Global traffic large extent mein terrestrial fibre aur submarine fibre-optic cable systems se travel karta hai. Cables continents ke beech enormous capacity connect karte hain; landing stations, backhaul, terrestrial networks and data centres se link hote hain.

Satellite connectivity remote regions, maritime, aviation and backup scenarios mein useful hoti hai. Different orbit types have different latency/coverage/capacity trade-offs. Low Earth Orbit systems geostationary orbit se lower latency offer kar sakte hain, but actual service depends on constellation, gateways, congestion, weather/obstruction and provider architecture.

Global digital service design mein geography matter karti hai:
- User India mein, app servers Europe mein, storage US mein, CDN edge Mumbai/Delhi mein ho sakta hai.
- User request edge location par terminate ho sakti hai, but origin database access still far region tak ja sakta hai.
- Cross-region replication introduces consistency, cost and legal/data-transfer questions.

## 14. Anycast and CDN: same service multiple locations se

Anycast mein same IP prefix multiple network locations se advertise ho sakta hai. Routing system client ko network path ke hisaab se reachable instance tak le ja sakta hai. Ye DNS resolvers, CDN and DDoS mitigation networks mein common concept hai.

CDN static/dynamic content ko geographically distributed edge network se serve kar sakta hai. Benefits:

- User-origin distance reduce.
- Cached files fast serve.
- Origin load decrease.
- DDoS absorption/edge security capabilities, provider design par depend.

Lekin CDN magic nahi:
- Private/personalized content carefully cache-control policy se handle hona chahiye.
- Cache invalidation and freshness design karna padta hai.
- User-specific response galti se shared cache mein store ho sakta hai if headers/config wrong.
- Dynamic database operations necessarily edge par cache nahi hote.

## 15. Real-world country-wise data path example

Maan lo ek company US mein incorporated hai, user India, Brazil and Germany mein hain, cloud compute Singapore and Frankfurt mein hai, and CDN multiple countries mein edge locations use karta hai.

Technical questions:
- DNS response user ko kaunsa endpoint deta hai?
- CDN cache hit hai ya origin request required?
- User data kis database region mein write hota hai?
- Backup kis country/region mein hai?
- Support staff ya subprocessors kin locations se access karte hain?
- Payment/identity provider kaunsa region process karta hai?
- Cross-border traffic ke contracts and legal requirements kya hain?

**Important:** Company incorporation country, user location, server location, data subject location and service targeting are separate facts. Applicable law sirf server ka country dekhkar decide nahi hota. Later Part 13–14 in questions ko deeper cover karega.

## 16. Safe practical labs

### Lab A — Apna IP config dekho

Windows PowerShell:

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
netstat -rn
```

Observe: assigned IP, prefix/netmask, default route, DNS resolver. Public-facing information share karne se pehle sensitive values redact karo.

### Lab B — DNS lookup

Windows/Linux/macOS (availability varies):

```bash
nslookup example.com
```

Or:

```bash
dig example.com A
 dig example.com AAAA
 dig example.com MX
```

`dig` command mein leading space copy na karna; commands separate execute karna.

Observe: resolver response, record types, TTL and whether IPv4/IPv6 records exist.

### Lab C — Route path (best-effort view)

Windows:

```powershell
tracert example.com
```

Linux/macOS:

```bash
traceroute example.com
```

Some networks ICMP/TTL-expired replies block or deprioritize karte hain. Missing hop ka matlab necessarily Internet broken ya packet lost to destination nahi.

### Lab D — Router and DNS troubleshooting

1. Check device has IP config.
2. Ping local default gateway (some networks block ping).
3. Resolve a known domain.
4. Test a known HTTPS site.
5. Compare Wi-Fi vs mobile hotspot.
6. Note whether issue DNS, local Wi-Fi, ISP path or destination-specific lagta hai.

Only your own device/network or a lab you have permission to test. Do not scan or probe networks without authorization.

## 17. Self-check

1. MAC and IP address alag layers/roles kyun use karte hain?
2. IPv6 128-bit kyun hai?
3. `/24` prefix ka meaning kya hai?
4. DHCP DORA flow mein four stages kaunse hain?
5. NAT firewall kyun nahi hai?
6. Recursive resolver and authoritative DNS server ka difference?
7. DNSSEC and DoH ka purpose kaise different hai?
8. Root DNS server Internet traffic route kyun nahi karta?
9. BGP operators ke business policies se kaise affect hota hai?
10. CDN edge cache hit aur origin fetch mein difference kya hai?

## References

1. [RFC 8200 — IPv6 Specification](https://www.rfc-editor.org/rfc/rfc8200)
2. [RFC 1034 — DNS Concepts and Facilities](https://www.rfc-editor.org/rfc/rfc1034) and [RFC 1035 — DNS Implementation and Specification](https://www.rfc-editor.org/rfc/rfc1035)
3. [ICANN RSSAC FAQ — DNS and Networking](https://www.icann.org/en/rssac/faq)
4. [RFC 4271 — BGP-4](https://www.rfc-editor.org/rfc/rfc4271)
5. [Cloudflare — How the Internet Works](https://www.cloudflare.com/learning/network-layer/how-does-the-internet-work/)
6. [IANA — IPv4 Special-Purpose Address Registry](https://www.iana.org/assignments/iana-ipv4-special-registry/iana-ipv4-special-registry.xhtml)
7. [IANA — IPv6 Special-Purpose Address Registry](https://www.iana.org/assignments/iana-ipv6-special-registry/iana-ipv6-special-registry.xhtml)
8. [RFC 1918 — Address Allocation for Private Internets](https://www.rfc-editor.org/rfc/rfc1918)
9. [RFC 9116 — A File Format to Aid in Security Vulnerability Disclosure](https://www.rfc-editor.org/rfc/rfc9116) (useful later for security contact operations)

---

**Next:** 05C — Transport and Application Protocols: TCP, UDP, QUIC, HTTP, WebSockets and TLS.
