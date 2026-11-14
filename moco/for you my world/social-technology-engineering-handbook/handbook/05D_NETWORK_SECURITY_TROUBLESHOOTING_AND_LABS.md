# 05D — Network Security, Troubleshooting, Architecture Labs and Failure Cases

**Series:** Technology Foundations  
**Edition:** English 1.0  
**Purpose:** Learn not only how networks work, but how to operate and troubleshoot them safely. This chapter focuses on defensive understanding and authorised practice.

---

## 1. Chapter goal: understand a network and operate it safely

A network can be fast and still be insecure. A firewall can be present and still be misconfigured. A server can be reachable and still expose data to unauthorised users. Network engineering therefore combines connectivity, performance, security, observability and recovery.

This chapter covers threat modelling, firewalls, IDS/IPS, common network attacks, VPNs and zero-trust concepts, layer-by-layer troubleshooting, safe commands, a home lab, architecture examples across industries and a sample outage investigation.

**Permission rule:** Perform scanning, packet capture, vulnerability testing and configuration changes only on systems you own or have explicit authorisation to test. Do not test public targets merely because they are reachable.

## 2. Threat model: what are you protecting?

A threat model starts with assets and trust boundaries, not with a list of fashionable security tools.

### Assets

- User accounts and credentials.
- Private messages, posts and media.
- Database and backup systems.
- API availability and service reputation.
- Payment and business records.
- Administrative interfaces and secrets.
- Network infrastructure and domain names.

### Threat actors

- Ordinary abusive users.
- Automated bots and credential-stuffing groups.
- Criminal attackers.
- Compromised vendors or suppliers.
- Malicious or careless insiders.
- Opportunistic attackers exploiting exposed systems.

### Entry points and trust boundaries

Map public web/mobile applications, APIs, admin tools, remote access, upload endpoints, webhooks, DNS, cloud control panels and third-party integrations. Mark where public traffic becomes trusted internal traffic, where user data enters a vendor and where administrators receive elevated access.

### Questions to ask

1. What can an attacker reach from the public Internet?
2. Which services are reachable only from a private network or VPN?
3. Which system authenticates the user or device?
4. Where is access authorised?
5. What data is exposed if one service is compromised?
6. How will suspicious traffic be detected?
7. How can service be isolated and recovered?

## 3. Firewall: network traffic policy enforcement

A firewall applies rules to network traffic. Rules may consider source/destination addresses, ports, protocols, connection state, application identity or other attributes, depending on the firewall type.

### Common firewall types

| Type | Typical role | Limitation to remember |
|---|---|---|
| Stateless packet filter | Allows/blocks packets using header fields | Limited connection/application context |
| Stateful firewall | Tracks connection state | State tables and rule design still require care |
| Next-generation firewall | Adds application/user/threat inspection features | More complex, encrypted traffic limits visibility |
| Web Application Firewall (WAF) | Filters HTTP requests using application-layer rules | Does not replace secure application code or authorisation |
| Host firewall | Controls traffic to/from an individual endpoint/server | Must be maintained on every relevant host |
| Cloud security group/network ACL | Controls cloud network reachability | Rules differ by provider and layer |

A default-deny approach can reduce exposure, but rules must allow necessary traffic and include monitoring. A firewall rule that is too broad may create more risk than expected.

## 4. IDS versus IPS

- **IDS (Intrusion Detection System):** Monitors activity and raises alerts about suspicious patterns.
- **IPS (Intrusion Prevention System):** Can actively block or disrupt traffic that matches configured detection rules.

Both may use signatures, protocol analysis, behaviour or anomaly detection. False positives can disrupt legitimate traffic. Detection systems need tuning, update processes, ownership and incident-response procedures.

A detection alert is not proof of a successful compromise. It is evidence that requires validation and investigation.

## 5. Common network-related threats

### A. Denial of Service and Distributed Denial of Service

A Denial-of-Service (DoS) attack tries to make a service unavailable. A Distributed DoS (DDoS) attack uses many sources or compromised systems to overwhelm a target or its upstream network.

Possible defensive measures:

- Provider-level DDoS mitigation and upstream coordination.
- Rate limits and request quotas.
- Connection and resource limits.
- Caching and CDN protection for suitable content.
- Traffic filtering and anomaly detection.
- Capacity planning and incident runbooks.

A CDN alone cannot guarantee protection for origin APIs, databases or all attack types. Exposing the origin directly may bypass some edge protection.

### B. Man-in-the-Middle (MitM)

A MitM attacker attempts to intercept or alter communication between parties. Risks increase on untrusted networks or when certificate validation is ignored.

Defences include correctly configured TLS, certificate validation, secure Wi-Fi, DNS/domain protection, device security and avoiding untrusted certificate installation. Do not disable TLS verification to make an error disappear.

### C. DNS spoofing and domain hijacking

An attacker may try to provide false DNS answers or gain control of a domain's DNS configuration or registrar account.

Defences:

- Protect registrar and DNS-provider accounts with MFA.
- Use role-based access and change approvals.
- Enable registrar locks where available.
- Monitor record and nameserver changes.
- Use DNSSEC where suitable and correctly managed.
- Maintain documented recovery and domain-expiry controls.

### D. IP/MAC spoofing and ARP/NDP abuse

An attacker may forge address information or manipulate local neighbour discovery. These attacks are most relevant in certain local-network and routing contexts; not every spoofed address automatically grants access.

Defences include switch protections where supported, network segmentation, secure Wi-Fi, correct neighbour-discovery configuration, ingress/egress filtering and application-layer authentication.

### E. Exposed ports and weak remote administration

A service exposed to the public Internet may be attacked through vulnerable software, weak credentials or incorrect configuration.

Defences:

- Expose only required services.
- Restrict management interfaces to trusted networks or approved access methods.
- Use MFA and strong key-based authentication where suitable.
- Patch services and remove unused software.
- Monitor successful and failed access.
- Avoid default credentials and unnecessary remote desktop exposure.

### F. BGP route leak or hijack

A network may accidentally or maliciously announce routes that affect how other networks reach a destination. Consequences can include traffic misdirection, outage or interception opportunities.

Defences include route filtering, prefix/origin validation, RPKI-based Route Origin Validation where deployed, monitoring and coordination with upstream providers. RPKI helps with origin validation but does not solve every BGP security problem.

### G. Rogue access point or evil twin

A fake Wi-Fi access point may imitate a trusted network name to attract users. Users may connect to the wrong network and expose traffic or credentials, especially when applications lack proper transport security.

Defences include enterprise Wi-Fi authentication, certificate validation, user awareness, disabling automatic connection to unknown networks and using trusted VPNs where appropriate. HTTPS remains important even on a VPN.

### H. Bot and credential abuse

Bots may automate sign-ups, scraping, login attempts, spam, credential stuffing and resource exhaustion.

Defences include rate limits, bot detection, abuse monitoring, MFA, breached-password checks where lawful, risk-based challenges, account recovery protection and clear appeal paths for mistakenly blocked users.

## 6. VPN versus proxy versus firewall versus zero trust

| Concept | Main purpose | What it does not automatically guarantee |
|---|---|---|
| VPN | Creates an encrypted tunnel between endpoints or networks | Does not make a compromised device safe or hide all activity from every party |
| Proxy | Makes requests on behalf of a client | Does not automatically encrypt the entire client-to-proxy path or provide identity security |
| Firewall | Applies network traffic policy | Does not fix insecure application logic |
| Zero-trust approach | Repeatedly evaluates identity, device and access context rather than trusting network location alone | Is not one product or a single firewall setting |

A VPN can protect traffic on an untrusted access network, but the VPN provider or corporate gateway may see metadata or traffic after the tunnel ends. A proxy may be used for caching, filtering, egress control or privacy, depending on design. Zero-trust architecture emphasises explicit, least-privilege access and continuous evaluation.

## 7. Network troubleshooting: diagnose layer by layer, not by guessing

Use a repeatable process:

1. **Clarify the symptom:** One device or all devices? One website or all services? Started when?
2. **Check physical/link state:** Cable, Wi-Fi association, signal, interface status and power.
3. **Check local IP configuration:** Address, prefix, gateway and DNS resolver.
4. **Check local gateway reachability:** This tests part of the local path, not the entire Internet.
5. **Check routing:** Does the system have a route to the destination?
6. **Check DNS:** Does the hostname resolve to an expected address?
7. **Check transport:** Can the client establish the required TCP/UDP path?
8. **Check TLS:** Is certificate validation and handshake successful?
9. **Check application:** What do HTTP status, application logs and backend dependencies show?
10. **Compare:** Another device, another authorised network or another region may help isolate the scope.
11. **Record evidence:** Time, commands, outputs, recent changes and affected services.

### Symptom-to-cause guide

| Symptom | Possible causes to investigate |
|---|---|
| No network connection | Power, cable, Wi-Fi authentication, interface or router failure |
| Local devices work; Internet does not | ISP access, gateway route, upstream outage or DNS issue |
| IP address works; domain name fails | DNS configuration/resolver issue |
| Some websites work; one application fails | Application outage, TLS, firewall, routing or provider issue |
| Slow downloads | Congestion, Wi-Fi interference, server capacity, packet loss or storage bottleneck |
| Video call stutters | Jitter, packet loss, CPU load, Wi-Fi congestion or relay path |
| TLS certificate warning | Wrong hostname, expiry, trust chain, clock issue or interception; do not ignore it |
| API returns 5xx | Backend, upstream dependency, load balancer, timeout or deployment issue |

A single ping failure is not proof that a server is down. Some hosts block ICMP while their Web service remains available.

## 8. Useful tools and safe commands

Use diagnostic commands on your own device and networks you are authorised to inspect.

### Windows

```powershell
ipconfig /all
route print
nslookup example.com
tracert example.com
Test-NetConnection example.com -Port 443
```

### Linux

```bash
ip address
ip route
resolvectl status
getent hosts example.com
traceroute example.com
ss -tulpn
```

Some commands may require installed packages or elevated privileges. Avoid changing firewall or interface settings until you understand the effect.

### macOS

```bash
ifconfig
netstat -rn
scutil --dns
dig example.com
traceroute example.com
lsof -i -P
```

### What each tool tells you

| Tool | Typical use | Important limitation |
|---|---|---|
| `ipconfig` / `ip` / `ifconfig` | Interface and address configuration | Does not prove remote service health |
| `route` | Routing table | Route presence does not prove the path works |
| `nslookup` / `dig` | DNS lookup | Resolver answers may be cached or policy-filtered |
| `ping` | Basic reachability/round-trip observation | ICMP may be blocked or deprioritised |
| `traceroute` / `tracert` | Path clues | Routers may not respond; path may be asymmetric |
| `ss` / `netstat` / `lsof` | Local sockets and listeners | Output visibility depends on permissions and OS |
| `curl` | HTTP/API request inspection | Use only approved endpoints and protect tokens |
| Wireshark | Packet capture and analysis | Captures can expose personal data and credentials |

## 9. Build a safe home networking lab

### Suggested setup

- A home router you own or administer.
- One laptop or desktop.
- A virtual machine if you want a separate test environment.
- Wireshark installed from its official source.
- A local test web server.
- Documentation-only IP ranges for diagrams.

Do not scan your ISP, school, neighbour's Wi-Fi or public infrastructure without explicit permission.

### Lab 1 — Observe the local network

1. Record your device's local IP address, prefix and default gateway.
2. View the routing table.
3. Identify whether the device is using Ethernet or Wi-Fi.
4. Compare with another device on your own network.
5. Do not publish public IPs or sensitive network details in a public issue.

### Lab 2 — DNS observation

```bash
dig example.com A
dig example.com AAAA
dig example.com MX
```

Compare record types and note TTL values. Do not attempt cache poisoning or unauthorized DNS changes.

### Lab 3 — HTTP and TLS observation

```bash
curl -I https://example.com
```

Then inspect the certificate for a domain you are authorised to test. Record the issuer, subject names and validity period. Do not bypass certificate warnings.

### Lab 4 — Create a local web server

On a computer you control, run a simple local server:

```bash
python -m http.server 8000 --bind 127.0.0.1
```

Open `http://127.0.0.1:8000` on the same device. Binding to loopback keeps the example local. Stop the server with Ctrl+C when finished. Do not expose the server to a public network unless you understand and intentionally configure the security boundary.

### Lab 5 — Wireshark

Capture only your own lab traffic. Start with a DNS query to a test domain and observe the packet layers. Use display filters such as `dns` or `tcp`. Do not capture other people's traffic or share captures containing personal data, cookies or tokens.

## 10. Network architecture examples across industries

### A. Small SaaS startup

A typical design may include a CDN/WAF, load balancer, application servers in private subnets, managed database, object storage and restricted administrative access. Monitoring and backups should be designed before public launch.

### B. Bank or fintech

A financial service may need strong network segmentation, privileged-access controls, HSMs, fraud systems, audit logging, redundancy and strict regulatory/vendor review. Exact obligations vary by jurisdiction and licence.

### C. Multiplayer game

Game architecture may use regional game servers, matchmaking, real-time transport, DDoS protection, telemetry, anti-cheat systems and separate account/payment services. Low latency is important, but cheating and account abuse also matter.

### D. Industrial/IoT environment

Industrial systems may separate operational technology (OT) from office IT, use controlled gateways, asset inventories, protocol-aware monitoring and carefully tested patch windows. Safety and uptime can be more important than rapid feature changes.

## 11. Network-design principles for a product team

- Expose the smallest possible public attack surface.
- Separate public, application, data and management networks where justified.
- Avoid directly exposing databases to the public Internet.
- Use TLS for data in transit.
- Apply least privilege to service-to-service traffic.
- Monitor DNS, certificates, routing, latency and packet loss.
- Rate-limit and protect critical APIs.
- Plan for provider and region outages.
- Document ports, dependencies, owners and change history.
- Test network changes in staging or controlled environments.

## 12. Security mistakes beginners make

- Assuming NAT is a firewall or complete security control.
- Exposing database and admin ports publicly.
- Reusing passwords or sharing private keys.
- Ignoring TLS certificate errors.
- Trusting an IP address as proof of user identity.
- Capturing traffic without permission.
- Allowing broad firewall rules “temporarily” and forgetting them.
- Ignoring DNS registrar protection.
- Logging tokens or private data.
- Assuming that a service is safe because it is hidden behind a VPN.

## 13. Mini incident scenario: API suddenly unavailable worldwide

Imagine users across several countries report that an API is unreachable.

A disciplined response:

1. Confirm the scope using monitoring from multiple regions.
2. Check DNS resolution and recent DNS changes.
3. Check certificate validity and TLS handshake errors.
4. Check CDN, load balancer and origin health.
5. Review provider status pages and upstream network incidents.
6. Compare network paths and BGP reachability information where available.
7. Check deployment history, firewall changes and capacity metrics.
8. Mitigate safely—rollback a bad release, restore a known-good route/configuration or use a documented failover.
9. Communicate impact and status accurately.
10. Preserve logs, timeline and evidence; write a post-incident review.

Do not assume a global API outage is a DDoS attack without evidence. It could be DNS, certificate expiry, bad deployment, cloud outage, routing incident, expired secret or overloaded dependency.

## 14. Network-security learning path

1. Learn IP addressing, subnetting and routing.
2. Understand DNS, TCP, UDP, HTTP and TLS.
3. Learn firewall rules and network segmentation.
4. Study threat modelling and logging.
5. Build a safe local lab with virtual machines.
6. Learn Wireshark and packet analysis using your own traffic.
7. Study defensive monitoring and incident response.
8. Practise authorised security testing in deliberately vulnerable labs.
9. Document findings and remediation, not just exploit demonstrations.

## 15. Final self-check

1. What does a firewall do, and what can it not fix?
2. How are IDS and IPS different?
3. Why is DDoS mitigation often needed upstream?
4. How can a domain registrar compromise affect an application?
5. Why should a VPN not be treated as a complete security solution?
6. What is the difference between a route problem and an application problem?
7. Which commands would you use to inspect IP, DNS and routing on your operating system?
8. Why should packet capture be restricted to authorised traffic?
9. What should happen during a global API outage?
10. Which network controls would you design for a small SaaS product?

## 16. Part 05 complete — recap

You have now studied network fundamentals, IP addressing, DNS, routing, transport protocols, HTTP, TLS, network security and troubleshooting. You should be able to describe how a device reaches an application, identify likely failure layers and practise safely in a lab you control.

**Next:** Part 06 — Web and Frontend Engineering. It explains how browsers request resources, render pages and run application code, and how HTML, CSS, JavaScript, TypeScript and frontend frameworks fit together.

---

## References and further study

1. [NIST — Cybersecurity Framework](https://www.nist.gov/cyberframework)
2. [NIST SP 800-41 Rev. 1 — Guidelines on Firewalls and Firewall Policy](https://csrc.nist.gov/pubs/sp/800/41/r1/final)
3. [CISA — DDoS guidance and resources](https://www.cisa.gov/)
4. [OWASP — Web Security Testing Guide](https://owasp.org/www-project-web-security-testing-guide/)
5. [RFC 2827 / BCP 38 — Network Ingress Filtering](https://www.rfc-editor.org/rfc/rfc2827)
6. [RFC 7454 — BGP Operations and Security](https://www.rfc-editor.org/rfc/rfc7454)
7. [MANRS — Mutually Agreed Norms for Routing Security](https://www.manrs.org/)
8. [Wireshark Documentation](https://www.wireshark.org/docs/)
9. [Microsoft Learn — Windows networking commands](https://learn.microsoft.com/windows-server/administration/windows-commands/windows-commands)
10. [Linux man-pages project](https://man7.org/linux/man-pages/)

*Security note:* Examples are for education and defensive operations. Testing systems without permission can violate laws, provider terms and other people's privacy.
