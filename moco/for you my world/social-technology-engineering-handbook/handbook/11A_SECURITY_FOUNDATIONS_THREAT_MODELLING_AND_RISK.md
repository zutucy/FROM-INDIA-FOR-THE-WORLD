# 11A — Security foundations, threat modelling and risk

**Part 11: Cybersecurity, ethical hacking and application security**  
**Safety boundary:** Practice only on systems you own, intentionally vulnerable labs, or systems covered by explicit written authorization.

## 1. What cybersecurity means

Cybersecurity reduces the likelihood and impact of unauthorized access, misuse, disruption, alteration or destruction of information and systems. It is not a single tool, a one-time audit, or merely antivirus. It combines architecture, people, process, source code, configuration, monitoring, incident response and recovery.

Start with four questions: What are we protecting? From whom or what? Through which paths could harm occur? How will we detect, contain and recover? Assets include accounts, personal data, source code, payment records, signing keys, backups, business continuity and user safety. Threats include criminals, abusive insiders, careless mistakes, compromised vendors, automated bots, faulty updates and infrastructure failures.

Security is risk management, not a promise of perfect safety. The appropriate controls depend on data sensitivity, exposure, threat environment, business model and likely harm.

## 2. Security objectives

| Objective | Meaning | Example control |
|---|---|---|
| Confidentiality | Only permitted parties see data | Access control, encryption, private-by-default settings |
| Integrity | Data and state are not improperly changed | Authorization, transactions, signatures, audit trails |
| Availability | Authorized users can use the service | Redundancy, rate limits, DDoS protection, recovery |
| Authenticity | Identity or message origin can be trusted | MFA, signatures, verified sessions |
| Accountability | Relevant actions can be investigated | Protected, privacy-aware audit logs |
| Privacy | Personal data is handled appropriately | Minimization, purpose limits, retention, rights workflows |

These goals sometimes conflict. More telemetry may improve a model but increase privacy exposure. Logging everything can help investigations but create a secondary sensitive database. Rate limits reduce abuse but can affect people behind shared IP addresses. Make trade-offs explicit and test them.

## 3. Short history of security thinking

Early computing environments were smaller and often protected physically. Time-sharing, remote terminals, personal computers and the Internet expanded the number of people who could interact with systems. Malware, worms, password theft, network intrusion and web application vulnerabilities became everyday engineering risks.

The Morris worm of 1988 disrupted many networked Unix systems and helped demonstrate the need for coordinated incident handling; the CERT Coordination Center was established at Carnegie Mellon following the incident. As the public web grew, applications exposed authentication, sessions, input handling and databases to large and diverse audiences. Cloud services later distributed the trust boundary across identity providers, hosting vendors, analytics SDKs, payment systems, open-source packages and CI pipelines.

The lesson is not that technology steadily becomes safe. Each new capability creates new attack surfaces. Revisit the threat model whenever architecture, data, vendors, audience or geography changes.

## 4. Assets, actors, attack surfaces and trust boundaries

- **Asset:** Something valuable: password-reset tokens, private messages, payment data, domain registration, build signing keys or backups.
- **Threat actor/event:** An entity or event capable of causing harm: attacker, malicious insider, mistake, supplier compromise, hardware failure or natural disaster.
- **Attack surface:** All reachable entry points: website, API, mobile deep links, file uploads, admin panels, OAuth callbacks, support tools, CI, cloud control plane and third-party scripts.
- **Trust boundary:** A point where data/control moves between different trust levels: browser-to-API, API-to-worker, tenant-to-tenant, public upload-to-internal processor or app-to-vendor.

A file remains untrusted after it enters your own object storage. A queue message is not automatically trustworthy because it came from an internal broker. Every boundary needs validation, authentication, authorization and observability appropriate to the risk.

## 5. Threat modelling method

Threat modelling identifies what can go wrong before the team commits to a design. Repeat it when a feature or dependency changes.

1. Define the feature, roles, assets and scope.
2. Draw data flows: clients, APIs, databases, storage, workers, vendors and trust boundaries.
3. Identify required security properties.
4. Brainstorm threats. STRIDE is a useful checklist: Spoofing, Tampering, Repudiation, Information disclosure, Denial of service and Elevation of privilege.
5. Assess likelihood, impact, exposure, blast radius and existing controls.
6. Choose mitigations, preferably secure architecture/defaults rather than user instructions.
7. Record residual risk, owner and due date.
8. Turn each important threat into a test, alert, runbook or acceptance criterion.

STRIDE is a brainstorming taxonomy, not a numerical risk score or exhaustive list.

### Example: private photo upload

Flow: browser selects file → API checks user and issues a limited signed URL → private object storage receives bytes → isolated worker validates and transforms media → database stores metadata → API determines who may view → CDN delivers with authorization-aware access.

| STRIDE | Threat example | Defensive design |
|---|---|---|
| Spoofing | Stolen session used as owner | Secure sessions, MFA options, revocation |
| Tampering | User changes object key or metadata | Server-side ownership checks, signed requests, immutable IDs |
| Repudiation | User denies changing visibility | Scoped, protected audit event |
| Information disclosure | Private object is public | Private bucket, authorization-aware delivery, no predictable public URL |
| Denial of service | Repeated huge uploads exhaust capacity | Size limits, quotas, rate limits, async processing |
| Elevation of privilege | Media worker has database-owner rights | Least-privilege service identity |

A signed URL is a time-limited capability, not proof that the user should access the object. Decide whether content is public, private, shared or temporary. Cache rules must preserve that decision.

## 6. Risk assessment

A severity score helps prioritize technical issues but is not a complete business-risk assessment. A moderate flaw exposing all private profiles may be more urgent than a severe issue in an isolated test system with no real data.

Assess impact, exploitability, exposure, affected users, blast radius, known active exploitation, detectability, recoverability, regulatory/contractual consequences and existing compensating controls. Keep a risk register with scenario, asset, likelihood, impact, owner, decision, due date and residual risk.

## 7. Frameworks and what they do

- **NIST Cybersecurity Framework 2.0:** Organization-level outcomes grouped into Govern, Identify, Protect, Detect, Respond and Recover.
- **OWASP Top 10:2025:** Awareness categories for major web-application risks. Not a complete test plan or certification.
- **MITRE ATT&CK:** Knowledge base of adversary tactics and techniques based on observed behaviour; useful to plan detections and coverage.
- **NIST SSDF:** Secure software development practices integrated throughout a lifecycle.
- **CIS Controls/Benchmarks:** Prioritized safeguards and configuration guidance for relevant systems.

Reading a framework does not make a company “certified” against it. Frameworks, certifications and attestations are different things.

## 8. Least privilege and defense in depth

Least privilege means each person, service, job and vendor gets only the permissions required for its task, for the shortest practical time. Use deny-by-default authorization, scoped tokens, short-lived credentials where possible, separate environments, periodic access reviews and removal of unused accounts.

Defense in depth uses multiple independent controls. A private video might rely on app-level authorization, private storage, short-lived delivery tokens, encryption, audit events and monitoring. No single control should be treated as sufficient.

## 9. Make security requirements testable

Weak: “Make uploads secure.”  
Testable: “Reject unsupported or oversized files; verify actual file format rather than trusting filename/MIME supplied by the browser; hold uploads privately until validation and policy checks pass; process in a resource-limited worker; and make unauthorized retrieval fail.”

For each feature define authorized actors/actions, data classification, validation, abuse limits, logs/alerts, rollback, privacy impact, retention and security tests.

## 10. Exercise

For an app you own, draw components and mark every untrusted input. List threats for each trust boundary and write tests proving unauthorized actions fail. Do not scan public IPs or test third-party systems.

## Sources

- NIST CSF 2.0: https://www.nist.gov/cyberframework
- NIST CSF functions: https://www.nist.gov/cyberframework/faqs
- OWASP Top 10:2025: https://top10.owasp.org/2025/
- MITRE ATT&CK Enterprise: https://attack.mitre.org/matrices/enterprise/
- NIST SSDF SP 800-218: https://csrc.nist.gov/pubs/sp/800/218/final
- CISA Secure by Design: https://www.cisa.gov/securebydesign
