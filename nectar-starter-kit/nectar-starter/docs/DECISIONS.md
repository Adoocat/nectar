# Decision log

Final decisions. Claude Code appends a row whenever it settles an unspecified detail (see CLAUDE.md).
Newest first.

| Date | Decision | Reason |
| --- | --- | --- |
| 2026-11-25 | Code signing (macOS notarization, Windows) happens only after every feature in FEATURES.md is done | Maintainer's choice; until then: SHA256SUMS, GitHub artifact attestations, README guide for Gatekeeper/SmartScreen |
| 2026-11-25 | Nectar plugin API in Phase 5, disabled by default; no Obsidian plugin API compatibility | Compatibility is very large in scope and plugins run code on the user's machine |
| 2026-11-25 | License: AGPL-3.0 | Keeps every derivative open source; same choice as Logseq, Joplin, SiYuan |
| 2026-11-25 | No Sync and no hosted Publish; README sync guide (Git/Syncthing/Dropbox) + "Export to static site" | No cloud and no servers by design |
| 2026-11-25 | Runs locally: release zip with single-file server, built web UI, launcher | No cloud storage, data stays on the user's computer |
| 2026-11-25 | Stack: Bun monorepo, TypeScript, Vue 3, Hono (see CLAUDE.md) | One language end to end; `bun build --compile` gives single-file executables |
| 2026-11-25 | Settings in `<vault>/.nectar/`; never touch `<vault>/.obsidian/` | Users can keep using Obsidian on the same vault |
| 2026-11-25 | Mobile apps out of scope; responsive UI | A local launcher cannot run on phones |
| 2026-11-25 | Platforms: Windows x64, macOS arm64 + x64, Linux x64; latest Chrome, Edge, Firefox, Safari | Covers nearly all desktop users |
| 2026-11-25 | UI languages: English and Turkish; default theme follows the OS | Maintainer's languages; least surprise |
| 2026-11-25 | Design: "Şeftali" tokens in DESIGN.md | Maintainer's brief: a beautiful, modern peach interface |
