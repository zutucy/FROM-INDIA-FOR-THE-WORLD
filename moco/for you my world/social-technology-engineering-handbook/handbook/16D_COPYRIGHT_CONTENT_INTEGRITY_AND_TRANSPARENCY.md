# 16D — Copyright, Content Integrity and Transparency

**Edition:** 13 November 2026  
**Purpose:** Explain the systems a digital product needs for copyright claims, authenticity, manipulated media, spam networks, impersonation, transparency and fair enforcement.

## 1. User content creates rights and responsibilities

Users may upload writing, photos, audio, video, logos, software, datasets and other works. The platform may receive a limited licence from the user to host, process, display and distribute that content according to the service terms. Such a licence does not mean the user owns third-party material or that the platform automatically receives every right needed for all uses.

Before launch, map:

- What licence the user grants to the service.
- Whether content can be publicly displayed, embedded, downloaded or remixed.
- Whether the product uses content for recommendation, moderation or AI model training.
- Whether creators can revoke or delete content and what technical/legal limits apply.
- What licences are needed for music, stock media, fonts, maps, datasets and software.
- Whether commercial use, territory, duration and attribution restrictions apply.

Open-source licences also matter. Maintain a software bill of materials and licence inventory; check attribution, notice, copyleft, source-disclosure and patent conditions with qualified counsel where needed.

## 2. Copyright notice workflows

A rights-holder reporting process should identify the work, the allegedly infringing content, the reporter's authority, required declarations and the requested action. The platform should have trained review and a record of each decision.

A general workflow:

`notice received → completeness/authority check → identify content → legal/policy review → temporary or final action as appropriate → notify affected parties → counter-notice/appeal if applicable → restore or retain according to law → repeat-infringer review`

Different jurisdictions have different notice, counter-notice, safe-harbour, knowledge, repeat-infringer and court-order rules. Do not copy a US DMCA form as a global solution. Use jurisdiction-specific legal review.

## 3. Trademark, impersonation and identity

Trademark complaints, impersonation and fraud can overlap but are not identical. Someone using a brand term in criticism or commentary may not be impersonating the brand. A fake account selling goods under a company's name may be deceptive. Review account context, purpose, confusion and the applicable law/policy.

Potential product controls:

- Report identity/impersonation.
- Verification with clear scope and limits.
- Reserved names only with documented criteria.
- Brand and public-figure impersonation escalation.
- Appeals for parody, fan or commentary accounts.
- Warnings against scams and off-platform payment requests.

A verification badge should not imply endorsement, expertise or safety unless that is exactly what the product means and the criteria are clear.

## 4. Synthetic media and AI-generated content

AI-generated images, audio and video can be creative, deceptive or harmful depending on context. Risks include non-consensual sexual deepfakes, impersonation, fake endorsements, fabricated evidence, political manipulation and fraud.

Controls may include:

- Provenance metadata when supported and reliable.
- User labels and disclosure prompts.
- Detection tools used as signals rather than proof.
- Reporting paths for impersonation and non-consensual imagery.
- Rules against deceptive impersonation and fraud.
- Context-sensitive treatment for satire, fiction, education and commentary.
- Appeals where a label or removal is disputed.

Metadata can be stripped, altered or absent. A provenance standard can improve traceability but cannot prove every unlabelled file is authentic. Do not claim that an AI detector can definitively determine truth.

## 5. Coordinated manipulation and platform integrity

Manipulation can involve fake accounts, purchased engagement, bot networks, coordinated reporting, spam campaigns, review fraud and deceptive amplification. Detection may use velocity, graph structure, device/account signals, content similarity and behavioural patterns. These are probabilistic signals; legitimate organisations can also coordinate, and accessibility tools or shared networks can resemble automation.

Use layered detection, risk-based friction, investigation and appeal. Avoid making opaque decisions solely on one signal such as IP address, follower count or text similarity.

## 6. Transparency reporting

A meaningful report may include:

- Government/legal requests by category and jurisdiction.
- Content/account enforcement by policy category.
- Appeal and reversal statistics.
- Copyright notices and counter-notices.
- Automated detection and human review proportions.
- Emergency requests and response counts where lawful to disclose.
- Data about response times and methodology.
- Known limitations and changes in measurement.

Protect users by aggregating sufficiently, suppressing small cells and avoiding exposure of reporters, victims or ongoing investigations. Explain definitions and changes across reporting periods.

## 7. Practical exercise

Create a mock copyright report system with: claimant identity, authority evidence, claimed work, content URL/ID, jurisdiction, requested action, reviewer decision, notice history, counter-notice state and audit events. Use synthetic test data only. Then add a separate impersonation queue and document why the decision standards differ.

## Further references

- WIPO copyright resources: https://www.wipo.int/copyright/en/
- Creative Commons licence chooser: https://creativecommons.org/choose/
- SPDX licence list: https://spdx.org/licenses/
- C2PA specifications: https://c2pa.org/specifications/
- Santa Clara Principles: https://santaclaraprinciples.org/
