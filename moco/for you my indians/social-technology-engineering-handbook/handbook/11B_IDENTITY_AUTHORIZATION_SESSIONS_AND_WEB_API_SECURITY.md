# 11B — Identity, authorization, sessions and web/API security

## 1. Identity is not permission

Keep four questions separate: identification (which account is claimed?), authentication (what proves control of it?), authorization (what may that principal do to this resource now?) and accounting (what happened and under whose authority?). A successful login never means “can read every record.” Every sensitive server operation must authorize the exact object and action. Hiding a button in the UI is not a security boundary.

## 2. Authentication methods

### Passwords

Passwords are reusable secrets. Store only salted, deliberately slow password hashes using a maintained password-hashing algorithm such as Argon2id, scrypt or appropriately configured bcrypt. Never store recoverable plaintext passwords or use a fast general-purpose hash such as plain SHA-256 for passwords. Follow current library guidance for parameters.

Add rate limits, breached-password checks where appropriate, generic error messages, secure reset flows, session revocation and protection against credential stuffing. Encourage unique passwords and password managers. Avoid arbitrary forced resets without a reason such as compromise.

### MFA and passkeys

MFA combines independent factors. Authenticator-app codes and hardware security keys are generally more phishing-resistant than SMS OTP, though all methods have recovery and usability issues. Recovery flows are often a weak point; protect recovery codes and notify users of sensitive changes.

Passkeys use public-key cryptography. The authenticator keeps a private credential while the service stores a public key. A challenge is signed; origin and relying-party binding help resist phishing. Passkeys reduce reusable-password risk but do not remove device-loss and account-recovery design requirements.

### OAuth and OpenID Connect

OAuth 2.0 is an authorization framework; OpenID Connect adds an identity layer. Not every access token is an identity token. Use Authorization Code with PKCE for public clients, exact redirect URIs, state and nonce as applicable, issuer/audience/signature/expiry validation and minimum scopes. Do not put confidential client secrets in browser or mobile source code.

## 3. Sessions, cookies and tokens

A server-side session stores state on the server and gives the browser an opaque identifier. This is convenient for revocation but requires a reliable session store. A signed token (for example JWT) carries claims and can be verified without a database lookup, but revocation, stale claims, key rotation and audience confusion become harder. JWT is a token format, not a complete authentication design.

For browser cookies, select `HttpOnly`, `Secure` and `SameSite` settings deliberately. Use narrow domain/path scope, rotate identifiers after login and privilege changes, and define idle/absolute expiry. Avoid long-lived secrets in localStorage when XSS could read them. Offer session review and “log out all devices” for sensitive products.

Access tokens should be short-lived where possible. Refresh-token rotation and reuse detection reduce replay risk. Design logout and revocation explicitly.

## 4. Authorization models

- **RBAC:** Roles map to permissions. Simple, but roles can proliferate.
- **ABAC:** Decisions consider subject, object, action and environment attributes.
- **ReBAC:** Decisions use relationships such as follower, workspace member or collaborator.

Products often combine these. A user may view a post if it is public, owned by them, or shared with an approved follower who is not blocked, subject to higher-level policy.

### Object-level authorization

Never rely on an unguessable UUID as permission. For `/posts/abc`, the server must check whether the requester may read that specific post. This addresses broken object-level authorization (BOLA/IDOR-style issues).

### Multi-tenant isolation

Do not accept a client-supplied tenant ID as proof of membership. Derive or verify membership through authenticated server-side data. Test cross-tenant reads and writes in APIs, exports, search, caches, jobs, webhooks and admin tools.

## 5. Common web/API weaknesses

- **Broken access control:** Verify ownership and relationship at the server on every sensitive route.
- **Injection:** Use parameterized SQL and safe APIs; do not concatenate untrusted input into queries, shell commands or dynamic code.
- **XSS:** Use context-aware output encoding, safe templates, careful rich-text sanitization and tested Content Security Policy. CSP is defense in depth.
- **CSRF:** Use SameSite cookies, anti-CSRF tokens or origin checks based on the design; never use GET for state-changing actions. CORS is not a general CSRF defence.
- **SSRF:** Restrict outbound destinations, validate DNS and resolved IPs, control redirects and egress, and block access to internal metadata/service networks.
- **Misconfiguration:** Remove defaults/debug endpoints, restrict admin surfaces, review CORS and storage policies, and keep errors from exposing internals.
- **Abuse/resource exhaustion:** Rate-limit by account, IP/network, tenant and operation cost. Account for shared networks and privacy.

## 6. Cryptography

Encryption provides confidentiality using keys; hashing produces a one-way digest; MACs authenticate data with a shared secret; digital signatures allow verification using a public key; key-derivation functions derive cryptographic keys. These concepts are not interchangeable.

Use authenticated encryption through maintained libraries, current protocols, managed key systems where appropriate and key separation by purpose/environment. Never invent cryptography. TLS protects traffic in transit, not a compromised endpoint. Encryption at rest does not prevent an authorized application process from reading data.

## 7. Secure upload and media endpoints

Treat every upload as hostile input. Require an authorized action or bound anonymous access; set maximum size and duration; validate file signatures and supported formats; generate server-side random storage keys; quarantine before publication; parse in isolated workers with resource limits; re-encode where sensible; avoid serving active HTML/SVG from a privileged origin; protect logs from leaking private keys/URLs; and ensure deletion covers derivatives, caches, replicas and downstream jobs according to policy.

## 8. API security checklist

- Authenticate and authorize every sensitive operation server-side.
- Validate schemas and bound lengths, arrays, pagination and filter complexity.
- Return only necessary fields; do not expose internal records by default.
- Apply per-account/tenant/resource quotas and cost limits.
- Configure CORS narrowly; never treat it as authentication.
- Redact tokens, passwords, messages and sensitive personal data from logs.
- Use idempotency keys for retryable state-changing operations where appropriate.
- Verify webhook signatures, timestamps and replay protection.
- Document API versions and deprecation for mobile clients.

## 9. Permission testing

Create a matrix of roles—anonymous, owner, follower, blocked user, moderator, support agent, tenant admin and platform admin—against actions such as view, edit, delete, export, report and moderate. Test allowed and denied outcomes. Ensure a second user cannot read drafts, private media, notifications, messages, exports or session records belonging to the first user.

## 10. Exercise

Build a local demo with two accounts and public, follower-only and private resources. Test identifier changes, block state and revoked sessions using your own local test client. Verify the backend denies unauthorized reads even if the frontend is bypassed.

## Sources

- OWASP Top 10:2025: https://top10.owasp.org/2025/
- OWASP API Security: https://owasp.org/www-project-api-security/
- OAuth 2.0 Security BCP (RFC 9700): https://www.rfc-editor.org/rfc/rfc9700
- OpenID Connect Core: https://openid.net/specs/openid-connect-core-1_0.html
- WebAuthn: https://www.w3.org/TR/webauthn-3/
- NIST Digital Identity Guidelines: https://pages.nist.gov/800-63-4/
- OWASP Cheat Sheet Series: https://cheatsheetseries.owasp.org/
