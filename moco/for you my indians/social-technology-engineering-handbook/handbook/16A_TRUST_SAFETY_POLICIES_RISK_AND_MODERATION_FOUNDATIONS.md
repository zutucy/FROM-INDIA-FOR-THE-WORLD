# 16A — Trust, Safety, Policies, Risk and Moderation Foundations

**Edition:** 13 November 2026  
**Purpose:** Explain how any user-facing digital service establishes safe-use rules, identifies abuse, designs enforcement and measures whether safety systems work. The examples use a social platform, but the principles also apply to marketplaces, forums, collaboration tools, games and AI products.

## 1. What trust and safety means

Trust and safety is the combination of product design, policy, engineering, operations and governance used to reduce harm and maintain a usable service. It is not identical to cybersecurity:

- **Cybersecurity** protects systems, accounts, data and infrastructure from compromise or misuse.
- **Trust and safety** addresses harmful behaviour and content occurring through the product, including behaviour by legitimate authenticated users.
- The two overlap: account takeover can enable harassment; spam can be both abuse and an availability risk; malicious uploads can be both a security issue and a user-safety issue.

A product is not safe merely because it has a Terms of Service link or an automated classifier. Safety is an operating capability with trained owners, escalation paths, evidence handling, quality review and measurable outcomes.

## 2. Build a policy system before building enforcement tools

A policy should define prohibited conduct in language a user can understand and a reviewer can apply consistently. Avoid vague rules such as “be nice” as the only standard. Use categories, definitions, examples, context and enforcement ranges.

A practical policy structure:

1. Purpose and scope: which products, features and users are covered.
2. Definitions: content, account, impersonation, threat, spam, private information, child, intellectual property claim, and so on.
3. Prohibited conduct: clearly defined categories.
4. Allowed or contextual conduct: news reporting, counterspeech, education, art, satire and other contexts that may need different treatment.
5. Enforcement: content removal, reach restriction where lawful and appropriate, feature limits, warning, temporary suspension, termination or referral to specialist teams.
6. Reporting and appeals: how decisions are challenged and reviewed.
7. Transparency: what users are told and what aggregate information is published.
8. Change control: policy version, effective date, reviewer, rationale and archived versions.

Policies should be written with local language, cultural context and applicable law in mind. A literal machine translation may change meaning or produce unfair outcomes. Legal requirements are a floor, not a complete safety policy.

## 3. Risk taxonomy

A starting taxonomy can include:

| Risk category | Examples | Potential product controls |
|---|---|---|
| Harassment and abuse | Targeted insults, intimidation, repeated unwanted contact | Report, block, mute, reply controls, rate limits, review queues |
| Threats and violence | Credible threats, praise or instruction depending on context | Specialist escalation, evidence preservation, emergency procedure |
| Self-harm and suicide | Encouragement, exploitation, graphic material | Context-sensitive handling, crisis resources, trained escalation |
| Child sexual exploitation and grooming | Sexual exploitation, solicitation, coercion | Strict detection and escalation, restricted access, legally required reporting |
| Non-consensual intimate imagery | Distribution or threats to distribute private sexual imagery | Fast report path, hashing/known-match tooling where lawful, privacy safeguards |
| Hate and discriminatory abuse | Targeting protected characteristics | Contextual policy, language expertise, appeal review |
| Spam and scams | Fake offers, phishing, repetitive promotion | Rate controls, reputation signals, user warnings, account review |
| Impersonation | Fake identity, deceptive affiliation | Verification options, reporting, evidence review |
| Misinformation/manipulation | Coordinated deception, fabricated media | Contextual labels or friction where appropriate; avoid overconfident automated truth judgments |
| Privacy violations | Doxxing, leaked credentials, sensitive personal data | Restricted access, fast takedown review, data exposure response |
| IP infringement | Copyright/trademark misuse | Rights-holder report process, counter-notice where required, repeat-infringer policy |
| Platform manipulation | Fake engagement, bots, coordinated inauthentic activity | Behavioural detection, rate limits, integrity investigations |

This taxonomy is a product starting point, not a universal legal classification. Local law may define additional categories or special procedures.

## 4. Severity and prioritisation

Not all reports should enter one undifferentiated queue. Prioritise according to credible harm, urgency, exposure, victim vulnerability, likelihood of continued distribution and available evidence.

A simple internal triage model:

- **P0 / immediate:** imminent physical danger, active child exploitation, credible imminent threats, major account/system compromise or ongoing mass exposure of extremely sensitive data.
- **P1 / urgent:** serious targeted harassment, non-consensual intimate imagery, credible impersonation scam affecting multiple users, large-scale abuse campaign.
- **P2 / standard:** policy violations requiring timely review but not an immediate emergency.
- **P3 / low urgency:** low-impact spam, borderline content or requests that can be handled in normal queue order.

The labels are examples. Define operational targets based on risk, jurisdiction and actual staffing. Never imply that an internal severity label overrides a statutory legal deadline.

## 5. Moderation system architecture

A moderation pipeline can combine user reports, proactive detection and specialist investigations:

```text
Content / account / activity event
        |
        +--> User report -----------------+
        |                                 |
        +--> Automated signals -----------+--> Intake + deduplication
        |                                 |
        +--> Trusted escalation ----------+        |
                                                 Risk triage
                                                     |
                                    +----------------+----------------+
                                    |                |                |
                                 No action       Human review    Emergency route
                                    |                |                |
                                 Record        Policy decision   Specialist response
                                    |                |                |
                                    +---------- Enforcement ----------+
                                                     |
                                           Notify + appeal + audit
                                                     |
                                           Quality review and metrics
```

Automated signals can prioritise review, detect known patterns or apply narrow high-confidence actions. However, classifier output is probabilistic. Context, sarcasm, language variation, reclaimed terms, news reporting and adversarial evasion can create false positives and false negatives.

For high-impact decisions, define when a human must review, what evidence they can see, what explanations are logged and how a user can appeal. Human review also needs quality assurance; “human in the loop” is not a guarantee of correctness.

## 6. Product design as prevention

Prevention is often more effective than moderation after harm occurs:

- Make profile and post visibility understandable.
- Provide block, mute, restrict and audience controls.
- Allow users to limit who can message, mention, tag or reply.
- Apply safe defaults for younger users where required.
- Add friction to high-risk behaviours such as mass messaging or repeated account creation.
- Make report controls easy to find without exposing reporters to retaliation.
- Avoid public counters or recommendation mechanics that reward abusive pile-ons.
- Give users clear controls for recommendations and sensitive content.
- Make privacy choices understandable at the point of action.

Safety controls should be tested for misuse. For example, a block feature should not disclose a user's new account or provide a harasser with a list of alternate accounts.

## 7. Measure safety without creating bad incentives

Possible metrics include:

- Time to first review by severity.
- Time to action for high-risk reports.
- Report volume by category and language.
- Confirmed violation rate and false-positive estimate.
- Appeal rate and appeal-overturn rate.
- Repeat-violation rate.
- Prevalence or exposure estimates for selected harms.
- User ability to discover and complete reporting.
- Reviewer workload, queue backlog and quality scores.
- User trust survey results.

Do not optimise only for number of removals or fastest closure. Those metrics can encourage rushed or excessive enforcement. Pair speed with correctness, appeal outcomes, harm reduction and user experience. Publish methodology and limitations when sharing aggregate measurements.

## 8. Governance and accountability

Every policy category needs an accountable owner, escalation contact and review cadence. Major policy changes should be versioned and reviewed by product, legal, safety, security, privacy and affected local experts as appropriate. Maintain an audit trail of high-impact decisions, but restrict access to sensitive reports and evidence. Staff should not browse user content without a legitimate work purpose.

## 9. Practical exercises

1. Draft a one-page policy for spam, including examples and non-examples.
2. Create a severity rubric for harassment and explain which facts increase urgency.
3. Draw a moderation queue architecture with report deduplication and appeal states.
4. Design a privacy-preserving report form that collects only necessary information.
5. Create a metric dashboard that measures both enforcement speed and decision quality.

## 10. Further references

- UN Guiding Principles on Business and Human Rights: https://www.ohchr.org/sites/default/files/documents/publications/guidingprinciplesbusinesshr_en.pdf
- Santa Clara Principles: https://santaclaraprinciples.org/
- OECD work on online safety and digital services: https://www.oecd.org/digital/
- UNICEF resources on child online protection: https://www.unicef.org/protection/violence-against-children-online
- NIST AI Risk Management Framework: https://www.nist.gov/itl/ai-risk-management-framework
