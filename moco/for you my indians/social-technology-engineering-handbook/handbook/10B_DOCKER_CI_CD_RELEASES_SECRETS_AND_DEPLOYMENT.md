# 10B — Docker, CI/CD, Releases, Secrets and Deployment

## 1. Reproducible software delivery

A developer's laptop may contain libraries and configuration that production does not. A reproducible build aims to make the deployed artifact traceable to source, dependencies and build steps. Lock dependency versions, review updates, generate software bills of materials (SBOM) where appropriate and retain build provenance.

## 2. Containers and Docker

A container packages an application and its userspace dependencies while sharing the host kernel. It is not the same as a full virtual machine. A Docker image is a layered template; a container is a running instance.

Good container practices:

- use minimal maintained base images;
- pin versions and update deliberately;
- run as a non-root user;
- copy only necessary files;
- use multi-stage builds;
- scan dependencies and images;
- do not embed secrets in image layers;
- set CPU/memory limits;
- use read-only filesystem where practical;
- handle SIGTERM and graceful shutdown.

## 3. CI and CD

**Continuous Integration (CI)** runs checks when code changes: formatting, lint, type checking, unit tests, integration tests, dependency/security scans and builds.

**Continuous Delivery/Deployment** automates preparing or releasing verified artifacts. A pipeline may:

1. check out exact commit;
2. install locked dependencies;
3. run tests and security checks;
4. build immutable artifact/image;
5. sign/attest artifact where appropriate;
6. deploy to staging;
7. run smoke tests;
8. approve production release if required;
9. deploy gradually;
10. verify health and roll back if necessary.

A green pipeline is evidence of checks passing, not proof of zero bugs.

## 4. Branching and code review

Use short-lived feature branches or trunk-based development with protected main branch. Pull requests should explain purpose, risks, testing and migration needs. Review security-sensitive changes carefully. Avoid giant branches that diverge for months.

## 5. Release strategies

- **Rolling deployment:** replace instances gradually.
- **Blue/green:** run old and new environments, switch traffic after validation.
- **Canary:** send a small portion of traffic to a new version, monitor and expand.
- **Feature flag:** deploy code but enable a feature for selected cohorts.

Choose by system architecture and risk. Stateful workloads and database changes need special planning. Rollback may not safely reverse a destructive database migration.

## 6. Database migration during deploy

Use expand-and-contract:

1. add new compatible structures;
2. deploy code that supports both old and new;
3. migrate/backfill data;
4. switch reads/writes;
5. observe and verify;
6. remove old structures later.

Run migrations with controlled permissions and clear failure recovery. Do not make every app instance race to run production migrations at startup.

## 7. Secrets management

Secrets include database passwords, signing keys, API tokens, webhook secrets and cloud credentials. Use a secret manager or protected deployment secret store. Apply least privilege and rotation. Avoid printing secrets in logs, command histories, CI output, screenshots or exception messages. Separate production secrets from test credentials. When a secret is exposed, revoke/rotate it and investigate use; deleting it from Git history is not enough.

## 8. Software supply-chain security

Dependencies can be vulnerable, compromised or abandoned. Use lockfiles, dependency review, automated vulnerability alerts, trusted registries, minimal permissions, signed artifacts and controlled build runners. Avoid installing random packages into production. Maintain an inventory of direct and transitive dependencies and a process for emergency updates.

## 9. Rollback and incident readiness

Every release should have:

- owner and change summary;
- artifact/commit identity;
- deployment and migration steps;
- smoke tests;
- dashboards/alerts to watch;
- rollback or mitigation path;
- customer impact assessment;
- incident communication route.

A rollback is not always the right choice if data schema or external side effects changed. Sometimes a forward fix is safer.

## 10. Practical lab

Create a Dockerfile for an API. Add CI that runs lint, type checks and tests. Build an immutable image, deploy to staging, run smoke tests and use a feature flag to enable a new endpoint for a test account. Rotate a test secret and verify the old value no longer works.

## Further reading

- Docker docs: https://docs.docker.com/
- GitHub Actions: https://docs.github.com/actions
- SLSA framework: https://slsa.dev/
- OWASP CI/CD Security Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/CI_CD_Security_Cheat_Sheet.html
- NIST SSDF: https://csrc.nist.gov/Projects/ssdf
