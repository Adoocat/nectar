# Nectar architecture

Everything runs on the user's computer. Nothing leaves it.

```
Launcher (start.bat / start.command / start.sh)
  ├─ starts ──────────────► nectar executable (Bun + Hono, 127.0.0.1:<port>)
  │                            │  reads / writes / watches
  │                            ▼
  │                         Vault folder on disk (.md, .canvas, attachments, .nectar/)
  └─ opens browser ──────► http://127.0.0.1:<port>/#token=<random>
                             Vue UI  ◄── REST + WebSocket (token on every request) ──► server
```

## Release zip layout
```
nectar-<version>-<os>-<arch>.zip
  nectar(.exe)        single-file server (bun build --compile)
  web/                built UI (vite build)
  start.bat | start.command | start.sh
  LICENSE  README.md  SHA256SUMS
```

## Repo layout
```
apps/web        Vue 3 UI
apps/server     local server
  src/security/ token, host/origin checks, path confinement  (CODEOWNERS: maintainer)
packages/core   shared types, Markdown/link/tag parsing, vault model
docs/           FEATURES, ARCHITECTURE, DESIGN, DECISIONS, design/ mockups
tests/fixtures/test-vault   reference vault for unit and e2e tests
```

## Responsibilities
- **Server:** file I/O confined to the vault, file watching, link/tag/search index (cached in `.nectar/cache/`),
  file recovery snapshots, settings persistence. Pushes file-change events over WebSocket.
- **UI:** editor, rendering, panels, views. Never touches the disk directly.
- **Core:** pure functions shared by both (parse a note → links, tags, headings, blocks, properties).

## API contract (initial)
All routes under `/api`, header `X-Nectar-Token` required, bodies validated with Zod.
- `GET  /api/vault` · `POST /api/vault/open`
- `GET  /api/files` (tree) · `GET /api/file?path=` · `PUT /api/file` · `POST /api/file/move` · `DELETE /api/file`
- `GET  /api/search?q=` · `GET /api/links?path=` (backlinks/outgoing)
- `GET  /api/settings` · `PUT /api/settings`
- `WS   /api/events?token=` (file created/changed/deleted, index updated)

Update this file whenever the contract changes.
