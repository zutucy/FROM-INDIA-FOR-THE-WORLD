# 15A — Global privacy, jurisdiction, data mapping and cross-border transfers

**Legal status date: 13 November 2026.** This is a product-engineering orientation, not legal advice. Laws, guidance, enforcement decisions and commencement dates change. Confirm official text and obtain local advice before launch.

## 1. There is no single worldwide privacy law

A service accessible worldwide can be subject to multiple regimes. Applicability can depend on establishment, user location, targeting, monitoring, data types, purpose, age, scale and sector. Incorporating in one country does not automatically mean only that country's law applies; equally, not every law automatically applies to every website visitor.

## 2. Historical development

Modern privacy rules grew from constitutional and human-rights principles, national data-protection statutes, OECD guidelines, Council of Europe Convention 108, sector laws and regional frameworks. The EU Data Protection Directive of 1995 was replaced by GDPR, which applied from 25 May 2018. Different regions developed comprehensive laws, sectoral rules, consumer-protection frameworks, cybersecurity rules and data-localization requirements.

The outcome is a patchwork. Some frameworks emphasize lawful processing and individual rights; others also add localization, security assessment or special government-access rules. A global product needs a map, not a single generic footer policy.

## 3. Map jurisdiction before choosing cloud regions

For each market identify company establishment, targeted users/language/currency, data collection points, controller/processor roles, primary cloud region, backups, support/admin access locations, analytics/ad/payment/identity vendors, subprocessors, data categories, age groups, retention, deletion and breach rules.

A cloud region is only one node. Logs, backups, telemetry, support, email, AI APIs and payment processors may process data elsewhere.

## 4. Data map and inventory

For each feature, record purpose, data category, source, recipients, storage locations, access roles, retention, legal ground/consent where required, security, user-rights workflow and transfer mechanism. Update it when an SDK, vendor, region, model or support tool changes.

Classifications such as public, internal, confidential, personal, sensitive and regulated help only when access and retention controls enforce them.

## 5. Controller, processor and vendor roles

Many regimes distinguish an organization deciding purposes/means from a provider processing on its instructions. The actual role depends on facts and law, not only contract labels. A vendor might be a processor for one activity and an independent controller for another. Assess each purpose and data flow.

Contracts may need documented instructions, confidentiality, security, subprocessors, rights support, breach notice, deletion/return, audits and transfer clauses.

## 6. Purpose, lawful basis and minimization

For every processing activity define a specific purpose, lawful ground where required, transparency, retention and access. Do not collect “just in case.” If analytics needs a weekly aggregate, retaining detailed identifiable click histories may be unnecessary.

Consent is not the only lawful basis in every regime. A consent banner does not make every activity lawful. Requirements for valid consent differ; do not bundle optional tracking into a core service deceptively.

## 7. International transfers

Possible legal mechanisms include adequacy decisions, standard contractual clauses, binding corporate rules, approved certification/codes, limited statutory exceptions, localization or security assessment. The correct mechanism depends on the source and destination jurisdiction, data, recipient, role and transfer facts.

A transfer tool does not replace a lawful purpose, transparency, security and individual rights. A contract cannot override mandatory local law. Where required or prudent, assess destination laws/government access, onward transfers, vendor access, encryption/key control, remedies and supplementary safeguards. Record and revisit the assessment.

## 8. Residency versus sovereignty

**Residency** usually refers to where data is stored or processed. **Sovereignty** concerns which jurisdiction's laws/authority may apply. Storing data in one country does not necessarily prevent another country's law from applying to the company/provider. Residency alone does not prove compliance.

Check primary data, replicas, backups, disaster recovery, telemetry, support, key management, logs and subprocessors.

## 9. Rights workflows

Depending on law, individuals may have access, correction, deletion, portability, objection, restriction, consent withdrawal or complaint rights. Build intake, identity verification, search, review, exceptions, response, evidence and downstream propagation.

Do not delete legally required records without a reviewed basis; do not use vague legal holds to retain everything. Separate active data from restricted records and document rationale/expiry. A deleted user may have copies in media derivatives, search, analytics, model features, vendors and backups.

## 10. Children and vulnerable users

Age thresholds, parental consent, age assurance, profiling and targeted-ad rules vary. A global “13+” checkbox is not universally sufficient. Design proportionate age assurance and assess false positives/privacy costs. Get specialist advice before allowing children to use a service.

## 11. Exercise

Draw all data flows for signup: browser, API, identity service, database, email, analytics and support. Mark data category, purpose, vendor role, countries, retention and transfer mechanism to investigate. Clearly label unknowns rather than inventing answers.

## Sources

- UNCTAD Global Cyberlaw Tracker (updated 9 Sep 2026): https://unctad.org/page/data-protection-and-privacy-legislation-worldwide
- GDPR text: https://eur-lex.europa.eu/eli/reg/2016/679/oj/eng/
- EU international transfer rules: https://commission.europa.eu/law/law-topic/data-protection/international-dimension-data-protection/rules-international-data-transfers_en
- EU adequacy decisions: https://commission.europa.eu/law/law-topic/data-protection/international-dimension-data-protection/adequacy-decisions_en
- Brazil ANPD transfer regulation: https://www.gov.br/anpd/pt-br/assuntos/assuntos-internacionais/transferencia-internacional-de-dados
