# 15B — European Union, EEA and United Kingdom: privacy and platform rules

**Status date: 13 November 2026.** Confirm official consolidated texts, national guidance and amendments before launch. EU and UK regimes are not interchangeable.

## 1. GDPR: core engineering implications

GDPR territorial scope includes certain organizations outside the EU that offer goods/services to people in the Union or monitor their behaviour there. Applicability depends on the actual activity, not simply where the server sits.

Core principles include lawfulness, fairness and transparency; purpose limitation; data minimization; accuracy; storage limitation; integrity/confidentiality; and accountability. Translate them into data inventories, purpose-specific processing, retention, access controls, notices, rights workflows, privacy by design and records.

Rights can include access, rectification, erasure, restriction, portability and objection, subject to conditions/exceptions. Some processing may require a Data Protection Impact Assessment (DPIA). A Data Protection Officer is mandatory only when statutory conditions are met; not every startup automatically needs one.

A personal-data breach may require supervisory authority notice within 72 hours after awareness unless it is unlikely to create risk to individuals. Communication to affected individuals may be required where high risk exists. Escalate immediately to privacy/legal specialists; do not copy this deadline to other countries.

## 2. EU international transfers

GDPR Chapter V regulates transfers to third countries. Tools include adequacy decisions, Standard Contractual Clauses (SCCs), Binding Corporate Rules and limited derogations. Adequacy decisions are specific and can change. Where SCCs are used, assess the destination and transfer context; supplementary safeguards may be needed.

An EU cloud region does not automatically resolve every transfer. Examine support access, telemetry, logs, subprocessors, backup and remote administration.

## 3. Digital Services Act (DSA)

The DSA creates due-diligence obligations for intermediary services and different categories of online platforms. Duties vary by service category, size and role. Topics include points of contact, transparency in terms, notice-and-action for allegedly illegal content, statements of reasons for certain moderation actions, complaint handling for covered services, transparency reporting and additional duties for designated Very Large Online Platforms/Search Engines (VLOPs/VLOSEs).

Do not assume every app has the same duties. Determine whether the service is an intermediary, hosting service, online platform, marketplace or other defined category, and assess thresholds/exclusions with EU counsel. VLOPs/VLOSEs have additional systemic-risk obligations.

Potential engineering implications:

- accessible notice/report forms and evidence capture;
- timestamps and policy version for moderation decisions;
- understandable reasons for restrictions;
- appeal/complaint workflows;
- trusted-flagger handling where applicable;
- recommender transparency and user choices under relevant provisions;
- ad transparency and restrictions on certain targeting;
- risk assessment/mitigation for designated large services;
- reporting and data access obligations where applicable.

## 4. EU AI Act

The AI Act uses a risk-based approach with different rules for prohibited practices, high-risk systems, transparency duties and general-purpose AI models. A company's role may be provider, deployer, importer or distributor depending on facts. Do not label every AI feature high-risk or assume every recommender receives the same classification; assess intended purpose and legal definitions.

As of 13 November 2026, the Commission's live implementation timeline (which reflects amendments introduced by the Digital Omnibus on AI) lists entry into force on 1 August 2024; general provisions and prohibited-practice rules from 2 February 2025; general-purpose AI rules and governance from 2 August 2025; most rules including specified transparency provisions from 2 August 2026; a further milestone on 2 December 2026 for certain new prohibitions and transition provisions; and later milestones in 2027 and 2028. The Commission page lists 2 August 2027 for Member States' AI regulatory sandbox milestone, 2 December 2027 for specified Annex III high-risk system rules, and 2 August 2028 for certain high-risk AI embedded in regulated products. Do not treat one summary date as applying to every AI system: identify the system, provider/deployer role, category, transition rule and current consolidated text. Re-check the live official timeline before launch.

For generative AI assess transparency, AI literacy, prohibited practices, provider/deployer role, documentation, human oversight and interaction with GDPR, DSA and copyright law. Synthetic-content/deepfake transparency may be relevant depending on system role and output.

## 5. UK GDPR and the Children's Code

The UK has its own UK GDPR and Data Protection Act framework, with the Information Commissioner's Office (ICO) as regulator. EU and UK rules can be similar but have separate transfer, regulator and legislative developments. Determine which regime applies and use its current transfer tools.

The ICO's Age Appropriate Design Code can affect services likely to be accessed by children. It addresses children's best interests, age-appropriate application, high privacy defaults, minimization, geolocation, profiling, parental controls and nudge techniques. Assess scope and current guidance with UK counsel.

## 6. Product examples

- **Private messaging:** analyse purpose, minimization, security, retention, abuse reporting, lawful requests and whether end-to-end encryption is offered.
- **Public recommendation feed:** assess ranking transparency, user choices, risk, data processing and service category.
- **Creator marketplace:** consider trader status, consumer protection, ads, tax, payments, disputes and marketplace-specific duties.

## 7. Pre-launch questions

Which EU/EEA and UK markets are targeted? What DSA service category applies? Which roles do you have per processing activity? Are children likely to use the service? Which AI systems are used and what legal role applies? Where are support staff, logs, backups and vendors? Which transfer tools are needed? Are notices, rights, appeals and reports operational?

## Sources

- GDPR official text: https://eur-lex.europa.eu/eli/reg/2016/679/oj/eng/
- European Commission data protection: https://commission.europa.eu/law/law-topic/data-protection_en
- EU international transfers: https://commission.europa.eu/law/law-topic/data-protection/international-dimension-data-protection/rules-international-data-transfers_en
- Digital Services Act package: https://digital-strategy.ec.europa.eu/en/policies/digital-services-act-package
- DSA legal text: https://eur-lex.europa.eu/eli/reg/2022/2065/oj/eng
- EU AI Act implementation timeline: https://ai-act-service-desk.ec.europa.eu/en/ai-act/eu-ai-act-implementation-timeline
- UK ICO Children's Code: https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/childrens-information/childrens-code-guidance-and-resources/
- UK ICO international transfers: https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/international-transfers/
