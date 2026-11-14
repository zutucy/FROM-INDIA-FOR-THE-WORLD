# 17D — Startup Finance, Budgeting, Unit Economics and Governance

**Edition:** 13 November 2026  
**Purpose:** Explain how to plan and monitor the money required to build and operate a software product. All numerical examples are illustrative; actual prices, taxes and financing rules vary by country, vendor and contract.

## 1. Separate build cost from operating cost

A software company has one-time and recurring expenses.

**Build/setup costs** may include product research, design, development, initial legal work, security review, domain and brand setup, migration and launch preparation.

**Recurring operating costs** may include salaries/contractors, cloud compute, database, storage, CDN egress, messaging/OTP, payment fees, monitoring, moderation, support, legal/accounting, marketing and insurance.

A product can be technically inexpensive to prototype but expensive to operate at scale. Video delivery, human moderation, customer support and compliance are often omitted from early cost estimates.

## 2. Build a driver-based budget

Instead of writing “cloud: ₹10,000” with no explanation, estimate workload drivers:

- Active users and concurrent users.
- Requests per user per day.
- Average request/response bytes.
- Media uploads per user and average file size.
- Video minutes uploaded and watched.
- Storage retention and derivative count.
- Search queries and analytics events.
- Email/OTP volume.
- Support tickets per active user.
- Reports/moderation volume.

A simplified monthly model:

`Total monthly cost = people + compute + database + storage + network egress + media processing + third-party APIs + security/monitoring + moderation/support + legal/finance + marketing`

For every line item, record unit, quantity, price source, billing period, currency, taxes, assumptions and uncertainty. Re-check pricing before procurement because public cloud rates and free tiers change.

## 3. Unit economics

Unit economics asks whether each customer, account, transaction or unit of usage can contribute positively after attributable costs.

Illustrative terms:

- **ARPU:** average revenue per user over a stated period.
- **Gross margin:** revenue minus direct cost of delivering the service, divided by revenue.
- **CAC:** acquisition spend divided by new customers acquired in the same cohort/period, with careful attribution.
- **LTV:** estimated lifetime contribution from a customer; highly assumption-sensitive.
- **Churn:** users/customers who stop using or paying over a period.
- **Payback period:** time needed to recover acquisition cost from contribution margin.

A simple expression:

`contribution per user = revenue per user - variable infrastructure cost - payment fees - variable support/moderation cost`

This is incomplete if it ignores fixed engineering, legal, management and marketing overhead. Use cohorts and sensitivity ranges rather than a single confident lifetime-value number for an early product with little history.

## 4. Example: media product economics

Imagine a product with free photo/video sharing. Registered users are not enough to estimate costs. Two users may have the same account count but very different storage and streaming behaviour.

Track:

- GB uploaded per active user/month.
- GB stored at end of month.
- GB delivered to viewers/month.
- Transcoding minutes and worker CPU/GPU time.
- Cache hit ratio.
- Average playback bitrate and minutes watched.
- Cost per 1,000 minutes delivered.
- Cost per creator and per active viewer.

Possible cost controls include upload quotas, adaptive streaming, deduplication where safe/legal, lifecycle tiers, derivative retention policies, CDN optimisation and paid plans. Do not lower safety or privacy protection simply to reduce cost.

## 5. Cash flow and runway

Profit and cash flow are not the same. A startup may show accounting revenue but still run out of cash because customers pay late, infrastructure is prepaid, salaries are due or annual expenses arrive together.

Runway estimate:

`runway months ≈ available cash / average monthly net cash burn`

This is a rough planning tool. Build scenarios for lower revenue, higher cloud use, delayed launch, security incident, regulatory work and hiring. Keep enough reserves for taxes, refunds, chargebacks and vendor commitments.

## 6. Pricing and monetisation

Possible models include subscriptions, usage tiers, transactions, marketplace fees, advertising, enterprise contracts, creator tools and paid API access. Each has different incentives and obligations.

- Subscription: predictable recurring revenue, but requires ongoing value and cancellation handling.
- Usage pricing: aligns price with consumption but can create unpredictable bills.
- Advertising: can monetise attention but adds ad-tech, privacy, brand-safety and measurement complexity.
- Marketplace fee: depends on successful transactions, dispute resolution and payments infrastructure.
- Enterprise: higher contract value but longer sales cycles, security reviews and support expectations.

Do not add monetisation before understanding how it changes product incentives. An ad system may create pressure to collect more behavioural data; a subscription may change access expectations; creator payouts require fraud prevention and tax workflows.

## 7. Financial controls

- Separate personal and company money.
- Use approved purchasing and reimbursement rules.
- Restrict billing-account permissions.
- Set cloud budgets and alerts.
- Review invoices and usage anomalies.
- Record vendor commitments and renewal dates.
- Reconcile payment processor reports with accounting records.
- Maintain tax and statutory records according to local law.
- Require extra approval for high-value or sensitive purchases.

Never give every developer owner-level billing and production access just because the team is small.

## 8. Funding and ownership

Funding options can include founder capital, revenue, grants, incubators, accelerators, angel investment, venture capital, debt and strategic partnerships. Each affects control, dilution, repayment, reporting and future fundraising. Eligibility, securities regulation, foreign investment rules and tax treatment vary by country. Obtain qualified advice before accepting money or issuing equity.

A pitch deck is not a financial model. Build a transparent model that states assumptions, cash needs, milestones, hiring plan, margin, downside scenario and how the money will be used.

## 9. Exercises

1. Build three monthly budgets: prototype, private beta and public launch.
2. Estimate cost for 1,000, 10,000 and 100,000 monthly active users using declared traffic assumptions.
3. Calculate contribution margin for free, subscription and advertisement-supported plans.
4. Create a 12-month cash-flow forecast with pessimistic/base/optimistic cases.
5. Identify which costs increase linearly, stepwise or non-linearly with usage.

## Further references

- SBA financial management resources: https://www.sba.gov/business-guide/manage-your-business/manage-your-finances
- Y Combinator startup library: https://www.ycombinator.com/library
- Cloud pricing calculators (re-check current prices): https://calculator.aws/ and https://cloud.google.com/products/calculator
- OECD SME and entrepreneurship resources: https://www.oecd.org/industry/smes/
