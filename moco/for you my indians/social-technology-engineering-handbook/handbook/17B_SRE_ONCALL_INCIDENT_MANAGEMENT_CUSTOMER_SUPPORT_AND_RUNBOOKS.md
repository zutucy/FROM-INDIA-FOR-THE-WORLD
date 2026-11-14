# 17B — SRE, On-Call, Incident Management, Customer Support and Runbooks

**Edition:** 13 November 2026  
**Purpose:** Explain how a technology service is operated after launch: monitoring, alerting, on-call, incidents, customer communication, postmortems, support queues and operational documentation.

## 1. Build operations into the product

A service is not finished when code is deployed. It is an ongoing promise that a user can perform important tasks reliably and safely. Operational ownership includes infrastructure, application health, data correctness, customer support, security, privacy and trust/safety escalations.

Define service owners before launch. Every critical dependency should have an owner, escalation route and documented recovery procedure.

## 2. Logs, metrics and traces

- **Logs** describe events and context. Use structured fields such as timestamp, service, environment, request ID, severity and safe error code. Do not log passwords, access tokens, private message bodies or unnecessary personal data.
- **Metrics** are numeric time-series measurements such as request rate, error rate, latency histogram, CPU, memory and queue age.
- **Traces** show a request's path across services and where time is spent.

Together these support observability, but they do not replace product analytics or user research. Set retention and access controls for telemetry; logs can contain personal data.

## 3. Alert design

An alert should mean a human needs to act. Avoid alerting on every transient error. Good alerts are tied to user impact, SLO burn, severe security signals or rapidly worsening dependencies.

A useful alert includes:

- What is broken and who is affected.
- Severity and likely user impact.
- First diagnostic steps.
- Link to dashboard and runbook.
- Owning team and escalation path.
- When to page versus create a ticket.

Tune alerts to reduce noise. A team that receives hundreds of low-value pages will eventually miss an important one.

## 4. Incident roles and process

During a major incident, define:

- Incident commander: coordinates actions and priorities.
- Operations lead: drives technical diagnosis and recovery.
- Communications lead: prepares internal/customer updates.
- Subject-matter experts: handle database, network, security, payments, moderation or privacy issues.
- Scribe: records timeline, decisions and evidence.

A basic process:

1. Detect and declare.
2. Assess impact and assign severity.
3. Contain or mitigate.
4. Communicate status without speculation.
5. Restore service safely.
6. Verify recovery using user-facing signals.
7. Preserve evidence if security/privacy incident is suspected.
8. Conduct a blameless post-incident review.
9. Track corrective actions to completion.

Do not delay containment while looking for a perfect root cause. At the same time, do not destroy evidence or data needed for a security investigation.

## 5. Incident severity

Example severity framework:

- **SEV-0:** immediate severe safety/security impact or broad catastrophic failure.
- **SEV-1:** major critical user journey unavailable or material data/privacy risk.
- **SEV-2:** partial degradation with workaround.
- **SEV-3:** limited issue with low impact.

Define specific criteria and decision authority. Severity may rise or fall as evidence changes. Security and trust/safety incidents may need separate specialised classifications and notification rules.

## 6. Runbooks

A runbook should be executable by an on-call engineer who did not write the service. Include:

- Purpose and scope.
- Symptoms and alerts.
- Preconditions and permissions.
- Safe diagnostic commands/queries.
- Decision tree.
- Mitigation steps and risks.
- Verification steps.
- Rollback or recovery.
- Escalation contacts.
- Evidence and communication requirements.
- Last-reviewed date and owner.

Never store production secrets in runbooks. Link to an approved secret manager or access procedure.

## 7. Common runbooks to prepare

- API error-rate spike.
- Database connection exhaustion.
- Database failover and recovery.
- Queue backlog growth.
- Object storage upload failures.
- CDN cache poisoning or stale/private content incident.
- Login/OTP provider outage.
- Suspected account takeover campaign.
- Secret or signing-key exposure.
- Data deletion or export failure.
- Moderation queue overload.
- Third-party payment/webhook outage.

## 8. Customer support as a system

Support is not an informal mailbox. It needs:

- Ticket intake and identity verification.
- Categories and severity.
- Service-level targets that match actual staffing.
- Escalation to engineering, privacy, security, legal or safety teams.
- Knowledge base and known-issue page.
- User communication templates.
- Refund, account recovery and data-request procedures where relevant.
- Audit trail and access restrictions.

Support agents should see only the data required to resolve their case. Do not ask users to send passwords, one-time codes or full payment credentials. Make account recovery resistant to social engineering.

## 9. Postmortems and learning

A blameless review explains system conditions, not just the last person who touched the code. Include impact, detection time, response timeline, contributing factors, what worked, what failed and prioritised actions. An action should have an owner, due date and measurable completion criteria.

Avoid generic actions such as “be more careful.” Prefer engineering changes such as rate-limited migration tooling, canary analysis, backup restore drills, alert coverage or safer defaults.

## 10. Exercises

1. Write a runbook for a queue backlog.
2. Simulate a production incident in staging and assign roles.
3. Draft a customer update that clearly separates known facts from investigation.
4. Conduct a restore drill and compare actual recovery time with RTO.
5. Review logs for unnecessary personal data and remove it.

## Further references

- Google SRE books: https://sre.google/books/
- Google SRE Workbook: https://sre.google/workbook/table-of-contents/
- NIST SP 800-61 incident response: https://csrc.nist.gov/pubs/sp/800/61/r2/final
- OpenTelemetry: https://opentelemetry.io/docs/
- Atlassian incident management guide: https://www.atlassian.com/incident-management
