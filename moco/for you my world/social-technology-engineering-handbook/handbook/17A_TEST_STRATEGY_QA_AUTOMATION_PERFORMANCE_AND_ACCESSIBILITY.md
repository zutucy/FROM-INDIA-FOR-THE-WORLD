# 17A — Test Strategy, QA, Automation, Performance and Accessibility

**Edition:** 13 November 2026  
**Purpose:** Build confidence that software behaves correctly, securely and accessibly before and after release. Testing is a risk-management activity, not merely a last step before deployment.

## 1. Quality means more than “no visible bug”

Software quality includes functional correctness, reliability, security, performance, accessibility, compatibility, usability, maintainability, privacy and operational supportability. A feature may pass a happy-path test and still fail badly when a user has slow internet, an expired session, an unusual screen reader, an old mobile version or a duplicated request.

Start by identifying the product's critical user journeys and the harm caused by failure. A payment, account recovery, private message, content deletion and admin permission change deserve stronger testing than a cosmetic animation.

## 2. The test pyramid and its limitations

A useful starting model:

- **Unit tests:** verify small functions or modules quickly.
- **Integration tests:** verify interactions with a real or controlled database, queue, storage service or API.
- **Contract tests:** verify expectations between independently developed services.
- **End-to-end tests:** exercise important journeys through the user interface and backend.
- **Exploratory tests:** humans investigate unexpected behaviour and usability.
- **Non-functional tests:** performance, security, reliability, accessibility, compatibility and recovery.

A pyramid is not a rule that every project must use exact percentages. The correct balance depends on system complexity and failure cost. A brittle collection of UI tests can slow releases without providing much confidence; a suite of isolated unit tests can miss integration failures.

## 3. Requirements should be testable

Weak requirement: “The feed should be fast.”

Testable requirement: “For the defined representative dataset and target region, the first useful feed response should meet the agreed p95 latency target under a specified load, excluding documented client-network conditions.”

A useful acceptance criterion states:

- Starting state and user permission.
- Input and action.
- Expected result.
- Error/edge cases.
- Observability signal.
- Privacy and security expectations.

## 4. Unit and integration testing

Unit tests should cover business rules and edge cases: permissions, validation, visibility, state transitions, quota calculations and ranking filters. Use deterministic clocks, seeded randomness or dependency injection where relevant so tests are repeatable.

Integration tests should verify actual boundaries: database constraints, transaction behaviour, cache invalidation, queue delivery, signed URL creation and third-party provider failure. Keep test data isolated. Never point automated tests at production data or production accounts without explicit controlled authorisation.

## 5. End-to-end testing

Prioritise journeys that matter most:

1. New user registration, email verification and recovery.
2. Login, logout, session revocation and account security.
3. Create/edit/delete content with privacy settings.
4. Upload and playback of media.
5. Search, pagination and empty states.
6. Reporting, blocking and appeal.
7. Payment/subscription flows if present.
8. Admin role separation and audit trail.
9. Data export/deletion request.

Test both success and failure. Examples: upload interrupted midway, duplicate button click, API timeout after a committed write, expired token, blocked user, missing image, stale browser tab and database unavailable.

## 6. Performance and load testing

Know what each test answers:

- **Load test:** expected workload over time.
- **Stress test:** push beyond expected capacity to learn failure behaviour.
- **Spike test:** sudden sharp increase.
- **Soak test:** long-duration load that can reveal leaks or gradual degradation.
- **Capacity test:** identify sustainable workload and bottlenecks.

Before testing, define workload assumptions: concurrent users, request mix, think time, payload size, region, data size, cache hit rate and ramp profile. A test with only repeated requests to one cached endpoint is not representative of a production social or SaaS workload.

Measure latency distribution, throughput, errors, resource utilisation, database connections, queue age and cost. p95/p99 values reveal slow-tail behaviour that averages can hide.

## 7. Security testing

Security testing can include static analysis (SAST), dependency analysis, secret scanning, dynamic testing (DAST), container/IaC scanning, manual code review, threat-model review and authorised penetration testing. Automated tools produce findings that need triage; they do not certify a system as secure.

Define scope and permission before a penetration test. Use a written rules-of-engagement document with domains, IPs, test windows, allowed techniques, rate limits, data handling, emergency contacts and stop conditions. Never scan or exploit third-party systems without explicit authorisation.

## 8. Accessibility and inclusive testing

Test semantic HTML, keyboard-only interaction, visible focus, form labels, error announcements, headings, contrast, zoom/reflow, captions, transcripts and screen-reader behaviour. Use both automated checks and manual testing; automation catches only a subset of accessibility barriers.

Test with different devices, input methods, language lengths, right-to-left layouts, low bandwidth and reduced-motion settings. Include disabled users and assistive-technology specialists in research where possible and compensate participants appropriately.

## 9. Compatibility matrix

Define a supported matrix rather than claiming support for “all devices.” Consider:

- Browser and version families.
- Desktop/mobile OS versions.
- Screen sizes and zoom.
- Network quality and data caps.
- Low-memory devices.
- Language/locale.
- Accessibility settings.
- Old mobile app versions still in circulation.

Use analytics to understand real client distribution, but do not collect more device data than necessary.

## 10. Release gate

A release should not ship just because a developer says “works on my machine.” Define gates such as:

- Required unit/integration/E2E tests pass.
- No unresolved critical security findings.
- Accessibility review complete for affected critical paths.
- Migration tested against realistic data.
- Backup/restore impact understood.
- Monitoring and alert ownership assigned.
- Rollback/forward-fix procedure written.
- Product, support and moderation teams informed.
- Feature flag and staged rollout configured where appropriate.

## 11. Useful tools

Examples include Playwright for browser automation, Vitest/Jest for tests, pytest for Python, k6 for load testing, OWASP ZAP for authorised DAST, axe tooling for accessibility checks, and OpenTelemetry-compatible monitoring. Tool choice should follow language, architecture and team capability; adding tools without ownership creates noise.

## 12. Exercises

1. Create a test matrix for signup, login, password reset and session revocation.
2. Write a test for a private resource that tries access as owner, follower, blocked account and anonymous visitor.
3. Simulate an API timeout after database commit and verify idempotency.
4. Build a load test with a realistic request mix and report p50/p95/p99.
5. Complete a keyboard-only test of the critical onboarding flow.
6. Draft rules of engagement for an authorised test environment.

## Further references

- ISTQB glossary and testing concepts: https://glossary.istqb.org/
- Playwright documentation: https://playwright.dev/docs/intro
- k6 documentation: https://grafana.com/docs/k6/latest/
- OWASP Testing Guide: https://owasp.org/www-project-web-security-testing-guide/
- W3C Web Accessibility Initiative: https://www.w3.org/WAI/
- axe accessibility tools: https://www.deque.com/axe/
