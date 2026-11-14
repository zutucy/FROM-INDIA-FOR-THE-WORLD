# 06C — JavaScript, TypeScript, React and Frontend Architecture

## 1. JavaScript's role

JavaScript became the standard programming language of the browser because browsers needed an embedded language for interactive pages. It later expanded into servers, desktop tooling, build systems and mobile development. The language is standardised through ECMAScript; browsers and runtimes implement that standard plus their own APIs.

Learn in this order: values and types, variables, functions, scope, arrays/objects, modules, errors, promises, async/await, events, DOM, fetch, testing, then framework concepts.

## 2. TypeScript

TypeScript adds a static type system and developer tooling on top of JavaScript. It helps detect many mistakes before runtime and improves refactoring/documentation. Types are generally removed during compilation; they do not validate untrusted JSON at runtime.

```ts
type UserSummary = {
  id: string;
  username: string;
  displayName: string;
};

function profilePath(user: UserSummary): string {
  return `/users/${encodeURIComponent(user.username)}`;
}
```

Do not write `const data = response.json() as UserSummary` and assume that the server actually returned that shape. Parse and validate runtime data with a schema/validation layer.

## 3. React mental model

React builds interfaces from components. A component receives props, may use state and returns a description of UI. State changes trigger rendering; React then reconciles the new UI description with the existing interface.

Important ideas:

- **Components:** small units with a clear responsibility.
- **Props:** input passed from parent to child.
- **State:** data that changes over time and affects rendering.
- **Events:** user interactions such as click, submit and input.
- **Effects:** synchronise with external systems; do not use effects for every calculation.
- **Keys:** stable identity for list items.
- **Context:** share values across a subtree when appropriate.
- **Composition:** combine smaller components instead of building one giant component.

React is not a database, authentication system or backend. A frontend framework cannot enforce access rights to data it should never receive.

## 4. Rendering choices

Web applications can render in several ways:

- **Client-side rendering (CSR):** browser downloads application JavaScript and builds much of the UI on the client.
- **Server-side rendering (SSR):** server generates HTML for a request, then the browser may hydrate it.
- **Static generation:** HTML is generated ahead of time for content that can be built in advance.
- **Incremental/revalidated rendering:** some frameworks refresh generated output under specified policies.
- **Hybrid rendering:** different routes/components use different strategies.

Choose based on content freshness, SEO, user-specific data, latency, hosting model and complexity. Server rendering does not automatically make a page private or secure; server code must still check permissions.

## 5. Next.js and similar frameworks

A full-stack web framework adds routing, build tooling, server rendering, asset handling and server-side capabilities around React. Next.js is one option, not a requirement. Other valid options include React with a different router/build system, Vue/Nuxt, SvelteKit, Angular or plain HTML for smaller projects.

For any framework, learn:

- where code runs (browser vs server);
- which components can access secrets;
- route and data-loading lifecycle;
- cache and revalidation rules;
- error boundaries and not-found handling;
- environment configuration;
- build output and deployment compatibility.

Never expose private API keys by placing them in public frontend environment variables. Assume any value bundled into browser JavaScript can be read by users.

## 6. Frontend state management

Not all data belongs in one global store.

- **Local UI state:** open modal, current tab, temporary input.
- **Server state:** feed pages, profile, comments; needs fetching, caching, invalidation and retry.
- **URL state:** search query, filters, pagination; useful for sharing and browser navigation.
- **Form state:** field values and validation errors.
- **Persistent preferences:** theme or display preference, subject to privacy and storage rules.

Use the simplest solution that meets the need. A server-state library can simplify caching and request lifecycle; a global client store can help shared client-only state. Adding multiple state libraries without boundaries creates confusion.

## 7. Frontend architecture for a larger app

Organise by product feature rather than only technical file type when that helps ownership. Example:

```text
src/
  app/                  # routes and layouts
  features/
    feed/
      components/
      hooks/
      api/
      schemas/
      types/
    profile/
    messaging/
    search/
  components/           # genuinely shared UI
  lib/                  # utilities and framework integrations
  styles/
  test/
```

A feature should know its own view logic and data contracts. Shared components should be generic enough to reuse, but avoid turning every tiny fragment into a shared abstraction.

## 8. Frontend performance

- Split code by route or feature where appropriate.
- Lazy-load heavy components not needed immediately.
- Use responsive images and modern formats.
- Reserve image dimensions to prevent layout shifts.
- Avoid huge client-side bundles.
- Debounce expensive search requests, but keep keyboard interaction responsive.
- Virtualise very long lists where measurement proves a need.
- Avoid unnecessary rerenders; profile first.
- Avoid main-thread work during critical interactions.
- Respect cache headers and invalidation requirements.

## 9. Frontend security

- Treat all user-generated text as untrusted.
- Avoid injecting HTML; if rich HTML is required, sanitise with a maintained, appropriate sanitizer.
- Use a Content Security Policy where suitable.
- Avoid exposing secrets.
- Protect state-changing actions against CSRF where the authentication design requires it.
- Do not assume hidden UI is access control.
- Validate server responses and handle errors safely.
- Do not render private information into HTML that is publicly cacheable.

## 10. Testing

- Unit-test pure functions and validation logic.
- Component-test state and interaction.
- End-to-end-test complete user journeys.
- Test keyboard and accessibility behaviour.
- Test mobile viewport, slow network and empty/error states.
- Add visual regression testing only where it provides value and is maintained.

## 11. Suggested projects

1. A static multi-page site with accessible navigation.
2. A JavaScript application that fetches public API data and handles loading/errors.
3. A React dashboard with forms, filters and paginated data.
4. A secure profile editor backed by your own API.
5. A feed UI that handles duplicate items, optimistic likes, stale data and failed requests.

## Further reading

- React Learn: https://react.dev/learn
- TypeScript Handbook: https://www.typescriptlang.org/docs/handbook/intro.html
- Next.js Docs: https://nextjs.org/docs
- MDN JavaScript Guide: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide
- MDN Fetch API: https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API
