# 17C — Team Design, Hiring, Vendors, Governance and Working Practices

**Edition:** 13 November 2026  
**Purpose:** Show how a software product team is organised, how responsibilities grow with product scale, and how to manage employees, contractors, suppliers and governance.

## 1. Organise around outcomes and ownership

A small team should not copy the org chart of a global technology company. Start with clear responsibilities, then add specialist roles when workload and risk justify them.

For an early product, a founder may cover product direction; one or more engineers may cover frontend/backend; a designer may be part-time; infrastructure, legal, security and accounting may use qualified external support. The same person can hold multiple responsibilities initially, but accountability must still be explicit.

A responsibility map should answer:

- Who owns product scope and priority?
- Who approves production releases?
- Who owns cloud access and security?
- Who handles user reports and appeals?
- Who approves privacy and data-processing changes?
- Who responds to incidents outside business hours?
- Who controls spending and supplier renewals?

## 2. Team structures as complexity grows

Common groups include:

- Product management and research.
- Design and accessibility.
- Frontend/web and mobile engineering.
- Backend/platform engineering.
- Data engineering and analytics.
- ML/AI engineering.
- Infrastructure/SRE.
- Security/privacy engineering.
- QA/test engineering.
- Trust and safety operations.
- Customer support and community operations.
- Legal, finance, HR and partnerships.

A startup may combine roles or outsource some work. A large organisation may split by product surface, platform capability, geography or customer segment. The key is to avoid unowned shared systems and unclear escalation paths.

## 3. Hiring for evidence, not buzzwords

A useful hiring process:

1. Define the work outcome and seniority.
2. Write realistic responsibilities and expectations.
3. Use structured interviews with consistent criteria.
4. Evaluate job-relevant skills through practical discussion or work samples.
5. Avoid unpaid production work disguised as an interview.
6. Check references consistently and lawfully.
7. Explain compensation, ownership, work location and contract terms clearly.
8. Provide onboarding, access controls and a review period.

For engineering candidates, assess problem-solving, code quality, debugging, trade-offs, security awareness, collaboration and ability to explain uncertainty. Do not equate typing speed or memorised trivia with engineering competence.

## 4. Founder and employee agreements

Commercial and legal structures differ by country. Common topics to review with qualified counsel include:

- Role, compensation and payment timing.
- Equity/share options, vesting and dilution where applicable.
- Intellectual property assignment and pre-existing work.
- Confidentiality and data handling.
- Security obligations and incident reporting.
- Termination, notice and handover.
- Conflict of interest and outside work.
- Dispute resolution and governing law.

Do not assume a contractor agreement automatically transfers every IP right in every jurisdiction. Ensure the correct legal entity owns or has licensed the code, designs, domains, datasets and brand assets.

## 5. Vendor and third-party management

Products depend on cloud hosts, email/OTP providers, analytics SDKs, payment processors, support tools, AI APIs, media services and contractors. Each vendor can become a security, privacy, reliability and business-continuity dependency.

Maintain a vendor register with:

- Service and purpose.
- Data received and sensitivity.
- Hosting/processing regions.
- Subprocessors.
- Access model and authentication.
- Security assurance and incident commitments.
- Contract/DPA terms.
- Retention/deletion process.
- Availability and support targets.
- Exit plan and portability.
- Owner and review date.

Do not select a vendor based only on a free tier. Consider lock-in, export ability, data portability, outage history, support and future price changes.

## 6. Governance and decision records

Useful lightweight governance documents:

- Architecture Decision Records (ADR): context, options, decision and consequences.
- Risk register: risk, likelihood, impact, owner and mitigation.
- Data inventory and processing map.
- Access review and privileged-role register.
- Incident and change logs.
- Vendor inventory.
- Release approvals and rollback record.
- Policy version history.
- Budget and forecast.

Governance is not paperwork for its own sake. It makes important decisions reviewable, especially after team members leave or an incident occurs.

## 7. Access and offboarding

Use individual accounts, MFA, least privilege and time-bounded access. Avoid shared admin credentials. Joiner/mover/leaver processes should include device access, source code, cloud roles, password vault, support dashboard, data exports, domains, signing keys and vendor consoles.

On offboarding, revoke credentials promptly, transfer ownership of repositories and billing, rotate shared secrets where necessary and preserve work records according to policy and law.

## 8. Team health and sustainable pace

A team that depends on one exhausted engineer is a reliability risk. Avoid normalising permanent emergency work. Use code review, documentation, pairing, reasonable on-call rotation, training and clear priorities. Measure outcomes and quality, not lines of code or online hours.

For trust/safety operations, consider secondary trauma, exposure to harmful material, safe staffing and escalation support. For globally distributed teams, account for time zones, language access and local employment law.

## 9. Exercises

1. Build a RACI chart for a five-person startup.
2. Create a vendor register for cloud hosting, analytics, email and AI services.
3. Write an architecture decision record comparing modular monolith and microservices.
4. Draft a joiner/mover/leaver checklist.
5. Identify single-person dependencies and design backup ownership.

## Further references

- NIST Cybersecurity Framework 2.0: https://www.nist.gov/cyberframework
- NIST Supply Chain Risk Management resources: https://csrc.nist.gov/projects/cyber-supply-chain-risk-management
- GitHub security best practices: https://docs.github.com/en/code-security
- OWASP Software Assurance Maturity Model: https://owaspsamm.org/
