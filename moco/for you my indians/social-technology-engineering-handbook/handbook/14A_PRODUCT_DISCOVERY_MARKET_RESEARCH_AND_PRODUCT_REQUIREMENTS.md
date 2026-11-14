# 14A — Product discovery, market research and product requirements

## 1. A product solves a real problem

A technically impressive app can fail because the problem is not urgent, the audience is unclear or users have no reason to switch. Product discovery reduces this risk before large engineering investment.

Separate: **problem** (what difficulty exists?), **user** (who experiences it and when?) and **solution hypothesis** (what might help and why would it be adopted?). Avoid beginning with “I want an app like X.” Study the job users are trying to do and where current options fail.

## 2. A short history of product thinking

Traditional projects often began with a fixed specification. Software's fast iteration encouraged continuous learning. Agile methods emphasized incremental delivery and collaboration; Lean Startup popularized hypotheses, minimum viable experiments and validated learning; human-centred design emphasized understanding people and testing prototypes. These methods are not substitutes for engineering discipline; they help select what is worth engineering.

## 3. Market and competitor research

Map alternatives, not just direct competitors. An alternative may be a spreadsheet, messaging group, email workflow, offline service, open-source tool or doing nothing.

Research audience segments, jobs-to-be-done, workflow, pain frequency/severity, workarounds, switching cost, trust/privacy expectations, accessibility, willingness to pay, acquisition channels and competitors' strengths/limits. Use public sources and ethical interviews. Do not scrape private communities or collect personal data without a valid basis. A few enthusiastic interviews are not proof of market size.

## 4. User interviews

Ask about past behaviour: “Tell me about the last time you tried to find collaborators” is stronger than “Would you use my app?” Avoid leading questions and pitching during discovery.

Interview flow: context/role → last real occurrence → current steps/tools → time, cost or risk → workaround → decision-maker/constraints → desired outcome. Record with consent, remove unnecessary identifiers and summarize themes. Quotes are not statistically representative.

## 5. Product Requirements Document (PRD)

A useful PRD contains:

- problem and background;
- target and excluded users;
- goals and measurable outcomes;
- scope and non-goals;
- user journeys and edge cases;
- functional requirements;
- non-functional requirements (performance, security, accessibility, reliability);
- data/privacy requirements;
- abuse/moderation cases;
- metrics, dependencies, risks and launch criteria.

Acceptance criteria must be testable. Example: “An invite is accepted only by its intended account before expiry; revoked invites fail; the event is audited; and the UI displays a clear state.”

## 6. MVP does not mean unsafe

A minimum viable product tests the riskiest value hypothesis with the smallest coherent experience. It does not mean broken authentication, missing privacy controls or no support. Prioritize must-have core value, should-have trust/usability, low-cost could-have and not-now items. Rank by uncertainty and risk too: a small UI feature may require major legal or infrastructure work.

## 7. Product metrics

Prefer user-value outcomes: activation (first meaningful task), retention (return and succeed), task success/time, user satisfaction with qualitative context, reliability/support load, paid conversion and gross margin. DAU/MAU and time spent can be useful diagnostics but dangerous as the sole definition of success.

## 8. Roadmaps and decisions

A roadmap communicates outcomes and learning goals, not a guarantee that every idea ships on a specific date. Include dependencies, security/compliance reviews, staffing, unknowns, maintenance and incident capacity. Keep decision records: question, options, evidence, risk, owner and revisit trigger.

## 9. Exercise

Choose one audience and one painful job. Interview five people who actually perform it, with consent and minimum data. Write a one-page problem brief, alternatives map, hypothesis, MVP boundary and three measurable outcomes. Do not start with a long feature wish-list.

## Sources

- GOV.UK user research: https://www.gov.uk/service-manual/user-research
- Nielsen Norman Group research methods: https://www.nngroup.com/articles/user-research-methods/
- Atlassian PRD overview: https://www.atlassian.com/agile/product-management/requirements
- Lean Startup principles: https://theleanstartup.com/principles
