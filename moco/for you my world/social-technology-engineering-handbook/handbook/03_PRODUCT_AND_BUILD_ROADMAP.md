# Part 03 — Product Strategy and the Complete Build Roadmap

**Handbook:** Social & Technology Engineering Handbook  
**Chapter:** Part 03  
**Edition:** English 1.0  
**Research and planning snapshot:** 13 November 2026  
**Prerequisites:** Parts 00, 01 and 02  
**Next:** Part 04A — Computer Hardware

---

## Chapter purpose

This chapter explains how to turn a social-platform idea into a testable product plan. It covers the decisions that should be made before coding: whose problem the product will solve, why people would join, what belongs in the first release, how requirements should be written, how to choose an architecture, how to organise a team, how to plan for international users and how to improve the product after launch.

Keep one principle in mind:

> **A social platform does not succeed because it has the largest number of features. It must solve a real user problem, give people a reason to return and operate safely, reliably and sustainably.**

The objective is not to copy every feature from Instagram, YouTube and X in the first release. The objective is to build a focused product that is genuinely useful to a small audience, then expand according to evidence.

## Chapter map

1. The difference between an idea, a product and a platform.
2. Product-strategy lessons from social-platform history.
3. Choosing target users and an initial market.
4. Problem discovery and user research.
5. Competitor and substitute analysis.
6. Product thesis and differentiation.
7. MVP versus a complete platform.
8. Requirements: PRDs, user stories and acceptance criteria.
9. Feature prioritisation.
10. User journeys and UX planning.
11. Architecture planning before coding.
12. Technology selection without hype.
13. Security, privacy and safety from day one.
14. Worldwide product planning.
15. Team and responsibility model.
16. Development workflow and quality gates.
17. Alpha, beta and public launch.
18. Post-launch operations and improvement.
19. Costs, business model and sustainability.
20. Risk register.
21. Practical build sequence.
22. Copy-ready planning templates.
23. Exercises.
24. Glossary.
25. Further reading.

# 1. The difference between an idea, a product and a platform

These three terms do not mean the same thing.

- **Idea:** “I will build an app like Instagram, YouTube and X.”
- **Product:** “Creators will get a service for displaying their work, discovering collaborators and organising project conversations.”
- **Platform:** The product plus its users, creators, content, relationships, rules, trust systems, integrations, distribution and business operations form a connected ecosystem.

To turn an idea into a product, answer five questions:

1. Who exactly is the user?
2. Which real problem does that user have?
3. How does the user solve it today?
4. What is missing from the existing solution?
5. Why would the product be sufficiently better or different for the user to switch?

If the fifth question has no strong answer, adding more features is unlikely to make the product useful. Clarify the problem and audience first.

## 1.1 Social networks have multiple sides

Social platforms are often two-sided or multi-sided ecosystems:

- **Content producers:** creators, organisations, brands, artists, streamers, journalists and communities.
- **Content consumers:** viewers, followers, fans, readers and learners.
- **Additional participants:** advertisers, paying subscribers, moderators, developers, partners and service providers.

Without creators, the audience may find little content. Without an audience, creators may have less incentive to publish. This coordination challenge is called the **cold-start problem**.

Think about cold start before writing a feature list. For example, connect photographers in one city with local businesses, or bring clips and discussions for one gaming community into a focused space. Serving a narrow community first can make the initial launch more manageable.

# 2. Product-strategy lessons from history

Part 02 covers the history of platforms in detail. The following are product lessons that can be drawn from those histories.

## 2.1 Focus a broad idea on a strong use case

Some successful products pivoted from a broad early concept or focused on one core behaviour. Instagram's early product, Burbn, contained several features. Photo sharing proved particularly promising, and the team focused the product in that direction. The lesson is not that every startup must pivot. The lesson is to observe actual user behaviour rather than treating the founder's assumptions as unquestionable.

## 2.2 A technology opportunity is not automatically a product need

Faster mobile Internet, smartphones, cameras, inexpensive storage and cloud systems made new social formats possible. Technical possibility alone does not make a feature useful. Test whether users actually use it, repeat the behaviour and receive value from it.

## 2.3 Network effects are real, but not automatic

A **network effect** occurs when a product's value can increase as relevant participants join.

For example, a messaging application may be less useful when none of a user's friends are available on it. However, not every new user benefits every other user equally. Spam accounts, fake followers and low-quality content can damage a network.

Measure healthy interactions, creator quality, trust and retention—not only the number of accounts.

## 2.4 Responsibility increases with growth

More users mean more content, reports, impersonation attempts, moderation work, data processing and potential attacks. Include safety in the initial architecture instead of postponing it until after growth.

## 2.5 Copying a feature is not differentiation

Stories, short videos, feeds, likes and hashtags are easy to describe and copy. It is much harder to give users a unique reason to choose a product. Differentiation may come from the audience, workflow, trust model, creator economics, user experience or a genuinely distinctive feature.

# 3. Choose target users and an initial market

“Everyone” is not a useful first target audience. “Everyone who uses the Internet” makes product decisions vague.

## 3.1 Examples of audience segments

| Segment | Possible need | Important product capability | Likely challenge |
|---|---|---|---|
| Photographers | Portfolio, discovery and client enquiries | High-quality galleries, categories and contact controls | Copyright and image theft |
| Gamers | Clips, teams, events and community | Video upload, game tags and groups | Moderation and copyrighted game/music content |
| Freelancers | Work showcase and collaboration | Portfolio, verified skills and project enquiries | Scam prevention and trust |
| Musicians | Audio/video showcase and fan community | Media playback, creator profiles and rights controls | Music licensing and piracy reports |
| Educators | Learning material and discussion | Search, playlists, captions and moderation | Misinformation and child safety |
| Local communities | Local updates and connections | Language-aware discovery and community controls | Local abuse, misinformation and safety |
| General creators | Audience growth and publishing | Publishing tools, analytics and feed | Strong competition and cold start |

## 3.2 A scoring method for choosing an audience

Give each possible audience a score from 1 to 5. This score does not replace research; it helps prioritise investigation.

| Question | Score 1 | Score 5 |
|---|---|---|
| Problem intensity | Minor inconvenience | Frequent and painful problem |
| Current alternatives | Strong existing alternatives | No suitable alternative |
| Reachability | Hard to contact users | Target users are easy to reach |
| Repeat usage | Rare need | Daily or weekly recurring need |
| Content supply | Difficult to recruit initial content | Initial creators can be recruited |
| Willingness to contribute or pay | Little evidence | Clear evidence of time, effort or payment |
| Safety complexity | High risk that cannot yet be managed | Risk can be managed responsibly |
| Differentiation | No clear advantage | Specific and defensible advantage |

Do not treat the total as the final truth. Explain the evidence behind each score. If safety complexity is high, do not hide it inside an average—record the risk separately.

## 3.3 How to write a user persona

A persona should not be an imaginary marketing character. It should be a concise working model based on interviews and observation.

**Example: independent video creator**

- Creates short tutorials and behind-the-scenes videos.
- Current workflow: publishes on several applications, stores source files separately and tracks brand enquiries in email or direct messages.
- Frustration: audience is fragmented, enquiry history is hard to organise and portfolio links become outdated.
- Desired outcome: one public work profile and structured collaboration enquiries.
- Constraints: limited time, mobile-first workflow and sometimes low upload bandwidth.
- Open question: Does this creator want another social feed, or mainly a portfolio and workflow tool?

The final question is important. Do not assume that every creator wants another feed.

# 4. Problem discovery: how to speak with users

Product discovery should begin by understanding current behaviour, not by asking people to approve a feature idea.

## 4.1 Weak and stronger interview questions

| Weak question | Better question |
|---|---|
| Would you use my app? | When did this problem last happen, and what did you do? |
| Do you like this feature? | Show me how you complete this task today. |
| Would you pay ₹100? | Have you paid for a similar solution? How much and why? |
| Do you need AI? | Which step takes the most effort, and why? |
| Is this design beautiful? | What were you trying to find, and where did you get stuck? |

People may politely say that an idea sounds good. Recent behaviour, actual workarounds and real spending are stronger evidence than compliments.

## 4.2 A practical interview process

1. Select a user segment and recruit participants who genuinely fit it.
2. Explain the research purpose and ask for consent before recording or retaining personal information.
3. Ask about a recent real experience, not an imaginary future.
4. Ask the participant to describe or demonstrate the current workflow when appropriate.
5. Ask what they tried, what failed, how often the problem happens and what it costs them.
6. Avoid pitching your solution until you understand the current problem.
7. Record observations separately from your interpretation.
8. Look for repeated patterns across participants.
9. Update the problem statement and list what remains unknown.

Do not collect unnecessary sensitive personal data. Use participant codes rather than names in research notes unless identification is genuinely needed and properly consented to.

## 4.3 Evidence hierarchy

A useful way to organise evidence, from weaker to stronger, is:

1. A founder's assumption.
2. A person's general opinion.
3. A stated intention to try a future product.
4. A description of a recent real problem.
5. A demonstrated current workaround or repeated behaviour.
6. Evidence of time, effort or money already spent to solve the problem.
7. A controlled test showing repeated use or willingness to pay.

This is a practical guide, not a universal scientific ranking. The right evidence depends on the product and risk.

## 4.4 Problem-statement template

```text
For [specific user segment],
when [situation or task occurs],
[problem] makes it difficult to [desired outcome].
Today they use [current workaround],
which creates [measurable cost or frustration].
Evidence: [interviews, observations or behaviour].
Unknowns: [what still needs testing].
```

# 5. Competitor and substitute analysis

A competitor is not only another social application. A user's substitute may be a spreadsheet, a messaging group, a website, email, a physical community or simply doing nothing.

## 5.1 Dimensions to analyse

- Target audience and primary user problem.
- Main workflow and time to first value.
- Content and relationship model.
- Search, feed and discovery approach.
- Privacy, safety and account controls.
- Accessibility and language support.
- Creator tools and monetisation.
- Mobile/desktop experience and network performance.
- Pricing, advertising and business model.
- Strengths, weaknesses and user complaints.

Use the product yourself where lawful and appropriate. Read public documentation and user feedback. Do not attempt to access private competitor data or misrepresent yourself to obtain it.

## 5.2 Competitor-matrix template

| Dimension | Your proposed product | Competitor A | Competitor B | Current workaround |
|---|---|---|---|---|
| Target user | | | | |
| Main problem | | | | |
| Main workflow | | | | |
| Discovery | | | | |
| Privacy and safety | | | | |
| Cost to user | | | | |
| Key limitation | | | | |
| Evidence/source | | | | |

Do not claim that a competitor lacks a feature without checking the current product and date. Product capabilities change.

# 6. Product thesis and differentiation

A **product thesis** is a testable explanation of why a product should exist, whom it serves and what advantage it may offer.

### Weak thesis

> We will combine Instagram, YouTube and X into one application for everyone.

This statement does not explain the first user, the problem, the reason to switch or how the product will become useful before it has a large network.

### More testable thesis

> Independent creators who manage portfolios and collaboration requests across several services need one organised public work profile and a safer way to receive project enquiries. We will test this with a small group of creators and local businesses before building a broad social feed.

This thesis can be tested through interviews, a prototype and a limited pilot.

## 6.1 Dimensions of differentiation

Differentiation might come from:

- A specific underserved audience.
- A better workflow rather than more features.
- Safer or more understandable privacy controls.
- Better creator tools or fairer economics.
- Strong local-language and accessibility support.
- Better performance on low-end devices or weak connections.
- A distinctive community or trust model.
- Better integration with existing work tools.

A feature is not a durable advantage merely because it is new. Ask whether it is hard to copy, valuable to the target user and sustainable to operate.

# 7. A full platform versus an MVP

An **MVP (Minimum Viable Product)** is the smallest responsible product that can test a core value hypothesis. It is not a broken demo and does not excuse weak security, privacy or safety.

## 7.1 Three possible scopes

| Scope | Purpose | Example |
|---|---|---|
| Prototype | Test understanding and usability | Clickable profile and feed mock-up with no real user data |
| MVP | Test a core workflow with real users | Account, profile, post, follow and basic feed |
| Mature platform | Support multiple workflows and larger operations | Media pipelines, messaging, moderation operations, analytics and monetisation |

## 7.2 Suggested release stages for a general creator platform

### Release A — Core identity and content

- Sign-up, login and account recovery.
- Profile and profile editing.
- Follow/unfollow or another clearly defined relationship model.
- Basic image or text posts.
- Feed with privacy and block rules.
- Reporting, blocking and admin review basics.

### Release B — Media and discovery

- Safe image and limited video upload.
- Object storage and media processing.
- Search for users and content.
- Basic explore/discovery.
- Notifications.
- Upload progress and retry behaviour.

### Release C — Community and communication

- Comments and replies.
- Groups or topic communities if validated.
- Direct messaging with abuse controls.
- Better creator tools and analytics.
- More mature moderation and appeals.

### Release D — Advanced product

- Advanced recommendation systems.
- Creator monetisation.
- Live video or calls where justified.
- Advertisements, subscriptions or marketplace features.
- International expansion and larger-scale architecture.

These are example stages, not mandatory features. A professional network, community service or media platform may need a different order.

## 7.3 Features that should not automatically be day-one requirements

Livestreaming, advanced AI recommendations, advertising, payments, creator revenue sharing, multi-region databases, microservices and a custom ranking model can all be expensive. Build them when evidence and requirements justify them, not because large platforms have them.

# 8. Product requirements: PRDs, user stories and acceptance criteria

## 8.1 What is a PRD?

A **Product Requirements Document (PRD)** describes the user problem, expected outcome, scope, behaviour, constraints, permissions and success conditions for a feature or product.

### PRD template

```markdown
# Feature: [Name]

## 1. Problem
What user problem is being addressed? What evidence supports it?

## 2. User outcome
What should the user be able to accomplish?

## 3. Goal
What measurable outcome should improve?

## 4. Non-goals
What is deliberately out of scope?

## 5. User journey
What steps does the user follow?

## 6. Functional requirements
What must the system do?

## 7. Non-functional requirements
What quality, performance, security and reliability constraints apply?

## 8. Permissions and privacy
Who can see, create, change or delete the data?

## 9. Failure cases
What happens when the network, service or user input fails?

## 10. Analytics
Which minimal events are needed to evaluate the feature?

## 11. Acceptance criteria
What observable tests prove that the work is complete?

## 12. Dependencies
Which teams, systems, vendors or approvals are required?

## 13. Rollout and rollback
How is the feature enabled, monitored and disabled if necessary?

## 14. Open questions and decision log
What remains uncertain, and who owns each decision?
```

## 8.2 Functional versus non-functional requirements

- **Functional requirement:** What the system must do. Example: a user can create a post with a caption and an image.
- **Non-functional requirement:** A quality or constraint. Example: a feed request should meet a defined latency target under an agreed test load, or private posts must never be returned to unauthorised users.

Non-functional requirements should be measurable where possible. “Fast” and “secure” are not testable until the team defines scenarios and thresholds.

## 8.3 User-story format

A common format is:

> As a [type of user], I want [capability], so that [benefit].

Example:

> As a creator, I want to make a post visible only to approved followers, so that I can share work with a limited audience.

A user story is not a complete specification by itself. It needs acceptance criteria, permissions, failure cases and accessibility considerations.

## 8.4 Acceptance-criteria example: private post

- The owner can select the intended visibility.
- Unauthorised visitors cannot retrieve the post through the UI or API.
- A user who is blocked cannot access content through direct URLs or alternate API calls.
- Search and recommendation systems do not expose the private post to ineligible users.
- Media URLs do not bypass the post's access rules.
- Tests verify both allowed and denied cases.

# 9. Feature prioritisation

A team has limited time and capacity. Prioritisation makes trade-offs explicit.

## 9.1 MoSCoW method

- **Must have:** Required for the core product or safe operation.
- **Should have:** Important, but a short-term workaround may exist.
- **Could have:** Useful if capacity remains.
- **Won't have now:** Explicitly deferred from this release.

Do not put a feature into “Must” merely because a competitor has it. Security, privacy, accessibility and legal obligations may be must-haves even when they are not visible features.

## 9.2 RICE method

RICE commonly stands for Reach, Impact, Confidence and Effort. A simplified score is:

\[
RICE = \frac{Reach \times Impact \times Confidence}{Effort}
\]

The team must define the time period and scoring scale. RICE supports comparison; it does not replace judgement. A high score does not override a legal duty, severe safety risk or critical reliability issue.

## 9.3 Safety and compliance can override feature scores

A feature with a low growth score may still be mandatory if it protects users or meets an applicable obligation. Examples include account deletion, reporting, access control, security logging and a grievance process.

# 10. User journeys and UX planning

## 10.1 Example: a new creator joins

1. The creator sees a clear explanation of the product.
2. The creator reviews the privacy and community rules.
3. The creator signs up using a supported method.
4. The product asks only for necessary profile information.
5. The creator chooses visibility and notification preferences.
6. The creator publishes or imports an initial work sample if supported.
7. The product explains how discovery works.
8. The creator can report a problem, block an account or find help.

Measure where users abandon the process. Do not collect unnecessary personal information merely to make the onboarding screen look complete.

## 10.2 Empty states

An empty state appears when there is no content, no search result, no notification or no conversation yet. It should explain what happened and offer a useful next action. It should not mislead the user into granting contacts, location or other permissions without a clear need.

## 10.3 Accessibility from the beginning

Plan for keyboard navigation, screen readers, text alternatives, captions, sufficient contrast, clear focus states, reduced motion and understandable error messages. Accessibility is not a final visual polish task; it affects the underlying components and content model.

# 11. Plan architecture before coding

## 11.1 Start with a context diagram

List the people and systems that interact with the product: users, web/mobile applications, APIs, database, object storage, payment provider, email/OTP provider, analytics, moderation tools and administrators.

Draw data flows and trust boundaries. Mark where personal data, credentials, media and payment information move.

## 11.2 Modular monolith versus microservices

| Modular monolith | Microservices |
|---|---|
| One main deployable application with clear internal modules | Several independently deployed services |
| Simpler local development and transactions | Independent scaling and deployment can be useful |
| Fewer network and operational failure points | More network calls, observability and distributed failure modes |
| Good starting point for many products | Useful when organisational and technical boundaries justify it |
| Requires discipline to keep module boundaries clear | Requires service ownership, contracts and operational maturity |

A modular monolith is a sensible starting point for many small teams. Do not split into microservices merely to appear sophisticated.

## 11.3 Event-driven background work

Some actions should not wait for all secondary work to finish. A post request may save the post and enqueue jobs to create thumbnails, process media, index searchable fields and send notifications. A queue and background workers can process these tasks asynchronously.

The system must handle retries, duplicate delivery, job failure, dead-letter handling and idempotency. A user should not receive duplicate notifications or create duplicate payments because a job was retried.

## 11.4 Architecture Decision Records (ADR)

An ADR captures a significant technical decision and why it was made.

### ADR-001: Start with a modular monolith

**Context:** A small team is building an early product. Requirements are changing, and the team has limited operational capacity.

**Decision:** Use one backend application with clearly separated modules and a separate worker process where needed.

**Alternatives:** Start with many microservices; use a serverless-only architecture; use a backend-as-a-service for selected functions.

**Consequences:** Local development and deployment remain simpler. Module boundaries must be enforced through code review and tests. Some modules may later be extracted if load or team ownership justifies it.

**Revisit when:** One module needs independent scaling or release cadence, a team needs independent ownership, or a clear reliability boundary justifies separation.

# 12. Select technologies without hype

## 12.1 Example starting stack

| Layer | Example technology | Why it may fit |
|---|---|---|
| Web frontend | React + Next.js + TypeScript | Reusable UI, routing and a mature Web ecosystem |
| Backend | Node.js + NestJS or another structured framework | TypeScript across application boundaries and modular organisation |
| Main database | PostgreSQL | Relational data, transactions, constraints and mature tooling |
| Cache/queue support | Redis or a managed queue | Caching and background-work patterns when required |
| Media storage | Object storage such as S3-compatible services | Large files are stored separately from relational records |
| Media processing | FFmpeg or a managed media service | Transcoding, thumbnails and format handling |
| Search | PostgreSQL initially; dedicated search later if needed | Avoid premature infrastructure |
| Deployment | Containers and a managed cloud platform | Reproducible builds and practical operations |
| Monitoring | Error tracking and OpenTelemetry-compatible tools | Diagnose failures and measure performance |

This is one possible stack, not a universal standard. Select based on team skills, costs, service availability, security requirements and expected workload.

## 12.2 Why not use every database?

Every additional database creates operational work: backups, monitoring, schema or index design, access controls, upgrades, vendor risk and data consistency decisions. Begin with the fewest systems that meet the requirements. Add a search engine, document database, analytics warehouse or specialised store only when a measured need justifies it.

## 12.3 Build versus buy

| Capability | Build yourself when | Buy/use a managed service when |
|---|---|---|
| Email delivery | Email delivery is core differentiated capability and you have the expertise | Standard account and notification email is enough |
| Video transcoding | Media processing is strategically specialised | Standard formats and volume fit a managed service |
| Payments | You are a regulated payment provider or have a justified specialised need | A licensed provider can handle payment processing |
| Authentication | Identity is a core product capability and you can secure it properly | Standard sign-in, MFA and recovery meet your needs |
| Search | Search relevance is a differentiator | Basic search is sufficient initially |

A vendor does not remove your responsibility for user data, access control, service availability or compliance.

# 13. Put security, privacy and safety into the product plan

## 13.1 Create a basic threat model

Identify:

- Assets: accounts, credentials, private posts, messages, media, payment records and administrative access.
- Actors: normal users, abusive users, bots, insiders, attackers and vendors.
- Entry points: web/mobile apps, APIs, uploads, webhooks, admin tools and integrations.
- Trust boundaries: public-to-private, user-to-admin, application-to-storage and company-to-vendor.
- Threats: account takeover, data exposure, abuse, spam, malicious files, data corruption and service disruption.
- Controls: authentication, authorisation, validation, rate limiting, encryption, logging, moderation and recovery.

## 13.2 Security requirements for the first product brief

- Store passwords using an appropriate password-hashing algorithm; never store raw passwords.
- Enforce authorisation on the backend for every protected object and action.
- Protect sessions and provide session revocation.
- Validate all untrusted inputs and uploaded files.
- Rate-limit sensitive endpoints.
- Store secrets outside source code.
- Encrypt network traffic and protect stored data according to risk.
- Keep audit logs for sensitive administrative actions.
- Test backups and incident procedures.

## 13.3 Product safety requirements

- Reporting and blocking should be easy to find.
- Users should understand privacy and audience controls.
- Moderation actions should have clear reasons and appeal routes where appropriate.
- High-risk content and child safety need dedicated policy and operational review.
- Recommendation systems should account for negative feedback and safety eligibility, not only engagement.

## 13.4 Privacy-by-design checklist

- Collect only data needed for a defined purpose.
- Explain purposes clearly.
- Set retention and deletion rules.
- Restrict access by role and need.
- Review analytics and advertising SDKs.
- Map vendors and cross-border data flows.
- Provide appropriate access, correction, deletion and consent controls as required by applicable law.
- Avoid using private user content for unrelated training or analytics without a lawful basis and transparent user-facing explanation.

# 14. Plan for worldwide users

## 14.1 Separate five geography questions

1. Where is the company incorporated and managed?
2. Where are the users located?
3. Where do compute, databases, media and backups physically operate?
4. Where are vendors and their support staff located?
5. Which jurisdictions' laws apply to the service and data processing?

These questions are related but not interchangeable. A company incorporated in one country may serve people in many countries and use infrastructure in several others.

## 14.2 Internationalisation versus localisation

- **Internationalisation (i18n):** Design the product so it can support multiple languages, writing systems, time zones, currencies and regional formats.
- **Localisation (l10n):** Adapt the product for a specific locale, including translations, date formats, local payment methods, support and culturally appropriate UX.

Also plan for right-to-left layouts where needed, Unicode input, name formats, address formats, local holidays and region-specific content rules.

## 14.3 Global media delivery

A global service may use object storage, regional processing and CDN edge locations. Plan for:

- Uploads from slow or unstable connections.
- Resumable or multipart upload where appropriate.
- Regional delivery and cache behaviour.
- Signed access to private media.
- Data retention and deletion across replicas and backups.
- Cost and bandwidth monitoring.

## 14.4 Regional rollout strategy

Do not launch everywhere simply because the application is technically reachable. Start with a market where you understand users, can provide support, can meet legal duties and can moderate content responsibly. Expand only after local requirements and operational readiness are clear.

# 15. Team and responsibility model

Small teams may combine roles, but responsibilities must still have owners.

| Responsibility | Typical owner | Output |
|---|---|---|
| Product strategy | Founder/product lead | Product thesis, roadmap and priorities |
| UX research/design | Product designer/researcher | User journeys, prototypes and usability findings |
| Frontend | Frontend engineer | Web/mobile interface and accessibility |
| Backend | Backend engineer | APIs, business logic and database integration |
| Data | Data engineer/analyst | Event definitions, pipelines and metrics |
| Infrastructure | DevOps/SRE engineer | Deployment, monitoring and reliability |
| Security/privacy | Security/privacy owner or specialist | Threat model, controls and review |
| QA | QA engineer/team | Test strategy and release evidence |
| Trust and safety | Policy/operations team | Reports, moderation, appeals and escalation |
| Legal/finance | Qualified professionals | Legal review, accounting and tax obligations |

## 15.1 Responsibility matrix

For each critical activity, record who is **Responsible**, **Accountable**, **Consulted** and **Informed** (RACI). Avoid a situation where everyone assumes someone else owns security incidents, data deletion or moderation appeals.

# 16. Development workflow and quality gates

## 16.1 Typical lifecycle

```text
Requirement -> Design -> Branch -> Implementation -> Review
    -> Automated tests -> Staging -> Approval -> Production
    -> Monitoring -> Feedback -> Next iteration
```

## 16.2 Environments

- **Local/development:** Individual development and experiments using non-production data.
- **Test/CI:** Automated builds and repeatable tests.
- **Staging:** A production-like environment for release checks.
- **Production:** The real service and real user data.

Do not casually copy production personal data into local or test environments. Use synthetic or appropriately masked data.

## 16.3 Git branch and review process

A typical flow is:

1. Create a short-lived feature branch.
2. Make a focused change.
3. Add or update tests and documentation.
4. Open a pull request.
5. Review code, security impact and database changes.
6. Run automated checks.
7. Merge only after required approvals.
8. Deploy to staging and verify.

Avoid direct unreviewed production edits.

## 16.4 Database migrations

Use version-controlled migrations. Prefer compatible changes: add a new field, backfill data, deploy code that uses it, then remove old fields only after old code no longer depends on them. Test migrations against realistic data volumes and have a recovery plan.

## 16.5 Release quality gate

Before release, confirm:

- Requirements and acceptance tests pass.
- No known critical security issue remains unaddressed.
- Permissions and privacy rules are tested.
- Database migration and rollback/recovery plans are reviewed.
- Monitoring and alerts are active.
- Support and moderation owners are available.
- Release notes and user-facing changes are clear.

# 17. Alpha, beta and public launch

## 17.1 Internal alpha

The internal alpha is used by the core team and invited testers. Its purpose is to find broken workflows, confusing UX, basic reliability issues and security problems before wider exposure.

## 17.2 Closed beta

A closed beta includes a selected group of external users. Explain what is experimental, how feedback is collected and how data is handled. Do not use beta status as an excuse to ignore privacy or user safety.

## 17.3 Public-launch readiness

### Product

- The target audience and value proposition are clear.
- The core user journey is usable.
- Help, settings and account recovery are available.

### Engineering

- Production deployment is repeatable.
- Monitoring and alerting work.
- Backups and restore procedures have been tested.
- Capacity and cost assumptions are documented.

### Safety and operations

- Reporting, blocking and moderation are operational.
- High-risk incidents have escalation paths.
- Support and complaint channels are staffed.

### Business and legal

- Terms, privacy and community policies have been reviewed.
- Vendor contracts and data flows are understood.
- Applicable registration, tax and regulatory obligations have been checked with qualified professionals.

## 17.4 Gradual rollout

Release to a small cohort, observe error rates and product metrics, expand gradually and pause if safety or reliability worsens. Feature flags can enable or disable a feature without redeploying the entire application, provided the flag itself is controlled securely.

# 18. After launch: operate, learn and improve

## 18.1 Product metrics

Potential metrics include:

- **DAU:** Daily active users.
- **WAU:** Weekly active users.
- **MAU:** Monthly active users.
- **Activation:** Percentage of new users who complete a meaningful first action.
- **Retention:** Percentage of users who return after a defined period.
- **Churn:** Users or customers who stop using or paying.
- **Creator supply:** Active creators and useful content availability.
- **Upload success:** Percentage of uploads completed successfully.
- **Playback quality:** Startup time, buffering and completion behaviour.
- **Safety operations:** Report volume, response time, appeal outcomes and repeat abuse.

Metrics require precise definitions and privacy review. A metric can be misleading if its event definitions, time window or denominator are unclear.

## 18.2 Feedback channels

Provide in-product feedback, support email or ticketing, report flows, user interviews and periodic usability sessions. Categorise feedback and distinguish individual preference from repeated user problems.

## 18.3 Incident management

For an outage, breach or user-safety incident:

1. Assign an incident owner.
2. Assess impact and urgency.
3. Protect users and preserve evidence.
4. Contain the issue.
5. Communicate accurately to affected stakeholders.
6. Recover service or apply a safety action.
7. Meet applicable reporting and notification duties.
8. Review the cause and improve controls.

# 19. Costs, business model and sustainability

## 19.1 Cost categories

- Compute and application hosting.
- Database, cache and search.
- Object storage.
- CDN and network bandwidth.
- Video processing and transcoding.
- Email, OTP and push notifications.
- Monitoring, backups and security tools.
- Moderation, customer support and legal review.
- Salaries, contractors and product design.
- Marketing, partnerships and creator programmes.

Video products may have significant bandwidth, storage and processing costs. A text-first product has a different cost profile.

## 19.2 Cost-model variables

Estimate:

- Daily and monthly active users.
- Peak concurrent users and requests per second.
- Uploads per user and average file size.
- Media watch time and average bitrate.
- Storage retention period and replicas.
- CDN cache-hit ratio and delivered bandwidth.
- Background processing volume.
- Support and moderation workload.

### Illustrative media calculation

Suppose 10,000 active users each upload one 20 MB video in a month. Raw uploaded volume is:

\[
10{,}000 \times 20\text{ MB} = 200{,}000\text{ MB} \approx 200\text{ GB}
\]

This is only the incoming raw file volume. It excludes transcoded versions, thumbnails, replicas, backups, failed uploads and content delivered to viewers. Playback bandwidth can exceed storage growth by a large amount, depending on view counts and video bitrate.

Do not turn an illustrative calculation into a price quote. Actual cost depends on provider pricing, region, storage class, request volume, bandwidth, taxes and negotiated discounts.

## 19.3 Business models

- Advertising.
- Premium subscriptions.
- Creator subscriptions.
- Creator tools or paid features.
- Revenue-sharing programmes.
- Brand partnerships.
- Marketplace services.
- Enterprise or community plans.

Each model changes product, privacy, finance and legal requirements. Advertising can introduce tracking and consent questions. Payments introduce fraud, refund, tax and provider obligations.

## 19.4 Unit economics basics

Unit economics examines revenue and variable cost per user, customer, transaction or other defined unit. Useful questions include:

- What does it cost to acquire an active user?
- What revenue does an average paying user generate?
- What are the service costs attributable to that user?
- What is the moderation/support cost per active user?
- How long does it take to recover acquisition cost?

Do not assume that a large user count is automatically a healthy business.

# 20. Risk register

A risk register records what could go wrong, how likely it is, how severe the impact would be, who owns it and what mitigation exists.

Example categories:

- Product-market fit risk.
- Cold-start and content-supply risk.
- Infrastructure and availability risk.
- Data loss or corruption.
- Account takeover and privacy exposure.
- Child safety and harmful content.
- Copyright and intellectual-property complaints.
- Vendor outage or lock-in.
- Unexpected bandwidth or moderation costs.
- Regulatory or cross-border data-transfer failure.
- Team capacity and key-person dependency.

## 20.1 Risk severity

A simple risk matrix combines likelihood and impact. Define the scales and escalation thresholds for the team. High-impact events such as private-data exposure, child exploitation or major service compromise should not be treated as ordinary product bugs.

# 21. Practical build sequence: from zero to release

## Phase 0 — Research and product definition

Deliverables:

- Target segment and problem statement.
- User interview notes and evidence.
- Competitor/substitute matrix.
- Product thesis and initial market choice.
- Initial risk register.

Exit condition: the team can explain who the first user is, which problem is being solved and what evidence supports the decision.

## Phase 1 — Requirements and design

Deliverables:

- PRD and user stories.
- User journeys and wireframes.
- Acceptance criteria.
- Data classification and privacy map.
- Threat model and safety baseline.
- Initial architecture diagrams and ADRs.

Exit condition: developers, designers and testers understand the intended behaviour and non-goals.

## Phase 2 — Technical foundation

Deliverables:

- Repository and folder structure.
- Local development setup.
- Development, staging and production environments.
- CI workflow.
- Database schema and migrations.
- API conventions.
- Logging and error handling.
- Secrets management.

Exit condition: a small feature can be built, tested, deployed to staging and monitored safely.

## Phase 3 — Core user experience

Deliverables:

- Sign-up, login and recovery.
- Profiles.
- Privacy settings.
- Follow/block or another defined relationship model.
- Content create/view/edit/delete according to permissions.
- Basic feed.
- Likes/comments if justified.

Exit condition: a new user can complete the core journey end to end.

## Phase 4 — Media and discovery

Deliverables:

- Safe uploads.
- Object storage.
- Processing pipeline.
- CDN delivery with correct access control.
- Search and basic discovery.
- Notifications where needed.

Exit condition: media and discovery flows pass normal, failure and security tests.

## Phase 5 — Trust, safety and operations

Deliverables:

- Reporting and block/mute.
- Moderation queue and appeals.
- Admin roles and audit logs.
- Backup and restore drills.
- Incident-response runbook.
- Support and grievance workflow.
- Legal and policy review for the initial market.

Exit condition: the team can respond to common user-harm, account and operational incidents.

## Phase 6 — Alpha and beta

Deliverables:

- Realistic test plan.
- Beta cohort.
- Feedback channels.
- Analytics with privacy controls.
- Cost monitoring.
- Bug and risk prioritisation.

Exit condition: target users can repeat the core workflow and serious defects are understood and addressed.

## Phase 7 — Public launch and iteration

Deliverables:

- Rollout plan.
- Public help and policy pages.
- Monitored production deployment.
- Support ownership or rota.
- Release notes.
- Product-metric review.

Exit condition: the product has a stable operating loop for continued learning and maintenance. The application is not “finished” merely because it has launched.

# 22. Copy-ready planning templates

## 22.1 One-page product brief

```markdown
# Product brief

Name / working title:
Version / date:
Product owner:

## Target first user

## User problem

## Current alternatives

## Product promise

## Why now / why us

## First core workflow

## MVP must-haves

## Explicit non-goals

## Safety and privacy baseline

## Initial launch market(s)

## Business hypothesis

## Success metrics

## Biggest assumptions

## Next validation experiment

## Open decisions
```

## 22.2 User-interview note

```markdown
Participant code (avoid unnecessary personal identity):
Target segment:
Date / consent status:

Recent real example:
Current workflow:
Tools used:
Time / cost / frustration:
Workaround:
What happens if unresolved:
What the user values:
Direct quote (only with appropriate permission):
Researcher interpretation:
Unknowns:
Next question or test:
```

## 22.3 Feature specification

```markdown
Feature:
Problem:
User outcome:
In scope:
Out of scope:
User flow:
Functional requirements:
Permission rules:
Privacy/data fields:
Error and retry behaviour:
Accessibility:
Analytics events:
Abuse/security cases:
Acceptance criteria:
Dependencies:
Rollout/rollback:
Owner:
```

## 22.4 Weekly product/engineering review

```markdown
What shipped?
What did users actually do?
What failed?
What safety reports or patterns appeared?
What did the metrics show?
What assumptions changed?
What is the largest current risk?
What is the next most valuable task?
What are we deliberately NOT doing now?
```

# 23. Practical exercises

## Exercise A — Choose an audience

Write down three possible audiences. Score them using Section 3.2. Choose one to investigate first; do not make a permanent commitment based only on a score.

## Exercise B — Conduct discovery

Speak with several people from the chosen segment. Ask about recent real workflows. Do not pitch your idea during the first part of the conversation. Record evidence separately from assumptions.

## Exercise C — Write the product thesis

Use the Section 6 template. Keep the thesis to one paragraph and list its supporting evidence and largest risk.

## Exercise D — Define the first release

List the must-have user outcomes, safety and privacy requirements, features deliberately deferred, and measurable success criteria.

## Exercise E — Draw the architecture

Draw a context diagram, component diagram and sequence diagram for a core action such as creating a post or uploading a video. Mark trust boundaries and external vendors.

## Exercise F — Test the idea

Create a clickable prototype or a limited functional slice. Observe target users completing the task. Record where they hesitate, misunderstand or abandon it, then revise the requirements.

# 24. Glossary

| Term | Meaning |
|---|---|
| Product | A service designed to create a defined user outcome |
| Platform | Product plus users, interactions, rules, ecosystem and operations |
| Target segment | The specific user group served first |
| User persona | An evidence-based working model of a user type |
| Problem discovery | Research into real user needs and workflows |
| Product thesis | A testable statement explaining why a product should exist |
| MVP | Minimum Viable Product; the smallest responsible product for testing core value |
| PRD | Product Requirements Document |
| User story | A user-centred description of a desired capability |
| Acceptance criteria | Testable conditions that define completion |
| Functional requirement | What the system must do |
| Non-functional requirement | A quality or constraint such as speed, security or reliability |
| MoSCoW | Must, Should, Could, Won't prioritisation |
| RICE | Reach, Impact, Confidence and Effort prioritisation framework |
| Cold start | Difficulty creating value before enough users or content exist |
| Network effect | Value that can increase as relevant participants join |
| Architecture | System structure, boundaries, data flows and design decisions |
| Modular monolith | One deployable application with well-separated internal modules |
| Microservice | An independently deployable service with a bounded responsibility |
| ADR | Architecture Decision Record |
| Feature flag | Runtime control to enable or disable a feature for a cohort |
| Threat model | Structured analysis of assets, threats, entry points and controls |
| i18n | Internationalisation: designing for multiple languages and regions |
| l10n | Localisation: adapting to a particular locale |
| Alpha | Early controlled test, often internal |
| Beta | Limited test with selected external users |
| Retention | Users returning after a defined period |
| Churn | Users or customers who stop using or paying |
| SLO | Service Level Objective, a measurable reliability target |
| Unit economics | Revenue and cost per user, customer, transaction or other unit |

# 25. Further reading and references

1. [Y Combinator — Startup Library](https://www.ycombinator.com/library/) — founder-oriented material on products, users, launches and company building. Advice is not a guarantee of success.
2. [The Mom Test — Rob Fitzpatrick](https://www.momtestbook.com/) — interviewing users about actual behaviour rather than asking leading “would you use it?” questions.
3. [Nielsen Norman Group — User Research](https://www.nngroup.com/topic/user-research/) — practical research and usability methods.
4. [Atlassian — Product Requirements](https://www.atlassian.com/agile/product-management/requirements) — requirements and product documentation concepts.
5. [Atlassian — RICE prioritisation](https://www.atlassian.com/agile/product-management/prioritization-framework) — prioritisation framework overview; formula variants differ between teams.
6. [C4 Model](https://c4model.com/) — context, container, component and code-level architecture diagrams.
7. [Microsoft Azure Architecture Center](https://learn.microsoft.com/en-us/azure/architecture/) — architecture patterns and trade-offs. Patterns are not provider-exclusive even when examples use Azure.
8. [Google SRE Book](https://sre.google/sre-book/table-of-contents/) — reliability engineering, monitoring, incident response and operations.
9. [OWASP Application Security Verification Standard](https://owasp.org/www-project-application-security-verification-standard/) — requirements for verifying application security controls.
10. [OWASP Threat Modeling](https://owasp.org/www-community/Threat_Modeling) — threat-modelling concepts and methods.
11. [W3C Web Accessibility Initiative](https://www.w3.org/WAI/) — accessibility standards and guidance.
12. [Unicode — International Components for Unicode](https://icu.unicode.org/) — internationalisation, locale data and formatting.
13. [OpenTelemetry Documentation](https://opentelemetry.io/docs/) — vendor-neutral telemetry for traces, metrics and logs.
14. [PostgreSQL Documentation](https://www.postgresql.org/docs/) — database features, transactions, indexes and administration.
15. [GitHub Actions Documentation](https://docs.github.com/en/actions) — automation and CI workflows.

## Chapter conclusion

Building a social platform is larger than a coding task. First validate the audience and problem. Define a clear product promise, scope, requirements and safety baseline. Then select the architecture and technologies. Test the MVP in a controlled way, demonstrate launch readiness and iterate based on real usage.

**Next chapter:** Part 04 — Technology Foundations: computer hardware, software, programming languages, operating systems, networking, protocols, servers, Git and developer tools, including their history, purpose, internal operation and practical exercises.
