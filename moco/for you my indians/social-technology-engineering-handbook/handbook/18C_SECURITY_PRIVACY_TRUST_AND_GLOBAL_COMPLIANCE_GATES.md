# 18C — Security, Privacy, Trust and Global Compliance Gates

**Edition:** 13 November 2026  
**Prepared with:** ChatGPT (GPT-6)  
**Purpose:** Connect cybersecurity, privacy engineering, trust and safety, and country-specific legal review into launch gates. A policy document is not a security control; a security control is not automatically legal compliance.

## 1. Start with assets, actors and trust boundaries

List what must be protected:

- Identity credentials, sessions, recovery channels and MFA factors.
- Private profiles, posts, messages and uploaded media.
- Personal information, location data, device/security telemetry and support records.
- Moderation reports, evidence, reviewer notes and appeals.
- API keys, signing keys, database credentials, cloud roles and backup keys.
- Source code, build artefacts, CI/CD runners, dependencies and admin consoles.
- Availability, integrity and reputation of the service.

Actors include ordinary users, creators, moderators, support staff, admins, contractors, vendors, automated clients/bots, attackers and government/legal requestors. Do not assume every authenticated user is trustworthy.

### Core trust boundaries

1. Untrusted client → edge/API.
2. Public API → privileged internal service.
3. Application → database/cache/object storage.
4. Queue publisher → worker consumer.
5. User-facing systems → moderator/admin tools.
6. Production → development/test environments.
7. Company → vendors/subprocessors.
8. One country/region → another country/region.

For each boundary record allowed identities, data crossing, validation, authentication, authorization, encryption, logging, rate controls and failure response.

## 2. Threat modelling workflow

Use a repeatable process such as STRIDE as a brainstorming aid, not as a claim that every risk has been found.

1. Draw data-flow diagrams and trust boundaries.
2. Identify assets and security/privacy objectives.
3. List abuse cases and attacker capabilities.
4. Evaluate likelihood, impact, affected people and business consequences.
5. Select preventive, detective and recovery controls.
6. Assign an owner and due date.
7. Test the control and record evidence.
8. Revisit after major feature/vendor/market changes.

Example threats:

| Threat | Example | Primary control family |
|---|---|---|
| Spoofing | Stolen session impersonates a user | MFA, session binding/rotation, re-auth for sensitive actions |
| Tampering | Client changes `ownerId` on a request | Server-side ownership checks and schema allow-lists |
| Repudiation | Admin denies removing content | Append-only audit event with controlled access |
| Information disclosure | Private media served from a public URL | Private origin, authorisation-aware delivery, short-lived signed URL |
| Denial of service | Upload flood consumes bandwidth/worker capacity | Quotas, size limits, queue backpressure, edge controls |
| Elevation of privilege | Moderator can grant themselves admin | Role separation, approval, least privilege, audit |

## 3. Identity, sessions and access control

- Passwords: use a modern password-hashing function with a unique salt and parameters reviewed against current guidance. Never encrypt passwords for later recovery or store plaintext.
- Authentication: use secure, rate-limited login and recovery; add phishing-resistant MFA for privileged users where feasible.
- Sessions: rotate after authentication/privilege changes; expire idle and absolute sessions; revoke on logout, recovery and compromise; protect cookies with appropriate Secure, HttpOnly and SameSite attributes.
- Authorization: default deny. Check resource ownership, relationship, privacy state, blocks, account status and role on the server for every object/action.
- Admin access: separate admin identity/workflows; MFA; just-in-time or time-bound access; least privilege; audited break-glass procedure.
- Secrets: managed storage, unique per service/environment, rotation, no secrets in Git or client bundles.
- Service identity: authenticate workloads to databases, queues and storage; do not share one all-powerful credential.

## 4. Secure media and user-generated content

- Apply maximum size, count, duration and rate quotas before upload.
- Use generated object keys; never trust the user's filename as a storage path.
- Validate actual content type and file structure; do not rely on extension alone.
- Store uploads outside executable web roots and serve with safe content headers.
- Scan/transform files in isolated workers with limited privileges and resource caps.
- Prevent decompression bombs, parser abuse and excessive pixel/duration resource use.
- Keep original/private objects inaccessible by default; expose only approved derivatives.
- Make cache policy consistent with visibility. Purge or invalidate derived copies after deletion/permission changes where required.
- Keep content moderation state separate from upload completion state.

## 5. Privacy by design

For each data element ask:

1. What purpose requires it?
2. Is it necessary, or can it be omitted/coarsened?
3. What is the applicable legal basis and notice/consent requirement in each market?
4. Who can access it and why?
5. Which vendors receive it?
6. Where are primary data, replicas, logs, support tools and backups located?
7. How long is it retained and how is it deleted?
8. Can the user exercise applicable rights?
9. Could it reveal sensitive traits or enable profiling, manipulation or harm?
10. Is it used for advertising, analytics, recommendations or AI training? Is that use separately explained and controlled?

Do not silently repurpose private user content to train models. Define purpose, notice, lawful basis, opt-out/consent as applicable, vendor terms, retention, access control and deletion implications before any such use.

### Deletion is a distributed workflow

An account deletion request can affect primary records, media derivatives, search indexes, caches, analytics, vendor processors, replicas and backups. Define:

- Immediate account/session restrictions.
- Verification and fraud safeguards proportionate to risk.
- Dependency inventory and deletion jobs.
- Legal hold/mandatory retention exceptions reviewed by counsel.
- Backup expiry and restore/re-delete procedure.
- Completion evidence and user communication.
- What cannot be removed from already lawfully shared/third-party copies, stated accurately.

Do not claim instant deletion from every immutable backup if the architecture cannot guarantee it. Publish an accurate process and retention period.

## 6. Trust and safety controls

- Community rules written in plain language with concrete examples.
- Report, block, mute and appeal tools accessible from relevant screens.
- Risk-based review queues with severity and escalation.
- Human review for context-sensitive/high-impact decisions.
- Moderator access separation, reviewer training and wellbeing controls.
- Evidence minimisation, access logging and retention limits.
- Repeat-abuse and coordinated manipulation response.
- Child/teen protections designed for the actual age range and market.
- Copyright and impersonation notice workflows.
- Transparency reporting and policy version history where appropriate.

Security alerts and content reports are different operational queues. A compromised account, grooming allegation, copyright notice and spam report need different triage, evidence and escalation paths.

## 7. Incident response and evidence

Prepare a written plan before an incident:

1. Detect and declare with severity and incident commander.
2. Triage: scope, affected services/users/data, safety risk and legal notification triggers.
3. Contain: disable compromised credentials, isolate affected workloads or limit feature exposure.
4. Preserve evidence safely; maintain access logs and chain-of-custody where needed.
5. Eradicate root cause and recover using known-good artefacts/backups.
6. Verify security, integrity, data correctness and user-facing functions.
7. Notify regulators/users/partners when required, within applicable timelines and after legal review.
8. Complete a blameless post-incident review with actions, owners and dates.

Never promise a reporting timeline without knowing the applicable regime and incident facts. Some laws/regulators have strict clocks; others use different thresholds and definitions.

## 8. Global legal readiness matrix

There is no single worldwide “social media permission”. Applicability depends on entity, user location, targeting, service type, data, age group, scale, content and local law. Prepare a market dossier for every country or region where the product is established, marketed, accepts users or monitors behaviour.

| Market / framework examples | Engineering and operations questions | Official starting points |
|---|---|---|
| EU / EEA | GDPR lawful basis, data subject rights, DPIA where required, transfer mechanism; DSA intermediary/platform duties and risk obligations; AI Act duties by role/use case and phased dates | https://commission.europa.eu/law/law-topic/data-protection_en ; https://digital-strategy.ec.europa.eu/en/policies/digital-services-act-package ; https://artificial-intelligence-act.ec.europa.eu/ |
| UK | UK GDPR and Data Protection Act; Online Safety Act duties depending on service; international transfer rules; children's code where in scope | https://ico.org.uk/ ; https://www.ofcom.org.uk/online-safety/ |
| India | DPDP Act and Rules commencement; IT intermediary rules and service classification; CERT-In directions; consumer, child, copyright and tax requirements | https://www.meity.gov.in/data-protection-framework ; https://www.meity.gov.in/ ; https://www.cert-in.org.in/ |
| United States | Federal/state privacy laws, FTC consumer protection, COPPA if child-directed or actual knowledge triggers, sector/state biometric and breach laws, DMCA processes | https://www.ftc.gov/ ; https://www.copyright.gov/dmca/ ; https://oag.ca.gov/privacy |
| China | PIPL, Data Security Law, Cybersecurity Law, content/service licensing, algorithm and generative AI rules, cross-border transfer and localization assessment | https://www.npc.gov.cn/ ; https://www.cac.gov.cn/ |
| Brazil | LGPD, ANPD guidance, children's/adolescent protections and local consumer rules | https://www.gov.br/anpd/ |
| Japan | APPI, PPC guidance, cross-border transfer and user-notice requirements | https://www.ppc.go.jp/en/ |
| Canada | Federal PIPEDA plus provincial privacy rules, child/privacy and consumer protections | https://www.priv.gc.ca/ |
| Australia | Privacy Act and APPs, Online Safety Act/eSafety obligations, child safety and consumer law | https://www.oaic.gov.au/ ; https://www.esafety.gov.au/ |
| South Korea | PIPA, PIPC guidance and communications/platform rules | https://www.pipc.go.kr/eng/ |
| Singapore | PDPA, PDPC guidance and applicable online safety/content rules | https://www.pdpc.gov.sg/ |
| Indonesia | Personal Data Protection Law and electronic-system obligations; local registration/transfer requirements may apply | https://www.komdigi.go.id/ |
| South Africa | POPIA and Information Regulator guidance; child and direct-marketing rules | https://inforegulator.org.za/ |
| Mexico | Federal/state privacy rules and relevant regulator/consumer obligations; verify institutional changes before launch | https://www.diputados.gob.mx/ ; https://www.gob.mx/ |

This is a starter map, not a complete jurisdiction inventory or legal conclusion. A target market can have state/provincial, sectoral, advertising, telecom, election, consumer, accessibility, tax, sanctions/export-control and app-store obligations not shown here. Obtain local legal advice.

## 9. Example current-law timing note: India DPDP

The Digital Personal Data Protection Act, 2023 and DPDP Rules, 2025 use phased commencement. The Gazette notifications distinguish provisions effective on publication, provisions scheduled one year after publication and provisions scheduled eighteen months after publication. On the 13 November 2026 edition date, do not state that every substantive processing obligation is already in force. Re-check the Gazette, subsequent notifications and actual applicable provision before a launch decision. A future scheduled date is not permission to ignore readiness work now.

Official sources:
- MeitY Data Protection Framework: https://www.meity.gov.in/data-protection-framework
- DPDP Rules, 2025 Gazette PDF: https://www.meity.gov.in/static/uploads/2025/11/53450e6e5dc0bfa85ebd78686cadad39.pdf
- DPDP Act commencement notification: https://egazette.gov.in/WriteReadData/2025/267647.pdf

## 10. Launch gates

Do not launch a public service until owners sign off on:

- Threat model and security test findings.
- Role/permission matrix and admin MFA.
- Privacy/data inventory and retention/deletion map.
- Vendor/subprocessor list and contracts.
- Market-specific legal applicability review.
- Report/block/appeal and emergency escalation.
- Child-safety strategy where minors may access the product.
- Copyright complaint process.
- Incident response and notification decision tree.
- Backup, restore and disaster recovery test.

## References

- NIST CSF 2.0: https://www.nist.gov/cyberframework
- OWASP ASVS: https://owasp.org/www-project-application-security-verification-standard/
- OWASP Top 10: https://owasp.org/www-project-top-ten/
- NIST Privacy Framework: https://www.nist.gov/privacy-framework
- EDPB: https://www.edpb.europa.eu/
- CERT-In: https://www.cert-in.org.in/
