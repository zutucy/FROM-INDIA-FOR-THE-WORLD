# 15D — Global launch matrix, data transfers and legal-change monitoring

## 1. A global service needs a market-entry process

Do not assume that because a website loads in a country it is ready to serve that country. A market-entry gate should assess audience, language, age, privacy, content, payment, tax, consumer rules, support and operational capacity.

## 2. Launch-gate questions

For each market, record:

1. Are you targeting the market through ads, pricing, language or local sales?
2. Who is likely to use the product: residents, children, businesses or professionals?
3. Are local languages, accessibility, dates/currencies and payment methods supported?
4. Which privacy, platform, consumer, copyright, AI and sector rules apply?
5. Where are primary data, logs, backups, support access and vendors?
6. Which cross-border transfer mechanism is needed?
7. Are complaints, safety reports, appeals and lawful requests operational?
8. Can incidents be detected and reported on applicable timelines?
9. Are user/vendor contracts and local notices accurate?
10. Can support respond in the expected language/time zone?
11. Who owns the go/no-go decision and legal sign-off?

## 3. Data-flow register template

| Field | What to record |
|---|---|
| Processing activity | Account registration, media upload, analytics, support |
| Data categories | Email, identifier, profile, device/security log, content |
| Purpose | Specific reason, not vague future use |
| Data subject | Member, visitor, creator, employee, child, etc. |
| Source | User, device, vendor, public source |
| System | Web, API, database, object storage, AI service |
| Vendor/recipient | Identity, email, analytics, payment, support |
| Locations | Primary, replica, backup, admin/support access |
| Role | Controller/business, processor, independent controller as assessed |
| Legal basis | Determined for jurisdiction/purpose |
| Retention | Period and reason |
| Security | Encryption, access, logging, backup |
| Rights path | Access/correction/deletion workflow |
| Transfer mechanism | Adequacy/SCC/contract/other route if required |
| Owner/review | Named owner and review date |

## 4. Jurisdiction-aware architecture

Avoid scattering country rules across dozens of controllers. Use a versioned policy/configuration layer with explicit owners and effective dates. But applicability cannot be reduced to a single `country_code` boolean: age, role, service category, purpose, threshold, data category and date may matter.

Use location signals only as needed and with privacy controls. Account residence, billing country, IP geolocation and user-declared location are different signals; IP alone cannot reliably prove residence or age because of VPNs, travel, shared networks and inaccuracies. Evaluate relevant policy server-side, maintain notices/preferences separately from inferred location, and log decisions without collecting unnecessary sensitive detail.

## 5. Vendor due diligence

Ask what data a vendor receives and why; its role; hosting/backup/support countries; subprocessors; transfer mechanism; encryption/key access; incident notice timing; deletion/right-request support; retention after contract; export format; audit assurances; and exit plan. Keep a vendor register and reassess after material changes.

## 6. Legal-change monitoring

Track official statutes/gazettes, regulator guidance and enforcement, court decisions, commencement notices, adequacy/transfer changes, sector notices and vendor contract updates. Social posts and summaries may alert you to an issue but are not authoritative.

For each change, record publication date, effective date, official source, impacted markets/features, required engineering change, owner, deadline and completion evidence. A law may be enacted long before its substantive obligations commence; phased commencement is common.

## 7. Example: EU user in a global app

A request may reach a global edge, but that fact alone does not decide legal scope. The application provides applicable notices and preferences; the identity provider may be a vendor; analytics receives only approved fields; storage and support locations are mapped; access and retention are enforced; and transfers use a valid mechanism where needed.

If the user later requests deletion, follow the request through primary database, media derivatives, search, cache, analytics, model features, vendors and backups under the relevant rules. A country-specific policy page alone does not satisfy the engineering work.

## 8. Go/no-go checklist

- [ ] Target market and service scope documented.
- [ ] Local legal review completed for applicable rules.
- [ ] Privacy notice and terms accurate/localized.
- [ ] Data inventory and processing records maintained where required.
- [ ] Age/child-safety decision documented.
- [ ] Rights requests and complaints tested.
- [ ] Cross-border transfers assessed and contracts in place.
- [ ] Security and incident-reporting process verified.
- [ ] Reporting, appeals and takedown process staffed.
- [ ] Consumer, payment, tax and copyright reviewed.
- [ ] Vendor/subprocessor list current.
- [ ] Support coverage and escalation confirmed.
- [ ] Monitoring and rollback ready.
- [ ] Named accountable owner approves launch.

## 9. Important limits

This is an engineering launch checklist, not a complete statement of law. It does not replace local counsel, a privacy professional/DPO, tax advisor or sector specialist. Payments, health, biometrics, children, encrypted messaging, advertising and generative AI can materially change the analysis.

## Sources

- UNCTAD Global Cyberlaw Tracker: https://unctad.org/page/data-protection-and-privacy-legislation-worldwide
- EU data protection: https://commission.europa.eu/law/law-topic/data-protection_en
- EU international transfers: https://commission.europa.eu/law/law-topic/data-protection/international-dimension-data-protection/rules-international-data-transfers_en
- India official resources: https://www.meity.gov.in/data-protection-framework
- Brazil ANPD: https://www.gov.br/anpd/
- UK ICO: https://ico.org.uk/
- US FTC: https://www.ftc.gov/
