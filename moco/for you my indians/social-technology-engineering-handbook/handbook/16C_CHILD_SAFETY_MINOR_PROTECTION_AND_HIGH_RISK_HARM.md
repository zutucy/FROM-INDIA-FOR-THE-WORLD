# 16C — Child Safety, Minor Protection and High-Risk Harm

**Edition:** 13 November 2026  
**Purpose:** Explain how products should reason about children and teenagers, high-risk contact, exploitation, privacy, age assurance, parental involvement and specialist response. Requirements vary substantially by country and product category; obtain qualified local legal and child-safety advice before launch.

## 1. Why child safety needs its own design work

Children and teenagers can face risks different from adults: grooming, sexual exploitation, coercion, bullying, unwanted contact, commercial manipulation, exposure to age-inappropriate content, location disclosure and pressure to share intimate information. Children may also have different capacities to understand consent, privacy settings and long-term data consequences.

A platform cannot solve these risks only by adding a date-of-birth field. Age data may be incorrect, and a product's design can itself expose young users to risk.

## 2. Start with an age and audience strategy

Before designing onboarding, decide:

- Is the product directed to children, teenagers, adults or a mixed audience?
- What minimum age applies in each target market and under which law or service rule?
- What happens when a user declares an age below the threshold?
- Is age assurance necessary, and what is proportionate?
- Which features are available to different age bands?
- How do parents/guardians become involved where legally required?
- What data is collected for age checks, how long is it retained and who can access it?

Do not assume a single global age threshold. Some legal frameworks distinguish children by age and context; some have special consent-age rules, platform duties or parental-consent requirements.

## 3. Age assurance trade-offs

Possible methods include self-declaration, parental confirmation, age estimation, document checks, identity-provider assertions and third-party age-assurance services. Each has limitations:

- Self-declaration is low-friction but easy to misstate.
- Document checks can be intrusive and create sensitive identity data.
- Facial age estimation can be inaccurate and create biometric/privacy concerns.
- Third-party services can reduce direct data collection but create processor, transfer, security and vendor-dependence risks.
- Parental consent workflows can be difficult when families lack stable identity documents or digital access.

Use proportionality: collect the minimum information needed to make a decision, avoid storing raw identity documents where possible, document accuracy/error rates, offer accessible alternatives and create a review process for false rejections. Age assurance should not become a hidden universal identity-tracking system.

## 4. Safer defaults for younger users

Depending on product and applicable law, controls may include:

- Private-by-default profiles or more restrictive discovery.
- Limits on unsolicited messages from adults or unknown accounts.
- Restrictions on public location sharing and precise metadata.
- Limited discoverability by phone/email.
- Strong controls for mentions, tags, comments and live interactions.
- Friction before sharing sensitive information.
- Clear block/report tools.
- Recommendation safeguards for age-inappropriate content.
- Limits on targeted advertising and behavioural profiling where required.
- Age-appropriate explanations and privacy controls.

The exact rules must be designed for the target jurisdiction and age band. A “teen mode” label does not prove compliance or safety.

## 5. Grooming and exploitation risk signals

Potential risk patterns include persistent unwanted contact, requests to move to private channels, secrecy instructions, threats, coercion, gifts or money used to manipulate, requests for intimate images and attempts to isolate a minor from trusted adults. Automated systems can surface patterns, but false positives are possible and context matters.

Do not build invasive monitoring that indiscriminately reads all private communications without a lawful, proportionate and transparent basis. Design limited reporting and detection methods, trained specialist review, and legally approved escalation paths. End-to-end encryption changes what a service operator can see; safety design must honestly account for those technical limits rather than promise impossible scanning.

## 6. Sensitive data and privacy

Children's data deserves heightened protection. Review:

- Whether each data field is necessary.
- Whether analytics or advertising SDKs collect identifiers.
- Whether precise location is collected or inferred.
- Whether public profile data could reveal school, routine or home location.
- Whether messages and uploads are retained longer than needed.
- Whether model training or personalisation uses children's data.
- Whether data can be deleted from backups, search indexes and derived systems according to a documented policy.

Privacy settings must be understandable to the user, not only present in a complex policy. Minimise collection and access by default.

## 7. High-risk incident handling

Create specialist pathways for:

- Suspected child sexual exploitation or grooming.
- Credible threats of physical harm.
- Self-harm or suicide crisis disclosures.
- Non-consensual intimate imagery.
- Doxxing and stalking.
- Sextortion, blackmail and coercion.

Define the trained internal responder, emergency escalation criteria, evidence-handling restrictions, legal reporting obligations, user-support language and after-action review. Staff should not request, copy or circulate illegal material. Use approved reporting channels and specialist guidance.

## 8. Crisis support: do not pretend a platform is a clinical service

When a user expresses crisis or self-harm intent, product responses should be compassionate, non-judgmental and designed with qualified experts. Provide locally appropriate crisis resources when possible. Avoid public confrontation, sensationalised labels or punitive automation. Define limits: an ordinary platform cannot guarantee emergency intervention or diagnose a person. Protect user privacy while following applicable legal duties and credible imminent-risk procedures.

## 9. Design and testing checklist

- Run child-rights and privacy impact reviews for relevant features.
- Test onboarding, age checks and consent for usability and exclusion errors.
- Test whether an adult can bypass restrictions by editing API requests or changing a declared birth date.
- Test block/report flows across alternate accounts and messaging channels.
- Test location metadata removal from uploaded media when promised.
- Review defaults after product updates; new features can reopen old risks.
- Include young people and child-safety specialists in appropriate, ethically designed research.
- Review any AI model trained or evaluated on child-related data under strict governance.

## 10. Legal and policy sources to verify per market

- UNICEF child online protection: https://www.unicef.org/protection/violence-against-children-online
- US FTC COPPA resources: https://www.ftc.gov/legal-library/browse/rules/childrens-online-privacy-protection-rule-coppa
- UK ICO Children's Code: https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/childrens-information/childrens-code-guidance-and-resources/
- EU Digital Services Act information: https://digital-strategy.ec.europa.eu/en/policies/digital-services-act-package
- India MeitY and official Gazette publications: https://www.meity.gov.in/ and https://egazette.gov.in/

A current official source must be checked for effective dates, amendments, scope and regulator guidance. Do not rely on a secondary summary for legal sign-off.
