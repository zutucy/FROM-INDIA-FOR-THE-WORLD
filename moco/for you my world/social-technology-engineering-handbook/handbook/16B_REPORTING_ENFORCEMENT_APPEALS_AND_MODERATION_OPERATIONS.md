# 16B — Reporting, Enforcement, Appeals and Moderation Operations

**Edition:** 13 November 2026  
**Purpose:** Turn policy into a real operating workflow: intake, triage, investigation, decision, enforcement, appeal, audit and continuous quality improvement.

## 1. A report is a case, not just a database row

A report should create a traceable case with a stable identifier and controlled access. A useful case record may include:

- Case ID and creation timestamp.
- Reporter account or anonymous/guest status where supported.
- Reported object: content, profile, conversation, advertisement, group or behaviour.
- Policy category and claimed harm.
- Evidence references, not unnecessary copied personal data.
- Risk/priority and reason for triage.
- Queue, assigned reviewer and timestamps.
- Decision, policy version and rationale code.
- Enforcement action and expiry/review date where applicable.
- User notifications and appeal state.
- Audit events and access history.

Separate the reporter's identity from the general review view where possible, because revealing the reporter can create retaliation risks. Avoid collecting information that the platform does not need.

## 2. Report intake design

A good report flow lets the user describe what happened without forcing them to expose more sensitive data than necessary. It should:

1. Identify the target content or behaviour reliably.
2. Offer clear categories and a concise description field.
3. Permit additional context or evidence when useful.
4. Explain emergency routes if there is immediate danger.
5. Confirm receipt and set realistic expectations.
6. Provide an accessible route to track or supplement the report where appropriate.

Prevent report abuse. A report button can itself be weaponised to mass-report a legitimate user. Apply deduplication, rate limits and abuse detection, but do not make it impossible for a victim or low-volume user to report a serious issue.

## 3. Moderation case state machine

A simple case state machine:

`submitted → deduplicated → triaged → assigned → under_review → decision_recorded → action_applied → user_notified → appeal_open/closed → archived`

Possible side states include `needs_more_information`, `legal_hold`, `escalated`, `reopened` and `system_error`. Transitions should be explicit and permission-controlled. A closed case should not silently lose its evidence or history.

Use idempotent jobs when applying actions. For example, retrying an enforcement worker should not suspend an account multiple times or send duplicate notifications. Record the actor and policy basis for every high-impact action.

## 4. Evidence handling and privacy

Evidence can contain intimate imagery, child exploitation material, personal addresses, medical information, threats or private messages. Design strict access:

- Role-based and case-based access controls.
- Just-in-time access for especially sensitive evidence.
- Audit logs of viewing, exporting and changing a case.
- Encryption at rest and in transit.
- Retention limits and legal-hold exceptions.
- Separate storage for especially sensitive evidence.
- No casual downloading to personal devices.
- Redaction or minimisation in analyst dashboards.

Do not reproduce, circulate or download illegal exploitative material for convenience. Follow legally approved escalation and evidence-handling procedures. Staff training must explain what not to access or preserve.

## 5. Decision quality and reviewer guidance

Moderators need policy examples, context guidance, escalation rules and a mechanism to ask for a second opinion. Reviewer interfaces should show only necessary context, but enough to avoid making decisions from a cropped screenshot when surrounding conversation materially changes meaning.

For high-impact decisions, consider:

- Two-person review for defined severe categories.
- Specialist escalation for legal, safety or language complexity.
- Confidence levels and uncertainty codes.
- Required rationale selection plus concise explanation.
- Calibration exercises with shared sample cases.
- Regular sampling of decisions across teams and languages.

Human decisions can also be biased or inconsistent. Measure inter-reviewer agreement, appeal outcomes and disparate error patterns; do not treat disagreement as proof that one reviewer is careless.

## 6. Enforcement ladder

Possible enforcement actions, from low to high impact:

1. Informational notice or warning.
2. Add friction (for example, confirm before sharing a potentially harmful action).
3. Limit a feature temporarily.
4. Remove or restrict specific content where justified.
5. Temporarily suspend posting, messaging or account access.
6. Require security recovery after suspected account compromise.
7. Permanently terminate an account for defined severe/repeated violations.
8. Escalate to an authorised legal or emergency channel where required.

The action should be proportionate, documented and consistent with applicable law and policy. Do not impose a penalty merely because a user has been reported many times; report volume is a signal to investigate, not proof.

## 7. Appeals and reversals

An appeal system is essential because moderation decisions are imperfect. An appeal should:

- Identify the decision and content/account involved.
- Explain how to challenge it.
- Allow the user to provide context.
- Route to a reviewer who can reconsider the decision, not simply rubber-stamp the original result.
- Preserve the original decision and record the outcome.
- Notify the user of the result and next steps, subject to legal/safety constraints.

Track appeal success and reversal reasons. High overturn rates can signal unclear policy, poor training, faulty detection or rushed decisions. A low appeal rate does not prove high accuracy; users may not know how to appeal or may not trust the process.

## 8. Emergency and law-enforcement requests

Create a documented process that routes emergency requests and legal demands to trained, authorised staff. Verify authenticity, jurisdiction, scope and legal authority. Disclose only data legally required or otherwise lawfully permitted, document the decision, and notify the user when allowed and appropriate. Do not let ordinary moderators improvise legal interpretation.

Emergency procedures should identify who is on call, which systems can preserve relevant records, which approvals are required and how to contact local authorities or qualified counsel. Cross-border requests can involve conflicts of law and require specialist legal review.

## 9. Moderator operations and wellbeing

Moderation work can expose people to disturbing material and sustained pressure. Operational controls include:

- Limit exposure to graphic material; use previews and warnings where possible.
- Provide wellbeing breaks and realistic queue targets.
- Offer confidential support and escalation after traumatic incidents.
- Rotate high-exposure work where practical.
- Provide training and supervisor support.
- Measure quality and safety, not raw cases-per-hour alone.
- Make sure vendor moderators receive appropriate training and protections.

Do not shift all difficult decisions to outsourced workers while withholding policy context, support or escalation authority.

## 10. Practical operational dashboard

A useful dashboard separates volume, urgency, accuracy, outcome and workload:

| Metric | Interpretation | Common pitfall |
|---|---|---|
| New reports by category | Demand signal | More reports may reflect easier reporting, not more harm |
| P0/P1 queue age | Urgent backlog | Low queue can hide false closures |
| Median/95th-percentile time to action | Operational speed | Fast action can be wrong action |
| Appeal overturn rate | Possible decision-quality signal | Not all users appeal |
| Repeat violation | Recurrence signal | Repeat can reflect detection differences |
| Reviewer disagreement | Calibration signal | Disagreement may be policy ambiguity |
| Evidence-access audit exceptions | Privacy/security signal | Low count needs reliable audit coverage |

## 11. Exercises

1. Implement a local report workflow with states and immutable audit events.
2. Add idempotency to enforcement jobs and test retries.
3. Create an appeal path that stores a second decision separately.
4. Draft an emergency request checklist and identify legal escalation owner.
5. Build a dashboard that shows queue health without ranking moderators solely by speed.

## Further references

- Santa Clara Principles on Transparency and Accountability in Content Moderation: https://santaclaraprinciples.org/
- OECD digital safety work: https://www.oecd.org/digital/
- NIST Privacy Framework: https://www.nist.gov/privacy-framework
- NIST SP 800-61 incident response resources: https://csrc.nist.gov/pubs/sp/800/61/r2/final
