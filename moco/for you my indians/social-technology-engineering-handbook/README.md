# Social & Technology Engineering Handbook

> **How does one tap on a screen become data travelling across the world, stored safely, ranked by algorithms and delivered back in milliseconds?** This handbook follows that journey—from the history of computing to the systems, teams and rules behind real digital products.

**Project creator & curator:** Vedansh Mandloi  
**AI assistance:** ChatGPT (GPT-6)  
**Release:** 1.0.0 · 14 November 2026  
**Format:** 65 Markdown learning documents · 19 numbered parts (`00`–`18`)  
**Language style:** Accessible technical English with a Hinglish-friendly study approach

---

## Start with a question

New to the subject? Don't start by memorising technology names. Pick a question that genuinely makes you curious:

- [**QUESTION.md — 66 questions that lead you through the handbook**](QUESTION.md)

For the complete syllabus and chapter-by-chapter map, open the [master roadmap](handbook/00_START_HERE_AND_MASTER_MAP.md). For authorship and limitations, read [About this handbook](handbook/ABOUT_THIS_HANDBOOK_GPT6.md).

## What this repository teaches

This is **not only a social-media guide**. Social platforms are used as familiar examples, but the curriculum spans the wider technology stack and the work required to operate real products.

| Parts | Learning area | What you explore |
|---|---|---|
| `00–03` | Orientation, history and product thinking | How the Internet and social platforms emerged; how to turn an idea into a build plan |
| `04–05` | Computing foundations | Hardware, operating systems, programming languages, networking and Internet protocols |
| `06–07` | Application engineering | Browsers, frontend, backend, APIs and software architecture |
| `08–10` | Data and production infrastructure | Databases, media, search, real-time systems, cloud, deployment and reliability |
| `11–13` | Security and advanced systems | Cybersecurity, ethical testing, data/AI, machine learning and distributed systems |
| `14–15` | Product and global operations | UX, business models, growth, privacy, regulation and regional operations |
| `16–17` | Responsible operation | Trust and safety, moderation, copyright, QA, teams, support and finance |
| `18` | End-to-end capstone | A connected reference architecture, data/API design, launch gates and runbooks |

## Recommended learning order

1. Read [`QUESTION.md`](QUESTION.md) and choose one question.
2. Read [`handbook/00_START_HERE_AND_MASTER_MAP.md`](handbook/00_START_HERE_AND_MASTER_MAP.md).
3. Study Parts `01–05` for history and foundations.
4. Study Parts `06–10` to understand how applications are built and operated.
5. Study Parts `11–13` for security, data/AI and distributed systems.
6. Study Parts `14–17` for product, law, safety and company operations.
7. Finish with Part `18`, then build a small project and test what you learned.

Helpful companions:

- [Hinglish glossary and study guide](handbook/HINDI_GLOSSARY_AND_STUDY_GUIDE.md)
- [Gap-fill supplement for Parts 00–10](handbook/GAP_FILL_SUPPLEMENT_00_10.md)
- [Quality audit and cross-part gap register](handbook/QUALITY_AUDIT_AND_CROSS_PART_GAP_REGISTER.md)
- [Dated technology and source register](handbook/VERSION_STATUS_AND_SOURCE_REGISTER_2026-11-13.md)
- [AI-assistance and authorship note](handbook/ABOUT_THIS_HANDBOOK_GPT6.md)
- [Community expectations](CODE_OF_CONDUCT.md) · [Security reporting](SECURITY.md) · [Learning support](SUPPORT.md)

## What makes a good way to study this?

For each technology, ask eight questions:

1. **Origin:** What problem existed before it, and who helped create it?
2. **Purpose:** Why was it built? What trade-off was it trying to improve?
3. **Internals:** What happens inside it, step by step?
4. **Use:** Where is it used in a real product or company?
5. **Alternatives:** What else could solve the same problem?
6. **Failure:** What breaks, becomes slow, expensive or unreliable?
7. **Safety:** What security, privacy, accessibility or abuse risks appear?
8. **Practice:** How can you test it safely and prove that it works?

Do not try to learn every technology at once. Build small labs, document failures, test assumptions and revisit the architecture as your understanding improves.

## Repository structure

```text
social-technology-engineering-handbook/
├── README.md                         # Project landing page
├── QUESTION.md                       # Curiosity-driven question index
├── LICENSE                           # Full standard CC BY-NC-ND 4.0 legal code
├── LICENSE-NOTICE.md                 # Project-specific attribution and scope
├── COPYRIGHT_AND_ATTRIBUTION.md      # Plain-language rights and credit guide
├── CONTRIBUTING.md                   # How to report errors and suggest improvements
├── CODE_OF_CONDUCT.md                # Community expectations
├── SECURITY.md                       # Responsible security/content reporting
├── SUPPORT.md                        # Where to ask learning questions
├── GITHUB_PUBLISHING_GUIDE.md        # Repository setup instructions
├── CITATION.cff                      # Citation metadata
├── CHANGELOG.md                      # Release history
├── .github/ISSUE_TEMPLATE/           # Structured correction/question forms
└── MANIFEST_SHA256.txt               # Integrity checksums
└── handbook/                         # All 65 original curriculum/reference Markdown files
```

All 65 original handbook Markdown documents are preserved in `handbook/`. The repository adds navigation, licensing, attribution, publishing guidance and the question index; it does not replace the curriculum with a summary.

## Credit and attribution

This project was initiated and curated by **Vedansh Mandloi**, with drafting, research organization and editorial assistance from **ChatGPT (GPT-6)**. ChatGPT is credited as an AI assistance tool, not represented as a human author or copyright owner. See [the authorship note](handbook/ABOUT_THIS_HANDBOOK_GPT6.md).

When referring to the project, use: **“Social & Technology Engineering Handbook — created and curated by Vedansh Mandloi with assistance from ChatGPT (GPT-6).”**

## License — read this before reusing the material

The original educational text and compilation are offered under **Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International (CC BY-NC-ND 4.0)**, to the extent the project creator holds licensable rights. The root `LICENSE` file contains the standard legal code; [`LICENSE-NOTICE.md`](LICENSE-NOTICE.md) explains how the license applies to this project. This allows people to read and study the material and to share unchanged copies for non-commercial purposes with proper attribution. It does **not** allow commercial use or public distribution of modified/adapted versions without separate permission.

**Important terminology:** this repository is public and source-available for learning, but it is **not “open source” under the Open Source Initiative's definition**, because the license restricts commercial use and distribution of adapted material. If your goal is collaborative open-source editing and unrestricted reuse, the license must be changed to one that permits those freedoms. Read [`LICENSE`](LICENSE) and [`COPYRIGHT_AND_ATTRIBUTION.md`](COPYRIGHT_AND_ATTRIBUTION.md) before publishing.

## Accuracy, safety and limitations

- The source/version register is a dated snapshot, not a promise that every tool, price, framework release or law remains current.
- Country-specific legal chapters are an engineering orientation, not a complete legal inventory or legal advice.
- Architecture examples are learning patterns, not universal prescriptions or production certification.
- Run security labs only on systems you own or are explicitly authorised to test.
- Never commit real passwords, API keys, private keys, personal data or confidential information.
- A real product still needs product-specific security review, privacy/legal review, accessibility testing, load testing, tested backups, incident ownership and operational support.

## Suggested GitHub repository metadata

- **Repository name:** `social-technology-engineering-handbook`
- **Description:** `A Hinglish-friendly, history-first learning handbook covering computing, software engineering, networking, cybersecurity, AI, distributed systems, product design and global technology operations.`
- **Suggested topics:** `computer-science`, `software-engineering`, `web-development`, `networking`, `cybersecurity`, `artificial-intelligence`, `distributed-systems`, `technology-education`, `hinglish`, `learning-resource`

See [`GITHUB_PUBLISHING_GUIDE.md`](GITHUB_PUBLISHING_GUIDE.md) for the publishing steps.
