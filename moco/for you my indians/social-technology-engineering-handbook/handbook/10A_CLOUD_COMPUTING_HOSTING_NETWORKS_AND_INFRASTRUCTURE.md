# 10A — Cloud Computing, Hosting, Networks and Infrastructure

## 1. What cloud computing means

Cloud computing provides on-demand computing, storage, networking, databases and managed services through provider infrastructure. It lets a team rent capacity rather than build a private data centre. The provider operates physical facilities and portions of the stack; the customer remains responsible for correct configuration, identity, data, application security and service choices under the shared-responsibility model.

## 2. Service models

- **IaaS:** virtual machines, networks and storage; customer manages much of the operating system and application stack.
- **PaaS:** managed runtime/platform; provider manages more of the underlying platform.
- **SaaS:** complete application delivered as a service.
- **FaaS/serverless functions:** event/request-triggered compute with provider-managed execution infrastructure; limits and cold starts/quotas matter.

“Serverless” does not mean no servers. It means the provider abstracts more server management.

## 3. Deployment patterns

- **Single VM:** simple early deployment; one failure can take the service down.
- **Managed application platform:** less infrastructure management, but platform constraints and vendor dependency.
- **Containers:** package app and runtime dependencies; still need scheduling, networking, storage, updates and security.
- **Kubernetes:** orchestrates containers across nodes; powerful but brings substantial operational complexity.
- **Serverless:** useful for event-driven or variable workloads; unsuitable for every workload.

Start with the simplest platform that satisfies reliability, compliance, scaling and team capability. A small product often does not need Kubernetes.

## 4. Regions and availability zones

Cloud providers divide infrastructure into regions and often multiple fault-isolated zones. A multi-zone design can survive certain local failures but does not automatically protect against application bugs, credential compromise, data corruption or region-wide failure. Cross-region replication introduces latency, cost and data-residency/legal considerations.

Choose region(s) using user latency, legal requirements, provider service availability, disaster recovery, price and support. Do not claim “data stays in country” unless every relevant service, backup, log, support access and subprocesser path has been verified contractually and technically.

## 5. Core infrastructure components

- Compute instances/containers/functions.
- Virtual private cloud/network, subnets and route tables.
- Firewalls/security groups and network ACLs.
- Load balancers and ingress/reverse proxies.
- Managed databases and cache.
- Object storage and CDN.
- Secrets/key management.
- DNS and certificate management.
- Monitoring/logging/tracing.
- Backup and disaster recovery.

## 6. Infrastructure as code

Infrastructure as Code (IaC) defines infrastructure in version-controlled configuration. Tools such as Terraform and provider-native templates help review and reproduce environments. IaC should use remote state securely, least-privilege deployment credentials, code review, policy checks and drift detection. Never commit secrets into infrastructure files or state without understanding encryption and access controls.

## 7. Environments

Keep development, test, staging and production separate. Use separate credentials and data. Do not copy real production personal data into development unless a documented lawful and secure process allows it; use synthetic or properly anonymised data. Staging should resemble production enough to reveal deployment and integration issues.

## 8. Networking in cloud

Understand virtual networks, private/public subnets, NAT gateways, DNS, load balancers, private endpoints, egress controls and firewall rules. Databases should usually not be directly internet-accessible. Expose only required endpoints. A “private subnet” is not a substitute for application authentication or encryption.

## 9. Cloud provider selection

Evaluate:

- regions and service availability;
- data-processing terms and subprocessors;
- residency/transfer requirements;
- security certifications and audit reports;
- operational maturity and support;
- pricing model and egress;
- portability and exit plan;
- team skills and ecosystem;
- reliability history and status transparency.

AWS, Azure, Google Cloud and regional providers all have strengths and trade-offs. A managed service is not automatically cheaper or safer; compare total operating cost.

## 10. Practical lab

Deploy a small API and managed database in a test environment. Put the database on a private network, expose the app through HTTPS, store credentials in a secret manager, configure logs and backup, then destroy and recreate the environment using IaC.

## Further reading

- AWS Well-Architected: https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html
- Google Cloud Architecture Framework: https://cloud.google.com/architecture/framework
- Microsoft Azure Well-Architected Framework: https://learn.microsoft.com/en-us/azure/well-architected/
- Terraform docs: https://developer.hashicorp.com/terraform/docs
- Kubernetes concepts: https://kubernetes.io/docs/concepts/
