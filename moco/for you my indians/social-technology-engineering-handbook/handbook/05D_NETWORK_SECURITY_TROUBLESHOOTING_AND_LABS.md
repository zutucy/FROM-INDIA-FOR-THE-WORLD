# 05D — Network Security, Troubleshooting, Architecture Labs and Failure Cases

**Part:** 05 — Networking and Internet Protocols  
**Language:** Detailed Hinglish  
**Research snapshot:** 13 November 2026

---

## 1. Goal: network ko samajhna hi nahi, safely operate bhi karna

Network security ka purpose sirf firewall install karna nahi. Real environment mein identity, device health, segmentation, encryption, routing, DNS integrity, monitoring, incident response and recovery ek saath kaam karte hain.

Is chapter mein:

- Common network attacks ko defensive perspective se samjhenge.
- Firewall, WAF, IDS, IPS, VPN, zero-trust and segmentation.
- DDoS, spoofing, DNS hijack, route leak and man-in-the-middle risks.
- Troubleshooting methodology.
- Safe home lab with virtual networks.
- Web product, office, cloud and global company network examples.

All practical work sirf apne devices, apne lab, or explicit written permission wale networks par karo. Random public IPs/domains scan, exploit ya overload mat karo.

## 2. Threat model: kis cheez ko protect karna hai?

Network security start karne se pehle threat model banao:

1. **Assets:** user data, admin panels, API keys, payment systems, servers, internal network, backups.
2. **Threat actors:** cybercriminals, bot operators, malicious insiders, compromised vendors, opportunistic scanners, state-linked actors (context dependent).
3. **Entry points:** public website, API, VPN, email, employee laptops, cloud console, exposed storage, remote administration.
4. **Trust boundaries:** public Internet ↔ CDN/WAF ↔ application ↔ database ↔ admin network.
5. **Impact:** data theft, account takeover, service outage, fraud, data tampering, reputational/legal consequences.
6. **Controls:** preventive, detective, responsive and recovery measures.

Threat model regularly update karo. Naya API endpoint, vendor, mobile app, admin tool, region or data category naya risk add kar sakta hai.

## 3. Firewall: network traffic policy enforcement

Firewall rules decide karte hain kaunsa traffic allow, deny or inspect hoga. Firewalls network layer, transport layer, application layer or cloud control plane par operate kar sakte hain.

### Common firewall types

- **Packet-filtering firewall:** IPs, protocol, ports and basic packet fields ke basis par filtering.
- **Stateful firewall:** Connection state track karke traffic decisions.
- **Next-generation firewall:** Deeper application inspection, identity, threat prevention etc.; actual capabilities vendor-specific.
- **Host firewall:** Individual server/laptop par traffic rules.
- **Cloud security groups / network ACLs:** Cloud network interfaces/subnets par policy controls.
- **Web Application Firewall (WAF):** HTTP request patterns and application-layer attacks ko filter karne mein help.

Firewall is not enough by itself. Allowed HTTPS traffic bhi malicious request carry kar sakta hai. Application authorization, secure code, endpoint protection, logging and monitoring needed hain.

## 4. IDS vs IPS

- **IDS (Intrusion Detection System):** Suspicious patterns/events detect karke alert generate karta hai.
- **IPS (Intrusion Prevention System):** Inline or active enforcement ke through selected malicious traffic block kar sakta hai.

False positives and false negatives dono possible hain. Rules/models tune karne honge; alert ka context and response procedure hona chahiye.

Network Detection and Response (NDR) tools traffic metadata/telemetry se suspicious activity identify kar sakte hain. Encrypted traffic mein payload visibility limited ho sakti hai; endpoint/server logs and identity events combine karna important hai.

## 5. Common network-related threats

### A. Denial of Service and Distributed DoS

**DoS** service availability degrade karne ka attempt. **DDoS** multiple distributed sources se traffic/requests generate karta hai.

Attack categories:
- Volumetric: bandwidth/link capacity consume.
- Protocol/state exhaustion: network or connection state resources consume.
- Application-layer: expensive HTTP/API actions repeatedly invoke.

Defenses:
- CDN/Anycast and upstream DDoS mitigation.
- Rate limiting and request budgets.
- WAF/bot management with careful tuning.
- Queue protection and concurrency limits.
- Capacity planning and graceful degradation.
- Provider/ISP escalation contacts and runbooks.

A simple rate limit alone large volumetric DDoS stop nahi karega; mitigation often upstream network providers/edge services ki need rakhta hai.

### B. Man-in-the-Middle (MitM)

Attacker two endpoints ke beech communication observe or modify karne ki position mein aa sakta hai. Risks include rogue Wi-Fi, compromised router, malicious proxy or certificate trust compromise.

Defenses:
- HTTPS with correct certificate validation.
- TLS settings and HSTS.
- Secure DNS and device posture where appropriate.
- Avoid ignoring certificate warnings.
- VPN on untrusted networks may protect a segment to VPN gateway, but it does not make destination/application automatically trustworthy.
- Endpoint malware protection and patching.

### C. DNS spoofing/domain hijack

Attacker forged DNS data, resolver compromise or registrar account takeover se user ko wrong endpoint par direct karne ki koshish kar sakta hai.

Defenses:
- Registrar MFA, account recovery protection, registry lock where appropriate.
- Least privilege DNS access.
- DNSSEC where supported and correctly maintained.
- DNS change alerts.
- Certificate monitoring and strong TLS validation.
- Domain renewal and ownership controls.

### D. IP/MAC spoofing and ARP/NDP abuse

Spoofing ka matlab network identity fields ko fake/impersonate karna. Local LAN mein ARP/NDP trust weaknesses misuse ho sakte hain. Attackers traffic redirect or disrupt karne ki koshish kar sakte hain.

Defenses depend on network:
- Switch protections such as DHCP snooping, Dynamic ARP Inspection and port security where supported/configured.
- Wi-Fi WPA2-AES/WPA3 with strong credentials.
- Network segmentation.
- IPv6 RA Guard and appropriate NDP protections where supported.
- TLS end-to-end where possible.

### E. Port exposure and weak remote administration

Admin ports public Internet par accidentally expose ho sakte hain. Weak passwords, stale software and missing MFA compromise risk badhate hain.

Defenses:
- Public exposure minimum.
- Admin access through VPN/zero-trust access gateway or managed secure channel.
- SSH keys and MFA where appropriate.
- Disable unused services.
- Patch OS/network device firmware.
- Restrict source identities and log admin actions.
- Rotate credentials/secrets after suspected compromise.

### F. BGP route leak/hijack

Incorrect or malicious BGP announcements traffic ko unintended path ki taraf divert/blackhole kar sakte hain. TLS still protects data confidentiality to a degree, but availability and metadata/route integrity concerns remain.

Defenses:
- Route origin validation using RPKI/ROV.
- Prefix/AS-path filtering and max-prefix limits.
- Route monitoring and alerting.
- Documented upstream-provider escalation process.
- Multi-provider resilience only if routing design is actually independent.

### G. Rogue access point / evil twin

Attacker legitimate Wi-Fi network jaisa SSID create karke users ko connect karne ki koshish kar sakta hai. HTTPS certificate validation important protection hai, but phishing, captive portal tricks and endpoint compromise remain possible.

Defenses: verified Wi-Fi, WPA3/WPA2 enterprise where suitable, certificate validation, managed devices, VPN/zero-trust policies and user awareness.

### H. Bot and credential abuse

Automated clients login/password reset/search/like/post endpoints abuse kar sakte hain.

Controls:
- Account- and IP-aware rate limits.
- Device/session risk signals with privacy safeguards.
- MFA/passkeys where feasible.
- Credential stuffing detection.
- CAPTCHA or risk challenges selectively, not as the only control.
- Abuse reporting and anomaly detection.
- Secure password reset and session revocation.

## 6. VPN vs proxy vs firewall vs zero-trust

| Technology | Primary purpose | What it does not guarantee |
|---|---|---|
| VPN | Encrypted tunnel between device/network and VPN gateway | Destination safety, anonymity from every party, or malware protection |
| Proxy | Intermediary for selected application traffic | Encryption/security unless separately configured |
| Firewall | Traffic policy enforcement | Correct application-level authorization |
| WAF | HTTP/application request filtering | Complete business logic security |
| IDS | Detect suspicious activity | Automatic blocking in every deployment |
| IPS | Detect and actively block selected traffic | Zero false positives or complete prevention |
| Zero Trust | Identity/context-based access, continuous policy evaluation | A single product or magic perimeter removal |

Zero Trust architecture generally starts from explicit verification, least privilege and assuming network location alone is not enough to trust a request. Device health, user identity, workload identity and policy context may matter.

## 7. Network troubleshooting: guess nahi, layer-by-layer diagnose karo

Ek disciplined order follow karo:

1. **Physical/link:** cable connected? Wi-Fi associated? signal/interference?
2. **Local config:** IP, prefix, gateway, DNS config received?
3. **Local network:** gateway reachable? VLAN/Wi-Fi isolation policy?
4. **Routing:** route table and next hop correct?
5. **DNS:** hostname resolve ho raha hai?
6. **Transport:** target port/service reachable?
7. **TLS:** certificate and handshake correct?
8. **Application:** HTTP status, authentication, authorization, server logs?
9. **Performance:** latency, loss, jitter, throughput, queueing?
10. **External dependency:** ISP, cloud provider, CDN, DNS provider, payment/email vendor?

### Symptom-to-cause guide

| Symptom | Possible causes | First checks |
|---|---|---|
| No network on one device | Wi-Fi, adapter, DHCP, local firewall | Link, IP config, gateway |
| All devices fail | Router, ISP, power, upstream outage | Router status, ISP incident |
| IP works, domain fails | DNS configuration or resolver | `nslookup` / `dig` |
| Website opens on mobile data only | Local ISP/DNS/routing/filter | Compare DNS, path and provider |
| Some sites work, one does not | Destination DNS/TLS/CDN/origin issue | Resolve record, cert, HTTP status |
| HTTPS certificate warning | Expired/wrong cert, wrong clock, interception | Check system clock and certificate chain; do not bypass warning casually |
| Slow file download | Server, CDN, congestion, Wi-Fi, TCP/QUIC | Throughput, route, packet loss, cache status |
| Video call choppy | Jitter, packet loss, low uplink, CPU load | Call stats, Wi-Fi, network congestion |
| API returns 429 | Rate limit or abuse control | Retry policy, quota headers, request rate |
| API returns 502/504 | Proxy/upstream timeout or unhealthy service | Gateway logs, upstream health, traces |

## 8. Useful tools and safe commands

### Windows

```powershell
ipconfig /all
route print
nslookup example.com
ping 1.1.1.1
tracert example.com
Test-NetConnection example.com -Port 443
```

### Linux

```bash
ip address
ip route
resolvectl status
getent hosts example.com
ping -c 4 1.1.1.1
traceroute example.com
ss -tulpn
curl -I https://example.com
```

### macOS

```bash
ifconfig
netstat -rn
scutil --dns
nslookup example.com
ping -c 4 1.1.1.1
traceroute example.com
```

Command availability and permissions vary by OS. Some commands require admin/root; do not use elevated privilege unless you understand why.

### What each tool tells you

- `ipconfig` / `ip address`: interface configuration.
- `route print` / `ip route`: routing table.
- `nslookup` / `dig` / `getent`: DNS resolution.
- `ping`: ICMP reachability/round-trip estimate; blocked ping does not prove host down.
- `tracert` / `traceroute`: attempts to reveal hop-by-hop path; filtering can hide hops.
- `Test-NetConnection`: basic connectivity check to host/port in Windows.
- `ss`: local socket/listening port state on Linux.
- `curl -I`: HTTP response headers/status.
- Wireshark: packet capture and protocol analysis on authorized traffic.

## 9. Build a safe home networking lab

### Suggested setup

- One laptop/desktop you own.
- Home router you administer.
- Optional second test device.
- Virtual machine (VM) with Linux.
- Virtual network configured as NAT or host-only in virtualization software.
- Wireshark for analysis.

### Lab 1 — Observe local network

1. Run IP configuration command.
2. Write down local IP, prefix, gateway and DNS server.
3. Open router admin dashboard only if you own/administer it.
4. Compare assigned address before/after reconnect.
5. Explain DHCP lease in your notes.

### Lab 2 — DNS observation

1. Resolve `example.com` using default resolver.
2. Query A, AAAA and MX records.
3. Compare results from another trusted resolver if you understand privacy implications.
4. Observe TTL values.
5. Explain why two resolvers may return different CDN edge addresses based on location, routing or policy.

### Lab 3 — HTTP and TLS observation

1. Run `curl -I https://example.com`.
2. Open browser Network tab.
3. Identify protocol version, status, response headers and timing.
4. Inspect certificate details in browser UI.
5. Explain why HTTPS payload is not readable in ordinary packet capture.

### Lab 4 — Make a local web server

Use a local development server bound to loopback or private lab interface, not an exposed public interface. Open it only from your own device or isolated lab. Learn:

- Listening port.
- Host firewall behaviour.
- `localhost` vs `0.0.0.0` bind.
- Private IP reachability.
- Why public exposure needs authentication, TLS, patching and a threat model.

### Lab 5 — Wireshark

Capture only your own test traffic. Use display filters from Wireshark documentation to study DNS, TCP handshake, TLS metadata and retransmission indicators. Do not decrypt or intercept other people's communications. Do not collect credentials/session tokens. Never upload raw packet captures without sanitising sensitive metadata.

## 10. Network architecture examples across industries

### A. Small SaaS startup

- Browser/mobile clients.
- DNS provider.
- CDN/WAF.
- Load balancer/reverse proxy.
- API application instances.
- Private database subnet.
- Managed Redis and queue.
- Restricted admin access.
- Logs/metrics/traces and alerts.

Database should not be directly reachable from arbitrary public networks. Application service gets only required DB access. Secrets stay in secret manager/environment injection, not source code.

### B. Bank/fintech

- Strong segmentation between public channels, internal services, payment processing and data stores.
- Strong identity/MFA and privileged access management.
- Encryption and key management.
- Fraud detection and immutable/auditable transaction records.
- Resilient connectivity and tested disaster recovery.
- Vendor and regulator requirements vary by jurisdiction.

Network security alone cannot make a payment correct. Application-level idempotency, ledger integrity, authorisation and reconciliation are separate requirements.

### C. Multiplayer game

- Matchmaking/control APIs.
- Regional game servers.
- Low-latency routing and health-based placement.
- DDoS mitigation.
- State validation and anti-cheat controls.
- Telemetry and reconnect handling.

### D. Industrial/IoT environment

- Sensors and controllers.
- OT/IT network segmentation.
- Strict allowlists and monitored gateways.
- Asset inventory and patch strategy compatible with safety constraints.
- Remote access tightly controlled.

Safety-critical systems need specialist risk assessment; do not casually scan or update production control networks.

## 11. Network design principles for a product team

1. **Minimise public exposure:** Publicly reachable endpoints should be intentional.
2. **Segment trust zones:** User traffic, application services, databases, admin, backups and management plane should not all share unrestricted connectivity.
3. **Encrypt in transit:** Public and sensitive internal links should use appropriate authenticated encryption.
4. **Authenticate both users and services:** Service-to-service identity matters in distributed architectures.
5. **Least privilege:** Every workload only gets required network access.
6. **Resilience:** Multiple zones/paths only help if failures are independent and tested.
7. **Observe:** Logs, metrics, traces, network flow telemetry and provider status should be correlated.
8. **Control cost:** Egress, CDN requests, inter-region transfer and NAT gateways can create unexpected bills.
9. **Plan DNS and certificates:** Renewal, ownership and rollback must be operationally owned.
10. **Practice recovery:** Restore, failover and incident playbooks must be tested.

## 12. Security mistakes beginners make

- Thinking NAT = firewall.
- Exposing database ports to the whole Internet.
- Putting API keys/private keys in GitHub.
- Disabling TLS certificate validation to “fix” a warning.
- Leaving default router/admin passwords.
- Assuming private IP means trusted.
- Trusting client-supplied user ID or role.
- Logging passwords, access tokens or sensitive payloads.
- Opening all inbound ports because “the app is not working.”
- Treating a successful ping as proof that HTTPS/API is healthy.
- Assuming one cloud region or one backup copy is disaster recovery.
- Running scans or stress tests on third-party systems without written authorisation.

## 13. Mini incident scenario: API suddenly unavailable worldwide

Suppose a global product starts returning errors in multiple countries.

**Do not immediately redeploy random code.**

1. Check incident scope and start time.
2. Check service health from multiple regions/networks.
3. Check DNS record changes and resolver answers.
4. Check CDN/WAF/load balancer and certificate status.
5. Check cloud provider status and recent infrastructure changes.
6. Check route/ISP incident notices if symptoms are regional.
7. Check origin API, database connections and queue health.
8. Apply documented mitigation or rollback.
9. Communicate status with accurate impact/updates.
10. Preserve logs and timeline.
11. After recovery, write blameless post-incident review: cause, impact, detection, response, corrective actions and owners.

**Important:** Incident response mein evidence preserve karo. Logs ko overwrite/delete karke problem hide karne ki koshish nahi karni.

## 14. Network security learning path

- Learn IP/subnets/DNS before scanning tools.
- Learn HTTP/TLS before proxying web traffic.
- Learn Linux permissions and process networking.
- Read OWASP Web and API Security materials.
- Practise in intentionally vulnerable local labs or authorised training platforms.
- Study packet analysis on self-generated traffic.
- Write a threat model and firewall policy for a toy app.
- Learn incident response and recovery, not only detection tools.

Useful references:
- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [OWASP API Security Top 10](https://owasp.org/API-Security/)
- [NIST Cybersecurity Framework](https://www.nist.gov/cyberframework)
- [CISA Secure by Design](https://www.cisa.gov/securebydesign)

## 15. Final self-check

1. Firewall and WAF mein difference?
2. IDS and IPS mein difference?
3. Why cannot a VPN promise complete anonymity?
4. DDoS ke volumetric, protocol and application-layer forms kya hain?
5. DNS provider account compromise ka impact kya ho sakta hai?
6. RPKI BGP routing ke kis part ko improve karta hai, aur kya solve nahi karta?
7. Why is network segmentation useful?
8. Ping fail hone par kaunse alternative checks karoge?
9. Why must private APIs still enforce authorization?
10. Global outage incident mein evidence and timeline preserve karna kyun important hai?

## 16. Part 05 complete — recap

Ab tumne networking ke four layers of understanding cover kiye:

- **05A:** Networking foundations and history.
- **05B:** IP addressing, subnetting, DNS, routing and global networks.
- **05C:** TCP, UDP, QUIC, HTTP, TLS and realtime application protocols.
- **05D:** Security, troubleshooting, labs and real-world architecture.

Part 05 ka objective expert network engineer banana nahi tha. Objective tha itna strong mental model dena ki tum backend, cloud, security and distributed systems ke next chapters ko samajh sako.

---

**Next Part 06:** Web and frontend engineering — browser internals, HTML, CSS, JavaScript/TypeScript, rendering, state, accessibility, mobile apps and performance.
