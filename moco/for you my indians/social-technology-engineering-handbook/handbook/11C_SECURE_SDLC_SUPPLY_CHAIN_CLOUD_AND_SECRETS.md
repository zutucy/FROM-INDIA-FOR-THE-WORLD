# 11C — Secure SDLC, software supply chain, cloud and secrets

## 1. Security belongs in the development lifecycle

If security review happens only after a feature is complete, architecture mistakes become expensive. A permission model, retention rule or vendor integration can shape the whole system. Security should therefore be part of discovery, design, implementation, review, testing, release, operation and retirement.

A Secure Software Development Lifecycle (Secure SDLC) adds security practices to the team's existing development method. A small team can begin with data inventories, abuse cases, lightweight threat modelling, safe coding standards, dependency checks, secret scanning, automated tests and an incident owner. NIST's Secure Software Development Framework (SSDF) is a useful practice reference; it is not a product certification.

## 2. Secure development stages

| Stage | Activities | Evidence |
|---|---|---|
| Discovery | Identify data classes, user harms and constraints | Data inventory, misuse cases |
| Design | Threat model, trust boundaries, least privilege | Architecture review, risk register |
| Coding | Validation, safe libraries, secure defaults | Reviews, coding rules |
| Build | Dependency/secret checks, provenance | Build logs, SBOM where useful |
| Test | SAST, DAST, API tests, manual review | Findings and triage |
| Release | Approval, signed artifacts, controlled rollout | Release record, rollback plan |
| Operate | Patch, monitor, handle reports/incidents | Alerts, runbooks |
| Retire | Revoke keys, close endpoints, remove data | Decommission checklist |

Risk-based gates matter. A change to authentication or payments needs deeper review than a harmless text adjustment. Do not create a manual approval bottleneck for every low-risk change when automated controls can handle it.

## 3. Code review and source control

Protect important branches, require appropriate reviews and automated checks, and separate production permissions. Review especially carefully code touching authentication, authorization, cryptography, data export, uploads, admin tools, moderation powers, payments, infrastructure and CI/CD.

Reviewers should ask: What input is trusted? Who can invoke this? Which data can be returned? What happens on a retry or partial failure? How will the change be monitored and reverted? Does it expand the attack surface?

## 4. Software supply-chain security

Applications depend on frameworks, transitive packages, build tools, container base images, CI actions, plugins and hosted services. A flaw in code you did not write can affect your product.

Good practices:

- Prefer maintained packages with clear ownership and release history.
- Minimize dependencies; each adds attack surface and update work.
- Use lockfiles and reproducible version selection, but keep an update process.
- Review install scripts and packages that execute code during builds.
- Scan known vulnerabilities and assess reachability/exploitability.
- Generate a Software Bill of Materials (SBOM) where useful or required.
- Verify signatures/provenance when supported.
- Protect package publishing credentials and CI tokens.
- Remove abandoned or compromised libraries.

A scanner can produce false positives and miss unknown vulnerabilities. “No findings” is not proof of security.

## 5. CI/CD as a high-value target

CI/CD can produce software deployed to all users, so protect it like production infrastructure. Prefer short-lived workload identity over static cloud keys. Grant each workflow minimum permissions. Pin and review third-party actions. Protect release environments. Isolate runners for untrusted pull requests. Separate build and deploy permissions. Log configuration changes and deployment approvals. Do not let an untrusted pull request execute code with production secrets.

Where feasible, make build artifacts identifiable and verifiable. Record source commit, dependency inputs, build identity and deployment target. Signed artifacts and provenance help answer “what exactly was deployed, and how was it built?”

## 6. Secrets lifecycle

Secrets include DB passwords, API keys, signing keys, OAuth client secrets, cloud credentials, webhook secrets and encryption keys. Never commit live secrets to Git, including private repositories. Deleting a secret from the latest commit does not remove copies from history, forks, logs or backups. Revoke and rotate any exposed secret.

Use a managed secret store or protected environment variables with strict permissions. Separate development, staging and production. Prefer short-lived identity. Keep cryptographic keys in a key-management service where appropriate. Record owner, purpose, access, rotation and revocation procedure. Avoid printing secrets in logs or shell traces.

## 7. Cloud shared responsibility

A provider secures parts of its underlying infrastructure; the customer remains responsible for how identities, data, code, access, configuration and services are used. The exact boundary varies by IaaS/PaaS/SaaS.

Review public exposure, IAM roles, service accounts, buckets, database networking, backups, encryption, logs, region, support access, subprocessors, retention and deletion. Managed services still need correct configuration. Protect root/owner accounts with strong MFA and recovery controls; do not give every developer unrestricted administrator access.

## 8. Infrastructure as Code and configuration drift

IaC makes infrastructure reviewable and reproducible, but an unsafe template can replicate a mistake everywhere. Protect state files, restrict access, avoid hard-coded secrets, review plans and detect drift. Keep local development separate from production. Use synthetic data in tests unless real data use is necessary, approved and carefully minimized.

## 9. Vulnerability management and disclosure

A vulnerability programme needs an intake channel, triage, owner, deadlines, remediation, verification and communication. Findings can come from scanners, vendor advisories, researchers, penetration tests, internal reviews and incidents.

Prioritize using exposure, exploitability, data/users affected, known exploitation, privilege required, compensating controls, patch availability and business/legal impact. Define response targets by risk tier; do not invent one patch deadline for every situation.

Publish a responsible disclosure policy describing in-scope assets, safe testing boundaries and reporting contact. Do not treat good-faith reporting as permission to access customer data or disrupt services. A bug bounty, if used, needs clear scope, duplicate handling, disclosure terms and operational ownership.

## 10. Secure release and rollback

A release should have an identifiable artifact, owner, tests, migration plan, rollout strategy, health checks, alerts and rollback/forward-fix procedure. Database changes may make binary rollback unsafe, so prefer backwards-compatible migrations and expand-contract patterns. Feature flags help limit exposure but must not be used as authorization controls.

## 11. Practical lab

In a repository you own: protect the main branch, require tests, enable dependency and secret scanning, use least-privilege CI permissions, protect the production deployment environment, record deployed commit identity and practice a rollback. Use disposable cloud accounts and no live credentials.

## Sources

- NIST SSDF SP 800-218: https://csrc.nist.gov/pubs/sp/800/218/final
- CISA Secure by Design: https://www.cisa.gov/securebydesign
- SLSA framework: https://slsa.dev/
- OpenSSF Scorecard: https://securityscorecards.dev/
- OWASP SAMM: https://owaspsamm.org/
- GitHub code security: https://docs.github.com/en/code-security
- AWS shared responsibility: https://aws.amazon.com/compliance/shared-responsibility-model/
