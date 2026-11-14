# 03 — Product Strategy and Complete Build Roadmap

**Handbook:** Social Platform Engineering Handbook  
**Format:** Hinglish (Roman Hindi + standard technical English)  
**Chapter:** Part 03  
**Version:** 0.2  
**Research / planning snapshot:** 13 November 2026  
**Prerequisite:** Chapters 00, 01 and 02  
**Next:** `04_TECHNOLOGY_FOUNDATIONS.md`

---

## Is chapter ka goal

Is chapter ka aim hai ki tum ek social media idea ko actual, testable product plan mein convert karna seekho. Yahan coding se pehle ke decisions cover honge: kiski problem solve karni hai, log kyun join karenge, first version mein kya banana chahiye, requirements kaise likhni hain, architecture kaise choose karna hai, team kaise organise hogi, global users ko kaise plan karna hai, aur launch ke baad product kaise improve hoga.

Ek core principle yaad rakho:

> **Social media platform ka success sirf features ki quantity se nahi aata. Product ko ek real user problem solve karni hoti hai, users ko wapas aane ka reason dena hota hai, aur system ko safe, reliable aur economically sustainable tareeke se operate karna hota hai.**

Isliye Instagram + YouTube + X ke har feature ko first release mein copy karna target nahi hai. Target hai ek focused product banana jo small audience ke liye genuinely useful ho, phir evidence ke basis par grow karna.

## Chapter map

1. Idea, product aur platform ka difference
2. Social product ki history se strategy lessons
3. Target users and initial market selection
4. Problem discovery and user research
5. Competitor and substitute analysis
6. Product thesis and differentiation
7. MVP versus full platform
8. Requirements: PRD, user stories and acceptance criteria
9. Feature prioritisation
10. User journeys and UX decisions
11. Architecture planning before coding
12. Technology selection without hype
13. Safety, privacy and security from day one
14. Worldwide product planning
15. Team and responsibility model
16. Development workflow and quality gates
17. Alpha, beta and public launch
18. Post-launch operations and product improvement
19. Costs, business model and sustainability
20. Risk register, templates, exercises and glossary

---

# 1. Idea, product aur platform mein difference

Ye three words same nahi hain.

- **Idea:** “Main Instagram, YouTube aur X jaisa app banaunga.”
- **Product:** “Creators ko apna work display karne, collaborators discover karne aur project conversations organise karne ke liye ek service milegi.”
- **Platform:** Product ke saath users, creators, content, relationships, rules, trust systems, developer/vendor integrations, distribution aur business operations ka connected ecosystem.

Ek idea ko product banane ke liye tumhe 5 questions answer karne honge:

1. Exact user kaun hai?
2. Us user ka kaunsa real problem hai?
3. Abhi woh problem kaise solve karta hai?
4. Existing solution mein kya missing hai?
5. Tumhara product itna better ya different kyun hoga ki user switch kare?

Agar fifth question ka strong answer nahi hai, toh naye features add karna zaroori nahi ki product ko useful banaye. Pehle problem aur audience clear karo.

## 1.1 Social network ke do sides hote hain

Social platforms aksar two-sided ya multi-sided ecosystems hote hain:

- **Content producers:** creators, organisations, brands, artists, streamers, journalists, communities.
- **Content consumers:** viewers, followers, fans, readers, learners.
- **Additional participants:** advertisers, paying subscribers, moderators, developers, partners and service providers.

Agar creators nahi honge toh audience ko content kam milega. Agar audience nahi hogi toh creators ko publish karne ka incentive kam ho sakta hai. Is coordination problem ko **cold-start problem** kaha jata hai.

MVP plan mein cold-start ka solution feature list se pehle sochna chahiye. Example: ek specific city ke photographers aur local businesses ko connect karna; ya ek niche gaming community ke tournament clips aur discussions ek jagah lana. Start mein narrow community ko serve karna platform ko launch karne mein help kar sakta hai.

---

# 2. History se product strategy ke lessons

Chapter 02 mein platforms ki historical evolution detail mein hai. Yahan un histories se product decisions nikaalte hain.

## 2.1 Focus broad idea se strong use-case par

Kuch successful products ne initial concept se pivot kiya ya ek core behaviour par focus kiya. Instagram ke early product Burbn mein multiple features the; photo sharing ka behaviour particularly promising nikla aur product ne us direction par focus kiya. Lesson ye nahi ki har startup ko pivot karna chahiye. Lesson ye hai ki users ke actual behaviour ko observe karo; founder ke assumptions ko sacred mat banao.

## 2.2 Technology opportunity product need nahi hoti

Faster mobile internet, smartphones, cameras, cheap storage aur cloud systems ne new social formats possible banaye. Lekin sirf technically possible hone se feature useful nahi hota. Product team ko test karna hota hai ki users actually us feature ko use karte hain, repeat karte hain aur value paate hain ya nahi.

## 2.3 Network effects real hain, automatic nahi

**Network effect** ka matlab: kuch conditions mein product ka value participants badhne par increase hota hai.

Example: messaging app par tumhare friends nahi hain toh app ka value low ho sakta hai. Lekin har social product mein har new user sab users ke liye equally useful nahi hota. Spam accounts, fake followers aur low-quality content network ko damage bhi kar sakte hain.

Isliye “users count” ke saath healthy interactions, creator quality, trust and retention bhi measure karo.

## 2.4 Growth ke saath responsibility bhi badhti hai

More users ka matlab more content, more reports, more impersonation, more moderation work, more data handling aur potentially more attacks. Safety ko baad mein add karne ke bajay product ke first architecture mein include karo.

## 2.5 Feature imitation differentiation nahi hai

Stories, short videos, feeds, likes ya hashtags copy karna easy to explain hai, lekin product ko unique reason dena difficult hai. Differentiation kisi feature mein, audience mein, workflow mein, trust model mein, creator economics mein ya user experience mein ho sakti hai.

---

# 3. Target users aur first market choose karna

“Everyone” target audience nahi hai. “Everyone who uses the internet” se product decisions vague ho jaate hain.

## 3.1 Audience segments ke examples

| Segment | Possible need | Important product capability | Likely challenge |
|---|---|---|---|
| Photographers | Portfolio, discovery, client enquiries | High-quality galleries, categories, contact controls | Copyright and image theft |
| Gamers | Clips, teams, events, community | Video upload, game tags, groups | Moderation, copyrighted game/music content |
| Freelancers | Work showcase and collaboration | Portfolio, verified skills, project enquiries | Scam prevention and trust |
| Musicians | Audio/video showcase and fan community | Media playback, creator profile, rights controls | Music licensing and piracy reports |
| Educators | Learning material and discussion | Search, playlists, captions, moderation | Misinformation and child safety |
| Local communities | Local updates and connections | Language/local discovery, community controls | Local abuse, misinformation and safety |
| General creators | Audience growth and publishing | Publishing tools, analytics, feed | Strong competition and cold start |

## 3.2 Audience select karne ka scoring method

Har possible audience ko 1–5 score do. Score research ka replacement nahi; prioritisation help hai.

| Question | Score 1 means | Score 5 means |
|---|---|---|
| Problem intensity | Minor inconvenience | Frequent, painful problem |
| Current alternatives | Good existing alternatives | No suitable alternative |
| Reachability | Hard to contact users | You can reach many target users |
| Repeat usage | Rare need | Daily/weekly repeated need |
| Content supply | Hard to get initial content | You can recruit initial creators |
| Willingness to contribute/pay | Low evidence | Clear evidence of time, effort or payment |
| Safety complexity | High unmanaged risk | Risk can be responsibly managed |
| Differentiation | No clear advantage | Specific defensible product advantage |

Total score ko final truth mat samjho. High score ka reason evidence ke saath explain karo. Safety complexity high ho toh score ko hide mat karo—risk ko separately plan karo.

## 3.3 User persona kaise likho

Persona imaginary marketing character nahi hona chahiye. Interview aur observation se nikla concise working profile hona chahiye.

Example:

**Persona: Independent video creator**

- Creates: short tutorials and behind-the-scenes videos.
- Current workflow: publishes on multiple apps, stores source files separately, tracks brand enquiries in email/DM.
- Frustration: audience fragmented, enquiry history hard to organise, portfolio links outdated.
- Desired outcome: one public work profile and structured collaboration enquiries.
- Constraints: limited time, mobile-first workflow, low upload bandwidth on some days.
- Open question: Does the creator want another social feed, or mainly a portfolio/workflow tool?

Last question important hai. Founder ko assume nahi karna chahiye ki creator ko ek aur feed chahiye.

---

# 4. Problem discovery: users se kaise baat karein

Product design ka start feature suggestion maangne se nahi, users ke current behaviour samajhne se hota hai.

## 4.1 Weak versus strong interview questions

| Weak question | Better question |
|---|---|
| Would you use my app? | Last time this problem happened, what did you do? |
| Do you like this feature? | Show me how you currently complete this task. |
| Would you pay ₹100? | Have you paid for a similar solution? What did you pay and why? |
| Do you need AI? | Which step takes the most effort, and why? |
| Is this design beautiful? | What were you trying to find, and where did you get stuck? |

People often politely say they like an idea. Past behaviour, repeated workarounds, existing spending and actual usage are stronger evidence than compliments.

## 4.2 Interview process

1. Recruit people from the exact segment.
2. Explain that you are researching their workflow, not selling an app.
3. Ask about a recent real example.
4. Ask them to show the current process if they are comfortable.
5. Note tools used, time spent, failure points and workarounds.
6. Ask what happens if the issue is not solved.
7. Avoid leading questions.
8. Summarise what you heard and ask whether you understood correctly.
9. Compare patterns across interviews; one person's preference is not universal evidence.

Always collect only the information necessary for research, explain how you will use it, and avoid collecting sensitive data casually. Record interviews only with informed permission and a suitable retention plan.

## 4.3 Evidence hierarchy

From weaker to stronger product evidence, roughly:

- A person says an idea sounds cool.
- A person says they might use it.
- A person signs up to hear more.
- A person tries a prototype on a realistic task.
- A person returns and uses it again.
- A person changes an existing workflow to use it.
- A person pays or invests meaningful effort, where appropriate.

No single item guarantees success. Repeated behaviour from the target audience is especially useful.

## 4.4 Problem statement template

```text
For [specific user segment],
when [specific situation occurs],
they struggle to [job/task] because [root cause].
Current alternatives are [tools/workarounds],
but these fail because [observed limitation].
A successful outcome would be [measurable user outcome].
Evidence: [interviews, observation, usage data, paid alternatives].
Unknowns: [what we still need to validate].
```

Example (illustrative, not validated research):

```text
For independent designers who work with small businesses,
when they need to show selected work and receive a project enquiry,
they struggle to keep portfolio links and client conversations organised.
Current alternatives include a general social profile, a portfolio site and DMs,
but the workflow is split across multiple tools.
A successful outcome would be a shareable work profile with structured enquiries.
Evidence: not yet collected.
Unknowns: whether users want a new network or only a better portfolio workflow.
```

The line “Evidence: not yet collected” is honest. Do not write fictional validation into a pitch or PRD.

---

# 5. Competitor and substitute analysis

Competitors are not limited to apps with the same name or feature. A spreadsheet, WhatsApp group, personal website, Discord server, email or offline community can be a substitute if it solves the same user job.

## 5.1 Analyse these dimensions

| Dimension | What to inspect |
|---|---|
| Audience | Who is the product primarily designed for? |
| Core job | What user task does it solve? |
| Creation | How easy is publishing/uploading? |
| Discovery | How do new users find content/people? |
| Relationships | Follow, friend, group, subscription or collaboration graph? |
| Communication | Public comments, private messages, calls? |
| Trust | Verification, reporting, blocking, moderation, appeals? |
| Privacy | Public/private controls, account visibility, data controls? |
| Creator value | Audience tools, analytics, payment, ownership? |
| Accessibility | Keyboard, captions, screen reader and language support? |
| Performance | Low-end devices, weak networks, media loading? |
| Business | Ads, subscriptions, transaction fees, sales or other model? |

Do not scrape private areas, bypass access controls or collect personal data in violation of a platform's rules. Use public product behaviour, published documentation, user interviews and permitted research methods.

## 5.2 Competitor matrix template

| User job | Existing solution | What users value | What fails | Your hypothesis |
|---|---|---|---|---|
| Publish portfolio | Portfolio website | Control and presentation | Discovery may be limited | Add relevant creator discovery |
| Share short clips | Video networks | Reach and easy playback | Work enquiries may be fragmented | Connect clips to creator work profile |
| Organise community | Group chat/forum | Familiarity and interaction | Discovery/archiving limitations | Structured topic and creator spaces |
| Find collaborators | DMs/professional networks | Existing contacts | Skill fit may be hard to assess | Search by work evidence and availability |

Fill this matrix using actual research, not assumptions.

---

# 6. Product thesis and differentiation

A **product thesis** is a short, testable explanation of why a specific product should exist and how it will create value.

Template:

```text
We serve: [initial audience]
Their repeated problem: [problem]
Our main promise: [clear outcome]
Our first unique workflow: [specific workflow]
Why current alternatives are insufficient: [evidence]
Why users may switch: [specific advantage]
How we know we are succeeding: [user outcome + metric]
Biggest risk: [risk]
Our next validation test: [experiment]
```

### Example of a weak thesis

“We will combine Instagram, YouTube and Twitter with AI, chat, reels, livestreams and blockchain.”

Why weak? It describes a large feature bundle, not a user problem or reason to switch.

### Example of a more testable thesis

“We help independent game artists and small game teams publish work samples and find collaborators through searchable portfolios and structured project enquiries. We will test whether creators return to update their work and whether teams send qualified enquiries.”

This does not prove the product will succeed; it creates a focused hypothesis that can be tested.

## 6.1 Differentiation dimensions

Differentiation can come from:

- A specific underserved audience.
- A workflow existing products do not handle well.
- Better privacy or user control.
- More useful discovery rather than simply more reach.
- Strong creator ownership and portability.
- Local-language experience and regional relevance.
- Better accessibility or low-bandwidth experience.
- Trust, verification and scam prevention.
- A better community governance model.

Do not claim “more secure,” “privacy-first” or “better algorithm” unless you can define, implement and verify what that means.

---

# 7. Full platform versus MVP

**MVP = Minimum Viable Product.** It is the smallest responsibly built product that can test the central user value with real users. It is not a deliberately insecure, broken or unmaintainable demo.

## 7.1 Three product scopes

| Scope | Purpose | Example |
|---|---|---|
| Prototype | Test a concept or interaction | Clickable design; fake/sample data clearly labelled |
| MVP | Test the core user value in a limited real release | Accounts, profiles, core publishing and discovery |
| Mature platform | Support broader usage, complexity and operations | Advanced recommendations, live video, creator payouts, global reliability |

A prototype can use fake content. A real MVP must not mislead users about what is real, how their data is handled or what safety protection exists.

## 7.2 Suggested release stages for a general creator platform

### Release A — Core identity and content

- Account registration, login and recovery.
- Profile creation and edit.
- User search.
- Follow/unfollow.
- Text and image posts.
- Basic feed.
- Likes and comments.
- Block, report and account privacy controls.
- Admin access with strict permissions and audit logs.

### Release B — Media and discovery

- Short video upload with sensible limits.
- Background media processing.
- Thumbnail generation.
- Search filters and hashtags.
- Explore/discovery page.
- Notifications.
- Basic creator analytics.

### Release C — Community and communication

- Private messaging, after abuse and privacy design is ready.
- Groups or topic spaces.
- Saved content.
- Better moderation queues and appeals.
- User data export/deletion workflows where required.

### Release D — Advanced product

- Personalised recommendations.
- Creator subscriptions or payments, only after legal, fraud and payment-provider work.
- Livestreaming, only after moderation, realtime infrastructure and operational staffing are ready.
- Ads, only after privacy, consent, targeting, measurement and advertiser safety are designed.
- International expansion by region, not by simply translating the UI.

These are an example order, not mandatory feature commitments. Research may show a different sequence.

## 7.3 Features that should not be treated as day-one requirements

- Global trending engine.
- Livestreaming at massive scale.
- Ad auction and real-time bidding.
- Fully personalised ML ranking.
- Multi-region active-active database.
- Complex creator payout and tax workflows.
- End-to-end encrypted group calls.
- Custom video codec or custom CDN.

Use established providers or simpler architecture until product demand justifies deeper investment.

---

# 8. Product requirements: PRD, user stories and acceptance criteria

A developer should not have to guess what a feature means. Product requirements turn an idea into something design, engineering and testing can work from.

## 8.1 What is a PRD?

PRD means **Product Requirements Document**. It describes the user problem, goals, scope, behaviour, constraints, success measures and open questions for a product or feature.

### PRD template

```markdown
# Feature: [Name]

## 1. Problem
Who has the problem? In which situation? What evidence supports it?

## 2. User outcome
What should the user be able to achieve?

## 3. Goal
What measurable change are we trying to create?

## 4. Non-goals
What will this feature NOT do in this release?

## 5. User journey
What steps does the user take?

## 6. Functional requirements
FR-01: ...
FR-02: ...

## 7. Non-functional requirements
Performance, availability, privacy, security, accessibility,
reliability, compatibility and maintainability expectations.

## 8. Permissions and privacy
Who can view, create, edit, delete, share or report this data?

## 9. Failure cases
Network loss, invalid input, duplicate request, permission denial,
server error, storage failure and retry behaviour.

## 10. Analytics
Which minimum events are required? What data must not be collected?

## 11. Acceptance criteria
Testable statements that define completion.

## 12. Dependencies
APIs, vendors, teams, legal review, design and infrastructure.

## 13. Rollout and rollback
Who gets the feature first? How is it disabled or rolled back?

## 14. Open questions and decision log
Unknowns, owner, due date and final decision.
```

## 8.2 Functional versus non-functional requirements

**Functional requirements** explain what the system does.

Examples:
- A signed-in user can create an image post.
- The post owner can edit the caption.
- A user can block another account.
- A private post is visible only to authorised viewers.

**Non-functional requirements** explain qualities and constraints.

Examples:
- The service should remain usable during an instance restart.
- Private media should not be publicly accessible through a permanent guessable URL.
- The upload flow should clearly show progress and failure state.
- The interface should support keyboard navigation.
- The API should have documented latency objectives.
- Data backups should be restorable and tested.

Non-functional requirements need measurable targets when possible. “Very fast” is not a testable target. Define a metric, measurement location, percentile and expected operating conditions.

## 8.3 User story format

```text
As a [user type],
I want [capability],
so that [user outcome].
```

Example:

“As a creator, I want to mark a post as private so that only approved followers can view it.”

A user story is not a complete specification by itself. Add permissions, error cases, accessibility and acceptance criteria.

## 8.4 Acceptance criteria example: private post

- Given a post is private, when a non-authorised user requests it through the web UI, the content is not displayed.
- Given the same user calls the API directly, the backend also denies access.
- Given a blocked user requests the post, access is denied according to the platform's block rules.
- Given an authorised follower requests it, access is permitted.
- Media URLs do not bypass the post's privacy control.
- Denied requests are handled without exposing private metadata.
- Tests cover both UI and direct API access.

Notice: hiding a button is not access control. Backend authorisation and media delivery rules must enforce the same policy.

---

# 9. Feature prioritisation

Feature lists always become longer than available time and capacity. Teams need a repeatable method to decide what to build first.

## 9.1 MoSCoW method

- **Must have:** Without it, the first release cannot responsibly deliver its core promise.
- **Should have:** Important, but a temporary workaround exists.
- **Could have:** Useful if capacity remains.
- **Won't have now:** Explicitly out of this release.

Example for first release:

| Feature | Priority | Reason |
|---|---|---|
| Signup/login and recovery | Must | Account access foundation |
| Profile | Must | User identity and creator presence |
| Create and view posts | Must | Core publishing loop |
| Report and block | Must | Basic user safety |
| Basic feed | Must | Content discovery for followed accounts |
| Advanced recommendation ML | Won't have now | Requires data, evaluation and safety work |
| Livestreaming | Won't have now | Large realtime and moderation burden |
| Creator subscription payments | Won't have now | Payments, fraud, tax and legal complexity |

## 9.2 RICE method

RICE is a prioritisation model:

`RICE score = (Reach × Impact × Confidence) / Effort`

- Reach: how many target users will be affected in a defined period?
- Impact: how much does it improve the chosen user outcome?
- Confidence: how strong is the evidence?
- Effort: person-time or complexity estimate.

Scores are a discussion aid, not objective truth. Do not inflate confidence to push a favourite feature.

## 9.3 Safety and compliance can override feature scoring

Some work is required even when it does not increase engagement. Examples: access control, report handling, security fixes, deletion flows, backups and legal obligations. These should not be postponed just because a growth feature has a higher RICE score.

---

# 10. User journeys and UX planning

A user journey maps the steps a person takes to reach an outcome.

## 10.1 Example: new creator joins

```text
Discover link
  -> landing page explains purpose and audience
  -> signup
  -> email/phone verification as designed
  -> choose username
  -> set profile visibility and basic privacy
  -> add profile details
  -> follow suggested relevant creators (optional)
  -> see a useful first feed
  -> publish or save a first post
  -> understand reporting and account controls
```

Every step needs a failure-state design:

- Verification message delayed.
- Username already taken.
- User loses network.
- Suggested users are irrelevant.
- User does not want to upload contacts.
- Upload fails.
- User wants to skip onboarding.

Do not force unnecessary permissions such as contacts, location or microphone before the feature needs them. Explain why a permission is requested.

## 10.2 Empty states

A new social app often has an empty feed. Empty screens can make a new product appear broken.

Possible responsible empty-state choices:

- Explain how to find relevant people.
- Offer optional topic selection.
- Show clearly labelled sample/demo content only in demo contexts.
- Suggest following a few verified or invited creators.
- Explain that the feed will improve as the user follows accounts.

Do not fabricate engagement, fake user counts or pretend sample posts are real users' content.

## 10.3 Accessibility from the beginning

Consider:

- Keyboard focus and navigation.
- Screen-reader labels.
- Text contrast and scalable text.
- Captions for relevant video content.
- Alt text for meaningful images.
- Avoiding colour as the only way to communicate status.
- Reduced-motion options.
- Touch target sizes.
- Plain-language error messages.

Accessibility is a product quality requirement, not just a visual polish stage.

---

# 11. Architecture planning before coding

Architecture is the set of important technical structures and decisions that shape the system. It includes components, boundaries, data flow, communication, security, deployment and failure handling.

## 11.1 Start with a context diagram

First draw outside actors and the system boundary.

```text
[Web browser] -----------+
[Android / iOS app] -----+----> [Social Platform]
[Admin / moderator] ----+
[Email / OTP provider] --------> [External provider]
[Object storage / CDN] <-------> [Social Platform]
[Payment provider] ------------> [Later-stage integration]
```

Then identify internal components:

```text
Client applications
  -> API entry point
     -> identity and permission checks
     -> user/profile module
     -> social graph module
     -> post/content module
     -> feed/discovery module
     -> media service
     -> moderation/report service
     -> notification service
  -> PostgreSQL / Redis / object storage / search
  -> background job workers
  -> monitoring, logs and alerts
```

## 11.2 Modular monolith versus microservices

**Modular monolith:** one deployable backend application with clear internal modules and boundaries.

Advantages:
- Easier to run locally.
- Fewer network calls between modules.
- Simpler deployment and debugging for a small team.
- Transactions and data consistency can be easier to manage.

Limitations:
- The application may become harder to deploy as one unit at very large scale.
- Modules can become tightly coupled if boundaries are not enforced.
- A failure or resource-heavy workload may affect the whole application unless isolated.

**Microservices:** independently deployable services communicating over network APIs or events.

Advantages:
- Independent scaling and deployments where boundaries are well chosen.
- Different teams can own services.
- Failure/resource isolation can improve when correctly engineered.

Costs and risks:
- Network failures and timeouts.
- Distributed tracing and debugging complexity.
- Data consistency and event ordering problems.
- Service discovery, API compatibility and versioning.
- More infrastructure and operational burden.
- More security boundaries and secrets to manage.

**Recommendation for a new small team:** begin with a modular monolith and separate background workers where useful. Split a service only when a real scaling, reliability, ownership or deployment reason exists. “Big companies use microservices” is not a sufficient reason.

## 11.3 Event-driven background work

Some tasks should not delay the user's main request:

- Video transcoding.
- Thumbnail generation.
- Sending emails or push notifications.
- Search indexing.
- Analytics aggregation.
- Moderation assistance.

An API can write a durable job/event to a queue. A worker processes it later. Design for retries, duplicate delivery and dead-letter handling. Do not assume a queue delivers every event exactly once; many practical systems provide at-least-once delivery, so workers should be idempotent where possible.

## 11.4 Architecture decision records (ADR)

For every significant decision, write a short record:

```markdown
# ADR-001: Start with a modular monolith

Status: Accepted
Date: YYYY-MM-DD

## Context
Small team, early product, limited operational capacity.

## Decision
One backend deployment with clear modules and separate workers.

## Alternatives
Microservices from day one; serverless functions for all logic.

## Consequences
Simpler local development and deployment initially.
Need disciplined module boundaries and future extraction plan.

## Revisit when
Independent scaling or team ownership makes a service split valuable.
```

This prevents a future developer from guessing why a tool was chosen.

---

# 12. Technology selection without hype

Never choose a technology only because it is popular on social media or because a major company uses it.

Evaluate each option on:

1. Does it solve the requirement?
2. Is the team able to build and operate it?
3. Is it mature enough for the workload?
4. What is the total cost, including operations and vendor lock-in?
5. Is there a reasonable migration path?
6. Does it meet security, privacy and compliance needs?
7. Does it have good documentation and support?
8. Is it overkill for the current stage?

## 12.1 Example starting stack

This is an illustrative, balanced stack for a web-first creator/social MVP—not a mandatory universal stack.

| Layer | Example choice | Why it may fit | Alternatives / limitations |
|---|---|---|---|
| Web UI | React + Next.js + TypeScript | Component ecosystem, routing and typed code | SvelteKit, Vue/Nuxt; framework learning cost |
| Backend | Node.js + NestJS | TypeScript across frontend/backend; structured modules | Fastify, Django, Spring, Go; team skill matters |
| Main database | PostgreSQL | Relational data, transactions, constraints and mature tooling | MySQL; document DB for suitable flexible workloads |
| Cache / queue support | Redis | Fast temporary data, rate limits and queue ecosystem | Managed queue services; Redis persistence model must be understood |
| Object storage | S3-compatible storage | Stores large media outside relational database | Vendor differences, egress/operation costs |
| Media processing | FFmpeg or managed transcoding | Established media tooling and codec support | Managed service can reduce operations but adds vendor cost |
| Search | PostgreSQL initially; OpenSearch later if needed | Avoid premature infrastructure | Dedicated search introduces index consistency and operations |
| Realtime | WebSocket gateway when needed | Bidirectional updates/messages | Managed realtime service; connection scaling complexity |
| CI/CD | GitHub Actions or equivalent | Automated test and deployment workflows | Vendor limits and runner security need review |
| Containers | Docker | Repeatable app environments | Can be unnecessary for a tiny serverless app |
| Monitoring | Sentry + OpenTelemetry-compatible backend | Error reports and traces | Privacy, sampling and cost must be configured |

## 12.2 Why not use every database?

A common beginner mistake is adding PostgreSQL, MongoDB, Redis, Elasticsearch, Kafka and ClickHouse before the product needs them.

Every new data system adds:
- Another deployment and access-control boundary.
- Backups and recovery responsibility.
- Schema/index operations.
- Monitoring and cost.
- Data consistency questions.
- More failure modes.

Begin with the smallest set that meets the requirements. Add a new system when you can describe the specific problem it solves and how you will operate it.

## 12.3 Build versus buy

| Capability | Build yourself when | Use a provider/service when |
|---|---|---|
| Email delivery | Email is core product IP (rare) | Normal transactional email |
| OTP/SMS | You operate a specialised telecom service | Standard verification messaging |
| Media storage | Storage technology itself is core research | You just need reliable object storage |
| Video transcoding | Codec/encoding is a differentiator | You need standard formats reliably |
| Payments | Payments are your regulated core business | You need standard checkout/payout rails |
| Authentication | Identity system is a core capability and team can secure it | Standard account login and recovery |
| CDN | Network delivery is your core business | Normal global asset delivery |

Buying a provider does not remove your responsibility. You still need configuration, access control, vendor due diligence, data processing terms, incident plans and exit/migration planning.

---

# 13. Security, privacy and safety in the product plan

Security cannot be an isolated final checklist. It must affect product requirements, architecture and release approval.

## 13.1 Create a basic threat model

A threat model asks: what assets matter, who may attack or misuse them, where are the entry points, what could go wrong, and what controls reduce the risk?

| Element | Questions |
|---|---|
| Assets | Accounts, private posts, messages, credentials, media, payment data, admin tools |
| Threat actors | Criminals, spammers, malicious users, compromised vendors, careless insiders |
| Entry points | Login, password reset, upload, search, APIs, admin panel, webhooks, mobile clients |
| Abuse cases | Account takeover, scraping, fake engagement, harassment, private media leakage |
| Impact | Exposure, account loss, fraud, service outage, legal and reputational damage |
| Controls | MFA for staff, secure sessions, authorisation, rate limits, encryption, monitoring, backups |
| Detection | Alerts, audit logs, anomaly patterns, user reports, incident triage |
| Recovery | Revoke sessions, rotate secrets, restore data, notify affected parties when required |

## 13.2 Security requirements for the first product brief

- Authentication and authorisation must be separate concepts.
- Every sensitive API action must enforce server-side object-level permissions.
- Admin access must be role-limited, protected and audited.
- Passwords must be stored using a purpose-built password hashing algorithm, never plaintext or reversible encryption.
- Sessions/tokens must have controlled lifetimes, revocation and secure storage.
- Login, signup, search, upload and messaging need appropriate anti-abuse/rate controls.
- Uploads must validate actual file content, size and processing safety.
- Secrets must not be committed to source control or exposed to the browser.
- Backups must be encrypted where appropriate, access-controlled and restore-tested.
- Security logs must avoid storing passwords, raw tokens or unnecessary sensitive content.

For technical depth, see Part 10: `10_SECURITY_PRIVACY_AND_DEFENDING_AGAINST_ATTACKERS.md`.

## 13.3 Product safety requirements

Every user-generated-content platform should design for:

- Report content, account and conversation where appropriate.
- Block and mute users.
- Privacy controls and visibility clarity.
- Moderation queue and escalation.
- Appeals or review process for consequential decisions.
- Spam and impersonation response.
- Emergency handling for credible threats and urgent safety reports.
- Clear rules and enforcement explanations.
- Staff permissions and moderator wellbeing.

Do not launch private messaging, live video or large public communities without considering the additional abuse and moderation load those features create.

## 13.4 Privacy-by-design checklist

For each data field or event, record:

- Why is it needed?
- Is it optional?
- Can the product work with less precise data?
- Who can access it?
- Which vendors receive it?
- Where is it stored and processed?
- How long is it retained?
- How can it be corrected or deleted where applicable?
- Is it used for analytics, ads, ranking or AI training?
- What user choice or notice is required?

A privacy policy cannot compensate for unnecessary collection. Collecting less data often reduces security, compliance and operational risk.

---

# 14. Worldwide product planning

A global social platform is not simply one server plus translated labels. Different countries have different languages, networks, devices, payment rails, user expectations and legal environments.

## 14.1 Separate five different geography questions

1. **Company jurisdiction:** where the legal entity is incorporated, managed and may be regulated.
2. **User jurisdiction:** where the person is located, resides or is otherwise connected to the service.
3. **Infrastructure location:** where compute, database, logs, backups and media are stored or processed.
4. **Vendor jurisdiction:** where cloud, payments, email, analytics, moderation and support vendors operate.
5. **Data transfer:** where data moves during normal use, support access, backup, analytics and incidents.

These questions are connected but not interchangeable. A US-incorporated company serving EU and Indian users may have to assess obligations from more than one legal system. A server region alone does not settle every legal question.

Detailed country/region analysis is in Part 12. The correct approach is to prepare a data-flow map and get jurisdiction-specific legal review before launch/expansion.

## 14.2 Internationalisation versus localisation

**Internationalisation (i18n):** design the software so it can support different languages, scripts, currencies, formats and regions.

**Localisation (l10n):** adapt the experience for a specific language or market.

Examples:
- Translation of interface labels and error messages.
- Right-to-left layout support where needed.
- Date, time, number and currency formatting.
- Unicode and multilingual search.
- Local language moderation coverage.
- Time-zone-aware notifications.
- Local payment options, if payments are offered.
- Country-specific legal notices and help routes.

Do not store local time as an ambiguous string. Store an unambiguous timestamp, then render it in the user's chosen or detected time zone. Do not assume all users in one country use the same language.

## 14.3 Global media delivery

Users may have different network speeds, mobile devices and data plans. Design for:
- Responsive image sizes.
- Adaptive video bitrate/streaming.
- Upload retry and resumability where feasible.
- Compression without destroying quality.
- Lazy loading and pagination.
- Captions and accessible controls.
- Clear data-usage choices for video-heavy products.
- CDN configuration that respects private content authorisation.

A CDN improves delivery; it does not by itself enforce privacy. Private media needs signed/authorised access and cache rules that prevent leakage.

## 14.4 Regional rollout strategy

Do not announce worldwide launch before support and moderation are ready for every supported market.

A sensible staged method:
1. Define the initial user segment and language.
2. Select a launch region where the team can provide support and moderation.
3. Map applicable laws and service-provider requirements.
4. Test network/device coverage.
5. Recruit initial creators and users.
6. Add the next region only when language, policy, support and infrastructure are ready.

---

# 15. Team and responsibility model

A small product team can share roles, but accountability still needs to be clear.

| Role / function | Main responsibility | Can be shared initially? |
|---|---|---|
| Founder / Product owner | Vision, target audience, priorities, decisions | Often yes |
| Product designer | Research, flows, wireframes, accessibility | Yes, with constraints |
| Frontend engineer | Web UI, browser behaviour, client integration | Usually dedicated as product grows |
| Backend engineer | APIs, business rules, data and permissions | Often core early role |
| Infrastructure / SRE | Hosting, deployments, monitoring, reliability | Can be shared/contracted initially |
| Security | Threat model, secure design, review, incident readiness | Specialist review may be contracted; ownership remains internal |
| QA / test engineer | Test strategy, regression and release confidence | Can be shared initially |
| Data / ML engineer | Analytics, search, ranking and recommendations | Usually later unless central to MVP |
| Trust & Safety | Moderation policy, reports, appeals and escalation | Must be planned before public UGC launch |
| Legal / privacy | Jurisdiction, contracts, privacy and regulatory advice | Qualified external counsel may support |
| Customer support | User questions, account recovery and complaints | Can start small but needs clear ownership |

Do not turn role estimates into fake promises about headcount or delivery time. Actual staffing depends on product scope, team skill, vendors, quality requirements and available budget.

## 15.1 Responsibility matrix

For critical workflows, define who is:
- **Responsible:** does the work.
- **Accountable:** owns the final outcome.
- **Consulted:** provides specialist input.
- **Informed:** receives the decision/update.

Example for a security incident:

| Task | Engineering | Security lead | Legal/privacy | Support/comms | Founder |
|---|---|---|---|---|---|
| Contain incident | Responsible | Accountable/lead | Consulted | Informed | Informed |
| Assess affected data | Responsible | Lead | Consulted | Informed | Informed |
| Legal notification decision | Consulted | Consulted | Accountable | Informed | Informed |
| User communication | Consulted | Consulted | Consulted | Responsible | Accountable |

Adapt it to the actual company. The key is avoiding “everyone thought someone else was handling it.”

---

# 16. Development workflow and quality gates

A professional development process makes work reviewable and reversible.

## 16.1 Typical lifecycle

```text
Problem evidence
  -> PRD and acceptance criteria
  -> Design and threat review
  -> Architecture/ADR
  -> Issue breakdown
  -> Feature branch
  -> Code + tests
  -> Pull request and review
  -> CI pipeline
  -> Staging deployment
  -> QA / security / product acceptance
  -> Gradual production rollout
  -> Monitoring
  -> Rollback or follow-up improvements
```

## 16.2 Environments

- **Local:** developer's machine; test accounts and synthetic data.
- **Development/shared test:** integration of current work.
- **Staging:** production-like environment for release verification.
- **Production:** real user traffic and real data.

Never copy production personal data into developer laptops or public test tools without a lawful, secure and necessary basis. Prefer synthetic or carefully anonymised data.

## 16.3 Git branch and review process

A simple approach:
- `main` remains deployable.
- A short-lived feature/fix branch contains a change.
- Pull request describes purpose, risk and tests.
- CI checks formatting, types, tests, dependency/security checks as appropriate.
- Reviewer checks business logic, permissions, data changes and maintainability.
- Release process merges and deploys through controlled automation.

Do not commit `.env` files, credentials, private keys, production dumps or user uploads into Git.

## 16.4 Database migrations

Production migrations should be backward-compatible where practical:
1. Add a new field/table without breaking old code.
2. Deploy code that can handle old and new forms.
3. Backfill records safely in batches.
4. Verify counts and integrity.
5. Switch reads/writes.
6. Remove old field only after no active code depends on it.

Take appropriate backups and test rollback/recovery procedures. A rollback of application code does not automatically reverse a destructive database migration safely.

## 16.5 Release quality gate

Before release, ask:
- Are acceptance criteria met?
- Are automated tests passing?
- Are permission tests included?
- Are security changes reviewed?
- Are migrations safe?
- Are logs and alerts ready?
- Is support/moderation ready?
- Is rollback/feature-disable possible?
- Is the user-facing change documented?
- Have privacy/data flows changed?

---

# 17. Alpha, beta and public launch

Launch is a sequence of controlled learning and risk management.

## 17.1 Internal alpha

Audience: team and invited internal testers.

Purpose:
- Validate core flows.
- Find obvious defects.
- Verify admin/moderation operations.
- Check logging and error handling.
- Test account recovery and deletion workflows.
- Confirm backup and restore procedures.

Do not treat internal testers as representative of every target user.

## 17.2 Closed beta

Audience: selected real users from the target segment.

Before inviting them:
- Explain that it is a beta and what may be incomplete.
- Provide a support/report path.
- Explain privacy and data use.
- Avoid collecting more information than needed.
- Set clear terms and acceptable-use rules.
- Have a process to handle harassment, abuse and account compromise.
- Monitor failures and costs.

Measure whether users complete the core task and return, not only how many sign up.

## 17.3 Public launch readiness

### Product
- Core use case works end to end.
- Onboarding is understandable.
- Accessibility basics are tested.
- Help and account-recovery guidance exists.

### Engineering
- Production configuration is separate from development.
- TLS is configured.
- Database backups and restore tests exist.
- Error monitoring and uptime/performance alerts exist.
- Rate limits and abuse protection are configured.
- Release and rollback procedures are documented.

### Safety and operations
- Report, block and moderation workflows work.
- A human owner is available for urgent escalations.
- Terms, privacy and community rules match actual product behaviour.
- Support and grievance channels are staffed.
- Incident response plan exists.

### Business and legal
- Business/entity, contracts, tax and payment requirements have been assessed for the relevant markets.
- Vendor and data-processing arrangements have been reviewed.
- Trademark/domain checks have been conducted.
- Any required age, privacy, intermediary, copyright or sector-specific requirements have been reviewed by qualified advisers.

A launch checklist is not a substitute for jurisdiction-specific legal advice.

## 17.4 Gradual rollout

Instead of exposing every user immediately:
- Release to internal users.
- Release to a small external cohort.
- Monitor error rates, support load, abuse reports and cost.
- Expand gradually when service health is acceptable.
- Use feature flags for risky features.

A feature flag is not a security boundary. Backend permissions must still be enforced even when the UI hides a feature.

---

# 18. Post-launch: operate, learn and improve

After launch, the product enters a continuous loop:

```text
Observe user behaviour and failures
  -> classify issue/opportunity
  -> validate root cause
  -> prioritise
  -> design and implement
  -> test and release
  -> measure outcome
  -> keep, change or roll back
```

## 18.1 Product metrics

| Metric | What it tells you | Caution |
|---|---|---|
| Activation | Whether a new user reaches a meaningful first outcome | Define meaningful action by product |
| DAU/WAU/MAU | Active usage over a time window | Counts alone do not show value |
| Retention | Whether users return after a defined period | Segment by signup cohort and user type |
| Creator activation | Whether creators publish/complete a useful setup | Avoid pressuring low-quality posting |
| Content quality | Whether users find content relevant/safe | Hard to reduce to one score |
| Report rate | Reports relative to usage/content | A low rate may mean under-reporting, not safety |
| Moderation response | How quickly cases are triaged/resolved | Include severity and accuracy, not speed alone |
| Upload success | Reliability of media creation flow | Segment by file size, device and network |
| Video start/rebuffer | Playback experience | Segment by region and connection |
| Crash/error rate | Product stability | Watch both client and backend errors |
| Cost per active user | Operational efficiency | Include storage, bandwidth and moderation cost |

Avoid blindly maximising time spent, notifications or engagement. These metrics can conflict with wellbeing, relevance, creator quality and safety.

## 18.2 Feedback channels

Collect feedback from:
- In-product feedback/report forms.
- Support conversations.
- Beta interviews.
- User sessions with informed consent.
- Product analytics with appropriate privacy controls.
- Creator/community advisory groups.
- Moderation trends and appeals.

Separate product feedback from abuse reports and legal complaints. They need different triage paths.

## 18.3 Incident management

For serious incidents, the team needs:
1. Detection and alert.
2. On-call or named owner.
3. Severity classification.
4. Containment and mitigation.
5. Investigation and evidence preservation.
6. Legal/privacy notification assessment where relevant.
7. User/vendor/regulator communication where required.
8. Recovery and validation.
9. Post-incident review focused on system improvements.

Do not promise users “zero downtime” or “no data loss.” Define reliability objectives, monitor them and be transparent about incidents.

---

# 19. Costs, business model and sustainability

A social app can be cheap to prototype and expensive to operate at scale. The largest cost drivers depend heavily on content format and user behaviour.

## 19.1 Cost categories

- Application compute and network egress.
- Database compute, storage, backups and replicas.
- Object storage for photos/videos/audio.
- CDN data transfer.
- Video transcoding and processing.
- Search and analytics infrastructure.
- Email, SMS and push notification providers.
- Abuse prevention, fraud tools and moderation.
- Customer support.
- Security audits and incident response.
- Team costs, legal, accounting, taxes and insurance where appropriate.

## 19.2 Cost model variables

Do not estimate hosting cost from registered users alone. Model:

- Monthly active users and peak concurrent users.
- Average requests per active user.
- Media uploads per day.
- Average image/video size.
- Average watch time and bitrate.
- Media retention period.
- Download/share traffic.
- Number of regions.
- Database reads/writes and index growth.
- Moderation reports per thousand users.
- Support contacts per thousand users.

### Illustrative media calculation

Suppose a hypothetical service stores 20,000 new videos, each averaging 80 MB, in one month.

Raw original upload volume:

`20,000 × 80 MB = 1,600,000 MB ≈ 1.6 TB` (decimal units).

This is not the full storage requirement. Transcoded outputs, thumbnails, replicas, versioning and retention can increase storage. Delivery bandwidth depends on how many times users watch the videos and at what bitrate. This example is a calculation method, not a quote for any cloud provider.

## 19.3 Business models

| Model | How revenue may occur | Risks / work |
|---|---|---|
| Advertising | Advertiser pays for eligible impressions/actions | Privacy, ad quality, brand safety, measurement and fraud |
| Subscription | Users pay recurring fee | Clear paid value, billing and cancellations |
| Creator membership | Fans subscribe to a creator | Payout, refunds, tax and content obligations |
| Transaction fee | Platform takes fee from eligible transactions | Disputes, fraud, payment-provider and tax complexity |
| Creator tools | Paid analytics/storage/workflow tools | Must prove business value |
| Business accounts | Organisations pay for advanced tools | Support and service-level expectations |
| Sponsorships | Brands pay for partnerships | Disclosure and brand-safety needs |

A platform does not need to use every model. Do not introduce payment features before understanding financial, fraud, regulatory and support requirements in launch markets.

## 19.4 Unit economics basics

Terms to understand:

- **CAC:** customer/user acquisition cost, depending on the business definition.
- **LTV:** estimated lifetime value of a customer/user under stated assumptions.
- **Gross margin:** revenue minus relevant direct costs, divided by revenue.
- **Churn:** users/customers who stop using or paying in a defined period.
- **Payback period:** time needed to recover acquisition cost from contribution margin.

Early estimates are uncertain. Label assumptions, measure actual behaviour and revise the model. A high user count with higher infrastructure/moderation cost than revenue is not automatically a healthy business.

---

# 20. Risk register

Start a risk register before public launch. Review it whenever product scope or geography changes.

| Risk | Example | Prevention / mitigation | Owner |
|---|---|---|---|
| No product-market fit | Users sign up but do not return | Narrow audience, interviews, behavioural evidence | Product |
| Cold start | Feed has little relevant content | Seed legitimate creator supply, niche rollout | Product/community |
| Account takeover | Stolen passwords or session | MFA options, rate limits, secure recovery, anomaly detection | Engineering/security |
| Private content leakage | Guessable media URL bypasses access | Authorised media delivery, private cache rules, tests | Backend/security |
| Spam/fake accounts | Bots manipulate follows and likes | Rate limits, detection, friction and moderation | Trust & Safety |
| Harassment | Users target another user | Report/block/mute, policy, escalation and appeals | Trust & Safety |
| Data loss | Accidental deletion or infrastructure failure | Independent backups, point-in-time recovery, restore drills | Infrastructure |
| Vendor outage | Email/storage/CDN fails | Retry, queueing, fallback and vendor incident plan | Infrastructure |
| Cost spike | Video bandwidth unexpectedly high | Usage limits, alerts, quotas and cost attribution | Finance/engineering |
| Legal mismatch | Product behaviour conflicts with local rules | Market assessment and qualified legal review | Legal/product |
| Team dependency | One person understands production | Documentation, access review, runbooks, peer review | Engineering lead |
| Bad recommendation outcome | Ranking amplifies harmful or low-quality content | Safety evaluation, user controls, audits and feedback | Product/data/safety |

## 20.1 Risk severity

For each risk, estimate:
- Likelihood: how plausible is it?
- Impact: how bad would it be?
- Detectability: how likely are we to notice quickly?
- Mitigation strength: how effective is the control?

A low-frequency, catastrophic-impact risk still deserves attention. Risk scoring should prompt decisions, not create fake certainty.

---

# 21. Practical build sequence: from zero to release

This is a dependency-based sequence. It is not a promise that one person can complete the entire platform in a fixed number of weeks. Actual time depends on prior skill, feature scope, team size, quality bar and budget.

## Phase 0 — Research and product definition

Deliverables:
- Audience hypothesis.
- User interview notes.
- Problem statement.
- Competitor/substitute matrix.
- Product thesis.
- First-release non-goals.
- Initial business hypothesis.

Exit condition: you can explain, in plain words, who the first user is, what job they need done and why your product may be useful.

## Phase 1 — Requirements and design

Deliverables:
- PRD.
- User stories and acceptance criteria.
- User journey diagrams.
- Wireframes and clickable prototype.
- Design system basics.
- Accessibility requirements.
- Threat model and privacy data inventory.

Exit condition: designers, developers and testers can describe the same expected behaviour without guessing.

## Phase 2 — Technical foundation

Deliverables:
- Repository and folder structure.
- Local development setup.
- Development/staging/production environments.
- CI workflow.
- Database schema and migrations.
- API conventions.
- Logging and error handling.
- Secrets management.

Exit condition: one small feature can be built, tested, deployed to staging and monitored safely.

## Phase 3 — Core user experience

Deliverables:
- Signup/login/recovery.
- Profiles.
- Privacy settings.
- Follow/block.
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
- Incident response runbook.
- Support and grievance workflow.
- Legal/policy review for initial market.

Exit condition: the company can respond to common user harm, account issues and operational incidents.

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
- Support rota/ownership.
- Release notes.
- Product metric review.

Exit condition: not “the app is finished”; rather, the product has a stable operating loop for continued learning and maintenance.

---

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

## 22.2 User interview note

```markdown
Participant code (not unnecessary personal identity):
Target segment:
Date / consent status:

Recent real example:
Current workflow:
Tools used:
Time / cost / frustration:
Workaround:
What happens if unresolved:
What user values:
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
What did metrics show?
What assumptions changed?
What is the largest current risk?
What is the next most valuable task?
What are we deliberately NOT doing now?
```

---

# 23. Practical exercise

Complete this exercise for your own proposed social product before moving into the technology foundations chapter.

## Exercise A — Pick an audience

Write three possible audiences. Score them using Section 3.2. Choose one to investigate first; do not permanently commit based only on the score.

## Exercise B — Conduct discovery

Speak to several people from that segment. Ask about recent real workflows. Do not pitch your idea during the first part of the conversation. Record evidence separately from assumptions.

## Exercise C — Write the product thesis

Use the Section 6 template. Keep it to one paragraph plus the evidence and biggest risk.

## Exercise D — Define the first release

Create a list of:
- Must-have user outcomes.
- Safety and privacy requirements.
- Features explicitly deferred.
- Success metrics.

## Exercise E — Draw architecture

Draw a context diagram, component diagram and one sequence diagram for a core user action, such as creating a post or uploading a video. Mark trust boundaries and external vendors.

## Exercise F — Test the idea

Create a clickable prototype or a limited functional slice. Observe target users completing the task. Note where they hesitate, misunderstand or abandon it. Revise the requirements.

---

# 24. Glossary

| Term | Meaning |
|---|---|
| Product | A service designed to create a defined user outcome |
| Platform | Product plus users, interactions, rules, ecosystem and operations |
| Target segment | Specific group of users being served first |
| User persona | Evidence-based working model of a user type |
| Problem discovery | Research into real user needs and workflows |
| Product thesis | Testable statement explaining the product's reason to exist |
| MVP | Minimum Viable Product; smallest responsible product to test core value |
| PRD | Product Requirements Document |
| User story | A user-centred description of a desired capability |
| Acceptance criteria | Testable conditions that define completion |
| Functional requirement | What the system must do |
| Non-functional requirement | Quality/constraint such as speed, security or reliability |
| MoSCoW | Must, Should, Could, Won't prioritisation |
| RICE | Reach, Impact, Confidence, Effort prioritisation model |
| Cold start | Difficulty creating value before enough users/content exist |
| Network effect | Value that can increase as relevant participants join |
| Architecture | System structure, boundaries, data flow and design decisions |
| Modular monolith | One deployable application with well-separated modules |
| Microservice | Independently deployable service with a bounded responsibility |
| ADR | Architecture Decision Record |
| Feature flag | Runtime control to enable/disable a feature for a cohort |
| Threat model | Structured analysis of assets, threats, entry points and controls |
| i18n | Internationalisation: designing for multiple regions/languages |
| l10n | Localisation: adapting to a particular locale |
| Alpha | Early controlled test, often internal |
| Beta | Limited test with selected external users |
| Retention | Users returning after a defined time period |
| Churn | Users/customers who stop using or paying |
| SLO | Service Level Objective, a measurable reliability target |
| Unit economics | Revenue and cost economics per user/customer/transaction |

---

# 25. Further reading and references

These resources support the methods and technical concepts in this chapter. Product practices are not laws of nature; adapt them to evidence and context.

1. [Y Combinator — Startup Library](https://www.ycombinator.com/library) — founder-oriented material on product, users, launching and company building. Useful advice, not a guarantee of success.
2. [The Mom Test — Rob Fitzpatrick](https://www.momtestbook.com/) — interviewing users about real behaviour rather than asking leading “would you use it?” questions.
3. [Nielsen Norman Group — User Research](https://www.nngroup.com/topic/user-research/) — practical research methods and usability guidance.
4. [Atlassian — Product Requirements](https://www.atlassian.com/agile/product-management/requirements) — requirements and product documentation concepts.
5. [Atlassian — RICE prioritisation](https://www.atlassian.com/agile/product-management/prioritization-framework) — prioritisation framework overview; formula variants can differ between teams.
6. [C4 Model](https://c4model.com/) — context, container, component and code-level architecture diagrams.
7. [Microsoft Azure Architecture Center](https://learn.microsoft.com/en-us/azure/architecture/) — architecture patterns and trade-offs; patterns are not provider-exclusive even when examples use Azure.
8. [Google SRE Book](https://sre.google/sre-book/table-of-contents/) — reliability engineering, monitoring, incident response and operational thinking.
9. [OWASP Application Security Verification Standard](https://owasp.org/www-project-application-security-verification-standard/) — requirements for testing application security controls.
10. [OWASP Threat Modeling](https://owasp.org/www-community/Threat_Modeling) — threat-model concepts and methods.
11. [W3C Web Accessibility Initiative](https://www.w3.org/WAI/) — accessibility standards and guidance.
12. [Unicode — International Components for Unicode (ICU)](https://icu.unicode.org/) — internationalisation, locale data and formatting concepts.
13. [OpenTelemetry Documentation](https://opentelemetry.io/docs/) — vendor-neutral telemetry concepts for traces, metrics and logs.
14. [PostgreSQL Documentation](https://www.postgresql.org/docs/) — database features, transactions, indexes and administration.
15. [GitHub Actions Documentation](https://docs.github.com/en/actions) — automation and CI workflows.

---

## Chapter conclusion

Ek social platform banana coding task se bada project hai. Pehle audience aur problem ko validate karo; phir clear product promise, scope, requirements aur safety baseline define karo. Uske baad architecture aur technology choose karo. MVP ko controlled manner mein test karo, launch readiness prove karo, aur real usage ke basis par iterate karo.

**Next chapter:** `04_TECHNOLOGY_FOUNDATIONS.md` — computer hardware, software, programming languages, operating systems, networking, protocols, servers, Git and developer tools: history, purpose, internal working and practical exercises.
