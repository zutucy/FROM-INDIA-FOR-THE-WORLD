# 15C — India, United States, China, Brazil, Japan and other market patterns

**Status date: 13 November 2026.** This is a high-level engineering comparison, not legal advice. Sub-national, sectoral and implementing rules can change outcomes. Obtain local advice before launch.

## 1. India

### Digital Personal Data Protection Act, 2023 and Rules, 2025

India's DPDP Act was enacted in 2023. The Gazette notification G.S.R. 843(E), dated 13 November 2025, provides phased commencement. Some institutional/enabling provisions commenced upon publication; a limited set is scheduled one year later; the main processing provisions are scheduled 18 months after publication, i.e. 13 May 2027, unless later notifications change the position. The DPDP Rules, 2025 were published in the Gazette on 13 November 2025 (G.S.R. 846(E)); the Gazette heading gives that date. Under the Rules' commencement clause, Rules 1, 2 and 17–21 commenced on publication; Rule 4 is scheduled one year after publication (13 November 2026); and Rules 3, 5–16, 22 and 23 are scheduled eighteen months after publication (13 May 2027), unless a later notification changes the position. Therefore, on the handbook's status date, do not claim that every substantive processing obligation is already in force. Check the exact commencement status of each provision and subsequent notifications.

The Act uses Data Fiduciary and Data Processor concepts. A child is generally an individual under 18 under the Act. Section 9 contains a framework for verifiable parental consent and safeguards/restrictions for processing children's data, subject to the statutory framework, exemptions and notifications. A birth-date checkbox alone is not a serious child-safety design.

Engineering readiness: purpose/notice records, consent and rights workflows, security safeguards, breach handling, retention/deletion, vendor contracts, grievance contact and age-related controls. Tie launch tasks to actual commencement dates.

### IT Rules and intermediary operations

A service hosting user content may be an intermediary under India's IT Act framework. The IT (Intermediary Guidelines and Digital Media Ethics Code) Rules, 2021, as amended, create due-diligence and grievance obligations based on service type/category and facts. Significant Social Media Intermediary status has additional duties. Classify the actual product; do not assume every app has identical compliance requirements.

CERT-In's 28 April 2022 directions cover specified entities and listed incidents, with a six-hour reporting requirement after noticing/brought-to-notice for covered incident categories, secure retention of ICT logs for a rolling 180 days within Indian jurisdiction, and other measures. Verify applicability and exact scope with counsel/security specialists.

## 2. United States

The United States does not have one omnibus federal consumer privacy statute equivalent to GDPR. The landscape combines federal sector laws, FTC enforcement, state comprehensive privacy laws, biometric/health/consumer laws, breach-notification statutes and children's privacy rules.

- **COPPA:** Applies to covered operators of child-directed services and certain services with actual knowledge they collect personal information from children under 13. The FTC finalized COPPA Rule amendments in January 2025, including changes involving separate parental consent for certain disclosures and limits on indefinite retention. Check current effective/compliance dates and FTC text.
- **California CCPA/CPRA:** Applies when statutory thresholds/criteria are met; addresses consumer rights and business duties relating to collection, use, sharing/sale and sensitive personal information. California has a dedicated privacy agency and ongoing regulatory developments.
- **Other states:** Many states have enacted privacy laws with different thresholds, rights, exemptions, sensitive-data rules and opt-out mechanisms. A state-by-state matrix is needed.
- **Sector rules:** Health, financial, education, communications and children's services may trigger additional laws.

Engineering consequences may include privacy-request intake, opt-out/preference propagation, vendor/data-sharing inventory, targeted-ad controls, child-directed-service assessment and breach-notification workflows. One state's law does not cover the entire country.

## 3. China

China's Personal Information Protection Law (PIPL) applies to processing in China and can apply extraterritorially in defined cases such as offering products/services to people in China or analysing their behaviour. It covers processing principles, sensitive personal information, individual rights, processors, duties and cross-border provision.

Cross-border mechanisms may include a CAC security assessment, standard-contract filing, certification or applicable exemptions, depending on operator status, data type/volume and current measures. Thresholds and exemptions have changed; check the current CAC rules and official notices. Do not assume all data must always remain in China or that every transfer is unrestricted.

A service targeting China may also face cybersecurity, data governance, content, licensing, algorithm recommendation and platform rules beyond PIPL. Local operations, hosting and vendor strategy may differ materially from a global deployment.

## 4. Brazil

Brazil's LGPD (Lei Geral de Proteção de Dados) is a comprehensive personal-data framework overseen by ANPD. It includes legal bases, rights, controller/operator roles, security and international-transfer rules. ANPD Resolution CD/ANPD No. 19 of 23 August 2024 regulates international transfers and standard contractual clauses; ANPD's official page notes subsequent correction/update information. Review the current consolidated text and transfer conditions.

Product implications include processing-purpose mapping, rights handling, vendor contracts, incident response, transfer mechanisms and accessible local-language transparency. Consumer and internet frameworks may also apply.

## 5. Japan

Japan's APPI is overseen by the Personal Information Protection Commission (PPC). It includes purpose specification, proper acquisition/use, security management, third-party provision and additional rules for provision to a third party in a foreign country. Overseas-transfer analysis may require consent or information about the destination's system and safeguards depending on the mechanism. Check current PPC guidance and amendments rather than relying only on an old translated copy.

## 6. Other markets worth mapping

- **Canada:** PIPEDA and provincial privacy laws; Québec has distinct requirements.
- **Australia:** Privacy Act/APPs, online safety and child-related rules may matter.
- **South Korea:** PIPA and transfer rules require local review.
- **Singapore:** PDPA accountability, notice/consent, protection and transfer limitation duties.
- **South Africa:** POPIA and its cross-border provisions.
- **Indonesia:** Personal Data Protection Law and implementing rules.
- **Türkiye:** KVKK and transfer amendments.
- **UAE/Saudi Arabia:** National, free-zone and sectoral privacy/data rules may differ.

This list is illustrative, not exhaustive. UNCTAD's Global Cyberlaw Tracker is a discovery index, not controlling law or legal advice. Follow it to the national regulator, statute and official gazette.

## 7. Compare markets using the same questions

| Dimension | Questions |
|---|---|
| Scope | Does targeting/resident monitoring trigger the rule? |
| Lawful processing | Which bases and notice/consent rules apply? |
| Rights | Access, correction, deletion, portability, objection? |
| Children | Age, consent, assurance, profiling and ads? |
| Breach | Who must be notified, when and at what threshold? |
| Transfers | Adequacy, contract, consent, certification, assessment or localization? |
| Platform | Notice/takedown, appeal, grievance, transparency, authority contact? |
| AI | Disclosure, risk categories, automated decisions, synthetic media? |
| Sectors | Health, finance, education, telecom, biometrics or payments? |
| Enforcement | Regulator, sanctions, audits and private rights? |

## 8. Exercise

Choose three target markets. For each, record official law, regulator, territorial scope, child rules, rights, breach process, transfer tools, platform duties, commencement status and counsel owner. Mark unknowns instead of guessing.

## Sources

- India DPDP framework: https://www.meity.gov.in/data-protection-framework
- India Gazette phased commencement (13 Nov 2025): https://egazette.gov.in/WriteReadData/2025/267647.pdf
- India DPDP Rules announcement: https://www.pib.gov.in/PressReleasePage.aspx?PRID=2190655
- CERT-In directions: https://www.cert-in.org.in/PDF/CERT-In_Directions_70B_28.04.2022.pdf
- UNCTAD Global Cyberlaw Tracker: https://unctad.org/page/data-protection-and-privacy-legislation-worldwide
- China PIPL text: https://en.spp.gov.cn/2021-12/29/c_948419.htm
- Brazil ANPD transfers: https://www.gov.br/anpd/pt-br/assuntos/assuntos-internacionais/transferencia-internacional-de-dados
- Japan PPC: https://www.ppc.go.jp/en/legal/
- FTC COPPA amendments: https://www.ftc.gov/news-events/news/press-releases/2025/01/ftc-finalizes-changes-childrens-privacy-rule-limiting-companies-ability-monetize-kids-data
- California Privacy Protection Agency: https://cppa.ca.gov/
