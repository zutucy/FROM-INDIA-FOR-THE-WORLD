# 06B — HTML, CSS, Accessibility and Responsive Design

## 1. Why HTML and CSS exist

The web needed a common way to describe linked documents and a separate way to control presentation. HTML describes the meaning and structure of content; CSS describes how that content should be presented across screen sizes, devices and user preferences. JavaScript adds behaviour where needed. Keeping these responsibilities distinct improves maintainability, accessibility, portability and progressive enhancement.

## 2. Semantic HTML

Semantic HTML uses elements according to their meaning, not merely their default appearance.

- `<header>`: introductory/header region.
- `<nav>`: major navigation links.
- `<main>`: primary page content.
- `<article>`: self-contained composition that could stand independently.
- `<section>`: thematic grouping, usually with a heading.
- `<aside>`: tangential/related content.
- `<footer>`: footer information.
- `<button>`: action.
- `<a>`: navigation to a resource.
- `<form>`, `<label>`, `<input>`: user input.

Do not choose a `div` and imitate a button if a real button works. Native elements already provide keyboard behaviour and accessibility semantics. A clickable `<div>` often creates avoidable accessibility and interaction bugs.

## 3. HTML forms and validation

Forms collect user input. Use labels connected to controls, explain required fields and provide clear errors. Client-side validation improves usability, but the server must repeat validation because clients can be modified or bypassed.

```html
<form action="/signup" method="post">
  <label for="email">Email address</label>
  <input id="email" name="email" type="email" autocomplete="email" required>
  <button type="submit">Create account</button>
</form>
```

Do not assume a browser's `required` or `type=email` is sufficient business validation. Verify ownership of an email through a trusted flow if email ownership matters.

## 4. CSS fundamentals

Core concepts:

- **Cascade:** rules compete according to origin, importance, layers, specificity and source order.
- **Inheritance:** some values flow from parent to child.
- **Box model:** content, padding, border and margin.
- **Layout:** normal flow, Flexbox, Grid, positioning and writing modes.
- **Responsive design:** adapt layout to available space and user settings.
- **Custom properties:** reusable design tokens such as `--space-3` or `--surface`.

Prefer a small, consistent design system over ad-hoc styles. Example:

```css
:root {
  --space-2: 0.5rem;
  --space-4: 1rem;
  --content-width: 72rem;
}

.page {
  width: min(100% - 2rem, var(--content-width));
  margin-inline: auto;
}

.feed-layout {
  display: grid;
  grid-template-columns: minmax(0, 1fr) 18rem;
  gap: var(--space-4);
}

@media (max-width: 48rem) {
  .feed-layout { grid-template-columns: 1fr; }
}
```

Use CSS Grid for two-dimensional layouts and Flexbox for one-dimensional alignment in many common cases. This is a rule of thumb, not a law.

## 5. Responsive design

A responsive interface should work across narrow phones, large phones, tablets, laptops, desktops, zoom levels and varying text sizes.

Design around content breakpoints rather than naming specific devices. Test:

- narrow viewport and landscape orientation;
- browser zoom and large text;
- touch targets and pointer devices;
- virtual keyboard covering form controls;
- image/video aspect ratios;
- long usernames and translated text;
- reduced motion;
- light/dark and high-contrast preferences.

Do not just shrink desktop UI. Mobile layouts may need different navigation patterns, interaction order and information hierarchy.

## 6. Accessibility is a product requirement

Accessibility helps users with visual, auditory, motor, cognitive and situational constraints. It also improves product robustness.

Practical baseline:

- Every form input has a programmatic label.
- All interactive controls work with keyboard.
- Focus is visible and not trapped unexpectedly.
- Heading hierarchy makes sense.
- Images have meaningful alternative text when informative; decorative images use empty alt text.
- Video has captions where applicable; audio has transcripts where useful.
- Colour is not the only way to convey status.
- Text and controls have sufficient contrast.
- Errors identify the field and explain how to fix them.
- Modal dialogs manage focus and close behaviour correctly.
- Motion can be reduced when users request it.

Use WCAG as a reference and test with automated tools plus keyboard and assistive technology. Automated checks catch only a portion of accessibility issues.

## 7. Design systems and component libraries

A design system is a shared set of design decisions, tokens, components, usage rules and accessibility patterns. It is not only a folder of buttons.

Build tokens for:

- colour roles (surface, text, border, danger, success);
- spacing scale;
- typography and line height;
- radii and elevation;
- responsive breakpoints;
- motion duration/easing;
- focus and disabled states.

Components should have defined states: default, hover, focus, active, disabled, loading, error and empty. Avoid creating abstractions before you understand repeated patterns; premature component systems become harder to change than duplicated simple code.

## 8. Content and localisation

Global products need more than translation. Support right-to-left scripts where required, date/time/number formats, plural rules, local address formats and longer text. Avoid embedding user-visible strings inside logic. Store timestamps in a consistent machine format (commonly UTC instants) and display them using the viewer's locale/time zone, while preserving the relevant event's actual time zone when the concept requires it.

## 9. Practical lab

Create a responsive profile page with:

1. Semantic header, navigation, main and footer.
2. Accessible profile edit form.
3. Responsive two-column desktop layout that becomes one column on mobile.
4. Visible keyboard focus.
5. Proper image alt text.
6. Loading, empty and error states.
7. A keyboard-usable modal.
8. A reduced-motion variant.

Run an accessibility checker, then test manually with keyboard-only navigation and a screen reader if available.

## 10. Common mistakes

- Using clickable `div` elements instead of buttons/links.
- Removing outlines without a replacement focus indicator.
- Setting fixed widths that overflow on phones.
- Using colour alone for meaning.
- Writing CSS selectors so complex that small changes break unrelated screens.
- Treating translations as a final cosmetic step.
- Trusting frontend validation without backend validation.

## Further reading

- MDN HTML: https://developer.mozilla.org/en-US/docs/Web/HTML
- MDN CSS: https://developer.mozilla.org/en-US/docs/Web/CSS
- W3C WCAG 2.2: https://www.w3.org/TR/WCAG22/
- W3C WAI tutorials: https://www.w3.org/WAI/tutorials/
- WHATWG HTML Standard: https://html.spec.whatwg.org/
