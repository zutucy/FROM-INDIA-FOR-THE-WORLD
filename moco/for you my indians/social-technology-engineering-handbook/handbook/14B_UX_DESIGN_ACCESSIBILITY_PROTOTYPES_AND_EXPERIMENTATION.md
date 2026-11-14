# 14B — UX design, accessibility, prototypes and experimentation

## 1. UX is the whole experience

User experience includes discovery, understanding, task completion, error recovery, trust, control over data and support. Visual styling is only one layer. Good UX makes actions clear, communicates system state and helps users recover when something fails.

## 2. Research and design loop

Understand context → map journey → locate friction → sketch alternatives → prototype → test → revise → measure after release. A Figma prototype cannot prove backend authorization, network behaviour, privacy, performance or error handling.

## 3. Information architecture and journeys

Information architecture organizes navigation and content relationships. Journeys describe user steps and decisions. Map success and failure paths: invalid signup, forgotten password, interrupted upload, private account, blocked user, moderation appeal and deletion request.

For each journey record user goal, entry point, decisions, required data, success state, failure/recovery state and support path.

## 4. Interaction states

Consider default, hover, focus, pressed, loading, disabled, success and error states. Forms need labels, validation, server-side error handling and correction paths. Upload interfaces need progress, retry/resume status and constraints. Empty states should explain what the page means and what action is available. Skeletons should not disguise a permanently failed load.

## 5. Accessibility

Accessibility is not decorative. Use semantic HTML, keyboard navigation, visible focus, meaningful labels, sufficient contrast, text alternatives, captions, accessible errors and reduced-motion support. WCAG 2.2 is a technical reference; test with assistive technologies and users. Automated scanners catch only a subset of barriers.

## 6. Responsive design and performance

Design for content/tasks across viewport sizes, not only named device models. Test slow networks, zoom, long text, translation expansion, touch targets and orientation. Measure Core Web Vitals and real-user performance. An animation can look smooth and still cause latency or motion discomfort.

## 7. Design systems

A design system includes tokens (colour, spacing, typography), components, interaction patterns, content rules and accessibility behaviour. Shared components improve consistency, but not every workflow should be forced into one rigid pattern. Version components and document breaking changes.

## 8. Usability testing

Give participants realistic tasks without telling them exactly where to click. Observe completion, hesitation, errors and interpretation. Ask what they expected. Small qualitative studies reveal usability problems; quantitative data helps estimate prevalence. Do not blame participants when repeated misunderstanding points to a design flaw.

## 9. Experiments and feature flags

Feature flags enable gradual release or rollback without a new deployment. They need owners, expiry/review dates and server-side authorization. A client-side feature flag is not access control.

A/B experiments need clean instrumentation, randomization, pre-defined metrics/guardrails, sample-size reasoning and checks for interference. In networked products, one user's treatment may affect others; cluster designs may be more appropriate.

## 10. Internationalization and localization

Use plain language, consistent terms and error messages not reliant on colour alone. Allow text expansion, Unicode, different date/time/number formats and right-to-left layouts where relevant. Internationalization (i18n) is product architecture; localization (l10n) adapts content and conventions to a region. Avoid hard-coded currency, timezone, country code or legal copy in shared components.

## 11. Exercise

Prototype signup/account recovery. Test keyboard-only use, screen-reader labels, invalid input, slow network and mobile viewport. Ask three people to complete tasks without guidance, record the five largest barriers and iterate.

## Sources

- W3C WCAG 2.2: https://www.w3.org/TR/WCAG22/
- W3C WAI tutorials: https://www.w3.org/WAI/tutorials/
- web.dev Core Web Vitals: https://web.dev/articles/vitals
- GOV.UK Service Manual: https://www.gov.uk/service-manual
