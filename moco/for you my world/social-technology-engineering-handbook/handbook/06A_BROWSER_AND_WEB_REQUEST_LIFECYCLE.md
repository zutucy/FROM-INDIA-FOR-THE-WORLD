# 06A — Browser Internals and the Life of a Web Request

> Scope: How a website travels from a URL in a browser to pixels on a screen. This chapter is about the web as a general platform, not only social networks.

## 1. What is a browser?

A browser is a client application that retrieves web resources, interprets web standards, executes scripts in a controlled environment, renders documents and gives people ways to navigate them. Chrome, Firefox, Safari and Edge are products; Chromium, Gecko and WebKit are browser-engine families/components. A browser is not merely a window that displays HTML. It contains networking, storage, rendering, JavaScript execution, security boundaries, accessibility and developer tools.

Typical internal areas include:

- **Browser process:** coordinates tabs, windows, permissions, navigation and user interface.
- **Renderer process:** parses and renders a page and runs much of its JavaScript. Modern browsers commonly isolate sites or documents into processes, though exact designs differ.
- **Network service:** performs DNS resolution, connections, TLS and HTTP requests.
- **GPU process:** helps composite layers and perform graphics work.
- **Storage services:** manage cookies, cache, local storage, IndexedDB and other browser data.

These are conceptual roles, not a guarantee that every browser has identical process boundaries.

## 2. Entering a URL: the full journey

Suppose a person enters `https://example.com/profile/veda`.

1. The browser parses the URL into scheme (`https`), host (`example.com`), path and optional query/fragment.
2. It checks applicable local information such as caches, service-worker rules, connection pools and DNS cache.
3. It resolves the hostname to one or more IP addresses through the configured resolver.
4. It establishes the appropriate transport connection. Depending on HTTP version and deployment, that may use TCP or QUIC.
5. For HTTPS, it establishes TLS and validates the certificate chain and hostname.
6. It sends an HTTP request containing method, path, headers and possibly a body.
7. A CDN, reverse proxy, load balancer or application server may receive the request first.
8. The response returns status, headers and content, or a redirect/error.
9. The browser processes HTML, discovers linked stylesheets, scripts, fonts and media, and requests them as needed.
10. The browser parses and renders the page, then executes application code and responds to user input.

A website load is therefore a sequence of network and local computation steps—not one magical download.

## 3. How a browser turns files into a screen

A simplified rendering pipeline is:

`HTML bytes → tokens → DOM → CSS parsing → CSSOM → style calculation → render tree → layout → paint → compositing`

- **HTML parser:** builds the Document Object Model (DOM), a tree-like representation of document elements.
- **CSS parser:** builds style rules represented conceptually by the CSS Object Model (CSSOM).
- **Style calculation:** determines which styles apply to each visible element.
- **Layout:** calculates geometry—positions and dimensions.
- **Paint:** records drawing operations such as text, borders and images.
- **Compositing:** combines layers into the final displayed frame; browsers may use GPU acceleration for some work.

The pipeline is simplified. Browser engines optimise, parallelise and sometimes skip stages. Changing a property that affects geometry can trigger layout; changing a colour may only require paint; transform/opacity changes may be composited efficiently in suitable cases. Profile before optimising rather than assuming every CSS property has the same cost.

### Why this matters

A page can download quickly but still feel slow if JavaScript blocks the main thread, layout repeatedly recalculates, images are oversized or a large component tree renders unnecessarily. Measure different experiences separately: initial server response, first content, largest content, interaction responsiveness, layout shifts and actual user-perceived performance.

## 4. JavaScript runtime in the browser

The JavaScript engine parses and executes JavaScript. The browser also exposes Web APIs such as timers, DOM, fetch, storage and media APIs. The **event loop** coordinates execution of tasks and microtasks with rendering opportunities. JavaScript on the main thread generally runs one task at a time; a long calculation can block clicks and animation even when the network is fast.

Example:

```js
button.addEventListener('click', async () => {
  button.disabled = true;
  try {
    const response = await fetch('/api/profile');
    if (!response.ok) throw new Error(`HTTP ${response.status}`);
    const profile = await response.json();
    renderProfile(profile);
  } catch (error) {
    showError('Could not load profile. Please retry.');
  } finally {
    button.disabled = false;
  }
});
```

`await` does not mean the browser freezes while waiting for a network response. The asynchronous operation completes later and schedules continuation work. However, heavy synchronous computation still blocks its executing thread. Web Workers can move suitable computation off the main thread, but they do not automatically have access to the DOM.

## 5. Browser storage: do not treat it as a trusted database

Browsers provide several storage mechanisms:

- **Cookies:** often used for server-managed sessions and preferences; attributes such as `HttpOnly`, `Secure` and `SameSite` matter.
- **localStorage:** simple origin-scoped key/value storage, synchronous APIs; avoid storing high-value secrets in it.
- **sessionStorage:** tab/session-scoped key/value storage.
- **IndexedDB:** asynchronous structured client-side storage for larger datasets/offline workflows.
- **Cache Storage:** commonly used by service workers to cache request/response assets.
- **HTTP cache:** caches resources according to response headers and browser rules.

Browser storage may be cleared, evicted or unavailable in private/restricted environments. It is not a substitute for server-side persistence, authorization or backups. Any data returned to a browser should be considered accessible to that user and potentially to malicious scripts running in the origin.

## 6. Same-origin policy and site isolation

The **same-origin policy** restricts how scripts from one origin interact with resources from another. An origin is based on scheme, host and port. CORS is a controlled mechanism that lets servers state which cross-origin browser requests may be shared with scripts; CORS is not authentication and does not stop non-browser clients from making requests.

Browsers use multiple additional protections, such as process/site isolation, sandboxing, permission prompts and content security policies. These reduce attack impact but do not excuse application-level security mistakes.

## 7. Browser developer tools

Learn these panels:

- **Elements/Inspector:** inspect DOM and computed CSS.
- **Console:** view errors and run debugging expressions.
- **Network:** inspect requests, headers, payload sizes, timing and cache.
- **Performance:** record main-thread tasks, layout and rendering bottlenecks.
- **Application/Storage:** inspect cookies, local storage, IndexedDB and service workers.
- **Accessibility:** inspect accessible names, roles and contrast.
- **Security:** inspect certificate and connection information.

Never paste unknown code into the console on a logged-in production account. Console snippets can execute with the page's permissions and access data available to that page.

## 8. Practical lab

1. Open a simple website and inspect its document in Elements.
2. Reload with Network open; identify the document, CSS, JS, font and image requests.
3. Disable cache and compare the load.
4. Inspect a request's status, headers, transferred size and timing.
5. Use Performance to record scrolling or a button interaction.
6. Block one image request and observe the fallback behaviour.
7. Test a page at mobile viewport size and slower network emulation.
8. Inspect cookies and confirm that session cookies have appropriate security attributes.

Only inspect systems and accounts you own or are authorised to test.

## 9. Common mistakes

- Believing the HTML file is the entire website.
- Assuming CORS secures an API.
- Storing authentication secrets in JavaScript-accessible storage without assessing XSS risk.
- Loading huge images when a small responsive version is enough.
- Doing expensive work on the main thread.
- Treating browser cache as permanent storage.
- Hiding errors rather than giving accessible retry states.

## 10. Further reading

- MDN, How browsers work: https://developer.mozilla.org/en-US/docs/Web/Performance/Guides/How_browsers_work
- MDN, Critical rendering path: https://developer.mozilla.org/en-US/docs/Web/Performance/Guides/Critical_rendering_path
- MDN, How the web works: https://developer.mozilla.org/en-US/docs/Learn_web_development/Getting_started/Web_standards/How_the_web_works
- WHATWG HTML Standard: https://html.spec.whatwg.org/
- W3C Web Accessibility Initiative: https://www.w3.org/WAI/
