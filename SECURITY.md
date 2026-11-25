# Security policy

## Reporting a vulnerability
Please **do not** open a public issue. Use GitHub's private vulnerability reporting
(Security tab → "Report a vulnerability"). You will get a reply within 7 days.

## Supported versions
Only the latest release receives security fixes.

## Threat model
Nectar runs a local server on the user's computer. The main threats and our defenses:

| Threat | Defense |
| --- | --- |
| Another device on the network reaches the server | Bind to `127.0.0.1` only |
| A website the user visits sends requests to `localhost` (CSRF) | Per-launch random token required on every request; `Origin` check; no CORS headers |
| DNS rebinding | `Host` header must be `127.0.0.1:<port>` or `localhost:<port>` |
| Path traversal / symlink escape | Every path resolved with realpath and confined to the vault root |
| Malicious note content (shared vaults) | DOMPurify, strict CSP, Mermaid strict mode, sandboxed iframes |
| Tampered release download | Releases built only in CI; SHA256SUMS and GitHub artifact attestations (`gh attestation verify`) |
| Malicious plugins | Plugins disabled by default; explicit opt-in with warning |

Nectar sends no telemetry and makes no outbound network requests by default.
