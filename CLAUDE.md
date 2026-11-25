# Nectar — Project rules for Claude Code

Nectar is an open-source (AGPL-3.0) note-taking app with **feature parity with Obsidian: nothing missing, nothing extra**.
It is a web app that runs **only on the user's own computer**: a release zip contains a single-file `nectar` executable
(local server), the built web UI and a launcher. No cloud, no accounts, no database server.

The maintainer is Demirkan. **Talk to him in Turkish.** Code, comments, commit messages, PRs and docs are in English.

## Read these first
- `docs/FEATURES.md` — the parity checklist. It defines scope. Do not build anything that is not on it.
- `docs/ARCHITECTURE.md` — how launcher, server and UI fit together; API contract.
- `docs/DESIGN.md` — the "Şeftali" (peach) design system. Never hard-code colors; use the CSS variables.
- `SECURITY.md` — threat model. Security rules below are non-negotiable.
- `docs/design/mockup-light.png` and `mockup-dark.png` (+ `.html` sources) — approved look of the main screen.
  Match its layout and feel; `docs/DESIGN.md` stays the source of truth for tokens.

## Test vault and expected behavior
- `tests/fixtures/test-vault/` is the reference vault (29 notes, canvas, base, attachments, a security note).
  Start at `Hoş geldin.md`; each note says what it tests. Unit and e2e tests use it.
- Tests must never modify it in place: copy it to a temp directory first.
- Demirkan does not use Obsidian. Expected behavior comes from https://obsidian.md/help — read the relevant
  page before implementing a feature and link it in the PR. Do not ask him how Obsidian behaves.
- `01 Markdown/Güvenlik testi.md` must render with nothing executed and no network request made; keep an e2e test for it.

## Final decisions (do not ask about these again)
Full log with reasons: `docs/DECISIONS.md`.
- License: **AGPL-3.0**.
- Sync and hosted Publish are not built. Local replacements: a README guide for syncing the vault folder
  with Git/Syncthing/Dropbox, and an "Export to static site" feature.
- Plugins: Nectar's own plugin API in Phase 5, disabled by default. No Obsidian plugin API compatibility.
  Themes and CSS snippets come earlier.
- Code signing: **only after every feature in `docs/FEATURES.md` is done.** Until then releases are unsigned,
  with SHA256SUMS, attestations and a README section on getting past Gatekeeper/SmartScreen.
- Mobile apps: out of scope. The UI must still work on narrow windows.
- Platforms: Windows x64, macOS arm64 + x64, Linux x64. Browsers: latest Chrome, Edge, Firefox, Safari.
- UI languages: English and Turkish. Default theme follows the OS (light/dark).

## When something is not specified (keep moving)
Do not stop to ask about small details. Decide, record, continue:
1. Pick the behavior closest to Obsidian's documented behavior.
2. If Obsidian gives no answer, pick the simplest option consistent with `docs/DESIGN.md` and the security rules.
3. Add one row to `docs/DECISIONS.md` (date, decision, reason) in the same PR and mention it in the PR description.

Ask Demirkan **only** when a choice would: change scope (add or drop a feature), weaken a security rule,
add a paid service or a dependency that is not AGPL-compatible, change a decision listed above,
or be hard to undo (data format on disk, public API).

## Stack (do not change without asking)
- Bun workspaces monorepo, TypeScript everywhere (`strict: true`).
- `apps/web`: Vue 3 + Vite + Pinia, plain CSS with CSS variables (no Tailwind), Reka UI, Lucide icons,
  CodeMirror 6, unified/remark, MathJax 3, Mermaid, Shiki, dockview, graphology + sigma.js, Vue Flow, pdf.js.
- `apps/server`: Bun + Hono + Zod, chokidar, MiniSearch. Compiled with `bun build --compile`.
- `packages/core`: shared types, Markdown/link/tag parsing, vault model. No DOM, no Node-only APIs.
- Tests: Vitest (unit), Playwright (e2e + visual). Lint/format: Biome. Typecheck: vue-tsc / tsc.

## Commands
- `bun install` · `bun run dev` · `bun run test` · `bun run test:e2e`
- `bun run lint` · `bun run typecheck` · `bun run build` · `bun run release` (CI only)

## How we work
1. One feature per session and per branch: `feat/<short-name>`, `fix/<short-name>`.
2. Start in plan mode. Present the plan in Turkish, wait for approval.
3. Before implementing a feature, look up its documented behavior on obsidian.md/help and match it.
   If behavior is unclear, ask instead of guessing.
4. Write the test first, then the code.
5. **Definition of done:** tests pass, `bun run lint` and `bun run typecheck` pass, the item is ticked in
   `docs/FEATURES.md`, and a PR is opened with `gh pr create` describing what changed and how it was tested.
6. Small, focused commits (Conventional Commits: `feat:`, `fix:`, `test:`, `docs:`, `chore:`).
7. Never delete or weaken a test to make it pass. If a test seems wrong, explain why and ask.

## Security rules (never break these)
- Server binds to `127.0.0.1` only. Never `0.0.0.0`.
- Every HTTP and WebSocket request must carry the per-launch session token; compare in constant time.
- Validate `Host` and `Origin` on every request. Send no CORS headers.
- Every path from the client is resolved (realpath) and must stay inside the vault root. Reject otherwise.
- Validate every request body with Zod.
- Sanitize rendered HTML with DOMPurify; keep the strict CSP; Mermaid `securityLevel: 'strict'`;
  embeds and Web viewer only in sandboxed iframes.
- No telemetry and no outbound network requests by default. Bundle fonts and icons.
- Never read, print or commit `.env` files, tokens or keys.
- Changes under `apps/server/src/security/` must be called out explicitly in the PR description.

## Dependencies
- Before adding a dependency: check its license is AGPL-3.0 compatible, check it is maintained,
  and prefer pure-JS packages (native modules break single-file compilation). State all three in the PR.
- Commit `bun.lock`. Never bump major versions silently.

## Vault compatibility
- Read and write Obsidian-flavored Markdown and JSON Canvas exactly as Obsidian does.
- Store Nectar settings in `<vault>/.nectar/`. Never read or modify `<vault>/.obsidian/`.
- Never modify a user's file unless the user performed an action that should modify it.
