# 10C — Observability, Reliability, Incidents and Infrastructure Costs

## 1. Monitoring vs observability

Monitoring checks known conditions through metrics, dashboards and alerts. Observability helps investigate unknown system behaviour using correlated telemetry. The three common telemetry types are metrics, logs and traces.

- **Metrics:** numeric time series (request rate, error rate, CPU, queue depth).
- **Logs:** timestamped event records with context.
- **Traces:** end-to-end request paths across services, with spans and timing.

Use correlation/request IDs to connect a user-visible failure to relevant server activity. Do not put passwords, access tokens or private message bodies into telemetry.

## 2. Service Level Indicators, Objectives and Agreements

- **SLI:** measured indicator, such as successful requests or latency.
- **SLO:** internal reliability target over a time window.
- **SLA:** external contractual commitment with defined terms/remedies.

An example SLI is the percentage of eligible API requests completed successfully within a latency threshold over 28 days. Define exclusions carefully. Do not declare an SLA simply because a dashboard has a percentage.

## 3. Error budgets

If an SLO allows a small amount of failure, the remaining error budget helps decide how much release risk the team can take. When the budget is exhausted, a team may prioritise reliability over new features. This is a governance tool, not a substitute for engineering judgement.

## 4. Useful alerts

Alert on user impact or actionable symptoms:

- sudden high error rate;
- p95/p99 latency above SLO;
- database saturation or connection exhaustion;
- queue backlog increasing faster than workers drain it;
- upload/playback failure rate;
- backup job failure;
- certificate expiry;
- unusual authentication failures;
- storage approaching quota.

Avoid alerting on every CPU fluctuation. An alert should say what is wrong, impact, relevant dashboard/runbook and who responds.

## 5. Incident response

A practical incident process:

1. Detect and acknowledge.
2. Assign incident commander/technical lead as appropriate.
3. Establish scope and user impact.
4. Stabilise/mitigate first.
5. Preserve useful evidence and logs.
6. Communicate internally and to affected users when required.
7. Recover and verify.
8. Conduct a blameless review focused on system causes.
9. Track corrective actions with owners and due dates.

Security incidents may trigger legal/regulatory reporting deadlines. Keep a separate privacy/security incident procedure and involve counsel/compliance leads promptly.

## 6. Reliability engineering

Common failure modes include: one database, a single region, expired certificates, exhausted connection pools, queue pile-ups, cache outage, dependency outage, bad deployment, traffic spike, storage quota, DNS misconfiguration and compromised credentials.

Design graceful degradation. If recommendations fail, show a basic chronological feed. If email provider is down, retain durable jobs and retry. If cache fails, protect the database from a sudden thundering herd. Define timeouts, retries with exponential backoff and jitter, circuit breakers where appropriate, bulkheads and load shedding.

Retries can amplify an outage. Use bounded retries, idempotency and queue back-pressure. Never retry every failed request forever.

## 7. Capacity planning and load testing

Measure workload shape: requests per second, concurrency, bytes per request, read/write ratio, media minutes, background jobs and geographic distribution. Use representative datasets and traffic patterns. A single benchmark number does not predict production performance.

Test normal load, expected peak, sudden burst, long soak and dependency failure. Keep load tests authorised and controlled; do not point them at third-party services without permission.

## 8. Cost engineering

Track cost by service, environment, region, product feature and unit of usage. Useful unit costs:

- cost per active user/month;
- cost per uploaded GB;
- cost per watched minute;
- cost per 1,000 notifications;
- cost per search query;
- cost per processed video minute.

Watch storage growth, egress, logs, snapshots, idle environments, NAT/managed service fees, unused disks and request volume. Build budget alerts, but remember alerts may arrive after the spend. Use quotas and limits to protect against runaway workloads.

## 9. Runbooks

A runbook should state symptoms, impact, initial checks, safe diagnostic commands, mitigation, escalation, rollback constraints and verification. Keep commands safe and tested. Restrict production access and record high-impact actions.

## 10. Practical lab

Instrument an API with metrics, logs and traces. Define an availability and latency SLO. Create an alert for elevated 5xx responses. Simulate a slow database in a local environment, observe the trace, mitigate and write a post-incident review with actionable tasks.

## Further reading

- Google SRE Book: https://sre.google/sre-book/table-of-contents/
- OpenTelemetry: https://opentelemetry.io/docs/
- Prometheus: https://prometheus.io/docs/introduction/overview/
- Grafana: https://grafana.com/docs/
- AWS Well-Architected Reliability Pillar: https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/welcome.html
