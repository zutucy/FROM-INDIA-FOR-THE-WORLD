# 14D — Team, organization, roadmap, metrics and go-to-market

## 1. Product organizations are cross-functional

A product team joins product, design, engineering, data, security, legal, operations and customer support. A small company may combine roles, but accountability still needs to be clear.

Typical responsibilities:

- Product manager: problem, priority, outcome and coordination.
- Designer/researcher: user research, flows and interaction design.
- Frontend/mobile engineer: client experience and integration.
- Backend engineer: APIs, business logic, persistence and vendors.
- Data/ML engineer: pipelines, measurement and models.
- SRE/DevOps: deployment, reliability and infrastructure.
- Security/privacy: threats and data-risk review.
- QA: risk-based test strategy and release confidence.
- Trust and safety: abuse rules, moderation and escalation.
- Support/operations: user issues and service workflows.

Titles matter less than ownership, coverage and communication.

## 2. Small-team operating model

An early product team may include a founder/product lead, designer (possibly part time), two or three engineers and shared QA/security/legal expertise. This is an illustrative shape, not a universal staffing minimum. Complexity, risk, platforms, media volume, countries and support expectations drive headcount.

When one person does many roles, explicitly schedule security, backup testing, QA, support and operations. A small team does not make these responsibilities disappear.

## 3. Roadmap and execution

Organize roadmap items around user outcomes and technical risks. Break work into milestones with dependencies and acceptance criteria. Separate discovery from committed delivery. Reserve capacity for maintenance, vulnerabilities, incidents and technical debt.

A project brief should record owner, goal, scope, non-goals, dependency, risks, acceptance criteria, rollout, instrumentation and rollback. Maintain a decision log for major technical/business choices.

## 4. Delivery metrics

DORA's software-delivery measures have evolved; use current guidance rather than treating any old four-metric list as timeless. Common measures include change lead time, deployment frequency, failed-deployment recovery time, change fail rate and deployment rework. These are system/team measures, not pressure to deploy unsafely.

Balance delivery measures with task success, reliability, latency, support volume, security findings and privacy incidents. A team can deploy frequently and still deliver poor value.

## 5. Incident and customer support

Create a ticket taxonomy separating account recovery, safety reports, billing, privacy requests, copyright complaints and technical issues. Assign severity and response targets based on user harm and legal commitments. Support agents should not have broad access to private content by default; create audited, purpose-limited access.

Escalate suspected security incidents, child-safety issues, imminent threats and regulated complaints to trained owners. Scripts help consistency but must allow escalation when a case does not fit.

## 6. Vendor management

Maintain a vendor register: data shared, purpose, role, region, subprocessors, retention, security controls, incident notice, deletion, audit rights, export format and exit plan. Contracts should reflect data roles and transfer requirements. Assess critical vendors before production use and reassess after material changes.

Plan what happens if a vendor fails: export data, rotate credentials, disable integration, change providers or operate in degraded mode. A SaaS outage can stop your business while your servers remain healthy.

## 7. Governance

Document who approves production access, high-risk data use, ad-targeting changes, AI models, legal terms, vendors and security exceptions. Use separation of duties for payments, key management and admin rights where possible. Audit exceptional access and decisions.

## 8. Go-to-market plan

Identify target segment, positioning, channel, landing page, onboarding, help content, support coverage, moderation capacity, pricing readiness, reliability and rollback gates, success/stop metrics and communication for known limitations. Launch to a cohort that matches support capacity. A smaller responsible launch is better than an uncontrolled one that harms users.

## 9. RACI exercise

For a release, assign Responsible, Accountable, Consulted and Informed roles for code review, privacy/security review, production deploy, incident response, user messaging and rollback. Each activity should have one clearly accountable owner.

## Sources

- DORA: https://dora.dev/
- Google SRE: https://sre.google/books/
- GOV.UK Service Manual: https://www.gov.uk/service-manual
- NIST SSDF: https://csrc.nist.gov/pubs/sp/800/218/final
