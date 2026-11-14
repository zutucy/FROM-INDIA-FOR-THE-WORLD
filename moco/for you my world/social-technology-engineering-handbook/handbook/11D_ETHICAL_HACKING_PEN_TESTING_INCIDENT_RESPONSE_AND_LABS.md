# 11D — Ethical hacking, penetration testing, incident response and safe labs

## 1. What makes hacking ethical?

Ethical hacking is authorized testing performed under a documented scope, purpose, rules of engagement and data-handling process. Calling an activity “learning” or “research” does not grant permission. Written authorization should specify assets, dates, permitted techniques, prohibited actions, rate limits, emergency contact, evidence handling and stop conditions.

A vulnerability scan identifies possible weaknesses. A penetration test safely validates selected weaknesses and business impact within scope. A code review examines implementation. A red-team exercise evaluates detection and response. A bug bounty accepts reports under published rules. These activities overlap but are not interchangeable.

## 2. Responsible testing lifecycle

1. **Pre-engagement:** Confirm ownership/authorization, scope, dates, contacts and legal constraints.
2. **Reconnaissance:** Collect permitted information about in-scope assets.
3. **Enumeration:** Identify exposed services and application behaviour within limits.
4. **Validation:** Test candidate issues safely, minimizing impact.
5. **Impact:** Demonstrate the smallest proof needed; do not collect unnecessary user data.
6. **Cleanup:** Remove test artifacts and restore modified state.
7. **Report:** Explain issue, preconditions, impact, safe reproduction, root cause and remediation.
8. **Retest:** Verify the fix and check for regression.

A good report helps developers reproduce and fix the problem. Redact secrets and personal data from evidence.

## 3. Common attacker paths from a defender's perspective

- Credential theft via phishing/password reuse: phishing-resistant MFA, safe recovery, session monitoring.
- Authorization abuse: object-level checks, deny-by-default rules and negative tests.
- Injection: parameterized operations and safe output encoding.
- Supply-chain compromise: dependency hygiene, provenance and scoped CI credentials.
- Cloud exposure: least-privilege IAM, private storage, configuration monitoring.
- Ransomware: identity hardening, network segmentation, protected backups and restore drills.
- Denial of service: edge protection, quotas, caching, backpressure and provider coordination.

MITRE ATT&CK can help defenders map observations to adversary goals and improve detection coverage. It is a knowledge base, not a certification checklist or a complete description of every threat.

## 4. Incident response before an incident

Prepare named incident commander and backup; security, engineering, privacy/legal, support and communications contacts; severity levels; cloud/vendor emergency contacts; evidence-retention procedure; backup/restore runbooks; key-revocation steps; notification decision process; communication templates and tabletop exercises.

### Response lifecycle

**Prepare → Detect/Analyse → Contain → Eradicate → Recover → Learn.**

- Detect: correlate alerts, user reports and system anomalies.
- Analyse: establish timeline, scope, affected assets/accounts/data and uncertainty.
- Contain: revoke compromised sessions/keys, isolate components or disable vulnerable workflows.
- Eradicate: remove persistence, patch root cause and rebuild compromised infrastructure where appropriate.
- Recover: restore trusted systems, rotate secrets, verify integrity and monitor.
- Learn: record root cause, controls that failed, decisions and tracked remediation.

Preserve relevant evidence before wiping systems when forensic review may be needed. Keep investigation data limited and access-controlled.

## 5. Breach response across countries

A breach may trigger different duties under law, contracts and sector rules. Notification deadlines, thresholds, authorities and content vary. Do not copy one country's deadline into a global plan. Determine affected individuals, jurisdictions, data types, controller/processor roles, vendors and applicable regimes. Consult qualified privacy counsel promptly while containment continues.

Record when detected, what is known, what remains uncertain, affected data, containment, risk assessment, decisions, notifications, evidence, remediation and closure. Avoid speculative public claims.

## 6. Ransomware and recovery

Backups should be separated from ordinary production credentials, protected from deletion/tampering and restored in a clean environment. A backup never restored is only an assumption.

Test restoration of databases and objects; recovery of keys/configuration; clean infrastructure rebuild; domain/account recovery; artifact/dependency availability; integrity checks; user communication and support surge. Define RTO (recovery time target) and RPO (tolerated data-loss window) per service and cost the design.

## 7. Safe labs

Use OWASP Juice Shop or WebGoat locally, intentionally vulnerable VMs in an isolated network, your own test API, or CTF platforms that explicitly permit the activity. Use snapshots, disposable credentials and synthetic data. Do not expose vulnerable labs publicly. Never use one lab as a bridge to scan adjacent systems.

## 8. Exercise: simulated account takeover

Scenario: unusual device login, followed by email change and bulk export.

1. Define evidence needed to verify the alert.
2. Revoke sessions and reset credentials in your local demo.
3. Check whether MFA or account recovery was bypassed.
4. Identify data accessed using audit events without dumping message bodies.
5. Preserve evidence and estimate scope.
6. Identify jurisdictions and notification decision owners.
7. Draft a cautious user update.
8. Add regression tests and controls.

The lesson: incident response is identity, data, logging, engineering, support, legal judgement and communication—not only patching.

## 9. When professionals are needed

Engage qualified security specialists for production penetration testing, cryptographic design, incident forensics, cloud reviews and regulated/high-risk systems. Verify credentials, scope, insurance, confidentiality and evidence handling. A scanner or AI-generated report does not replace skilled review.

## Sources

- NIST incident handling guidance: https://csrc.nist.gov/pubs/sp/800/61/r2/final
- NIST CSF 2.0: https://www.nist.gov/cyberframework
- MITRE ATT&CK: https://attack.mitre.org/
- OWASP Juice Shop: https://owasp.org/www-project-juice-shop/
- OWASP WebGoat: https://owasp.org/www-project-webgoat/
- NIST NICE Framework: https://www.nist.gov/itl/applied-cybersecurity/nice/nice-framework-resource-center
