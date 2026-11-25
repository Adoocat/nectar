# Nectar feature parity checklist

Scope = Obsidian's features, nothing missing, nothing extra. Reference: https://obsidian.md/help
(core plugin list: https://obsidian.md/help/Plugins/Core+plugins). Match the documented behavior.

Out of scope by decision: Obsidian Sync (cloud), hosted Publish, mobile apps.
Local replacements: vault folder works with Git/Syncthing/Dropbox (documented in README); "Export to static site".

Tick an item only when its tests pass.

## Phase 0 — Foundation
- [ ] Monorepo skeleton (`apps/web`, `apps/server`, `packages/core`), Biome, TS strict, Vitest, Playwright
- [ ] CI: lint, typecheck, unit, e2e on every PR (Windows, macOS, Linux runners)
- [ ] `.github/dependabot.yml` (weekly, grouped updates for bun and GitHub Actions), `CODEOWNERS`
      (`apps/server/` and `.github/workflows/` → @maintainer), CodeQL code scanning enabled once code exists
- [ ] Local server: 127.0.0.1 only, session token, Host/Origin checks, path confinement, Zod validation
- [ ] Launcher scripts (Windows `.bat`, macOS `.command`, Linux `.sh`) start server and open browser with token
- [ ] Vault: open folder, create new vault, switch vaults, recent vaults list
- [ ] File explorer: tree, create note/folder, rename, move (drag and drop), delete to trash, sort options, reveal active file
- [ ] Settings infrastructure stored in `<vault>/.nectar/`
- [ ] Release workflow: per-OS zip (Windows x64, macOS arm64 + x64, Linux x64), SHA256SUMS, artifact attestation
- [ ] README: install and launch, verifying downloads, getting past Gatekeeper/SmartScreen on unsigned builds,
      syncing a vault with Git/Syncthing/Dropbox

## Phase 1 — Editor and Markdown
- [ ] Editing modes: Live Preview, Source mode, Reading view
- [ ] Internal links `[[note]]`, `[[note#heading]]`, `[[note#^block]]`, `[[note|alias]]`, Markdown links
- [ ] Link autocomplete while typing `[[`
- [ ] Embeds `![[...]]`: notes, headings, blocks, images (with size), audio, video, PDF (with page)
- [ ] Block identifiers `^id`
- [ ] Callouts (all types, foldable, nested)
- [ ] Properties (YAML frontmatter) with typed editor: text, list, number, checkbox, date, date & time
- [ ] Tags, nested tags, tags in properties
- [ ] Highlights `==`, comments `%%`, strikethrough, footnotes (inline and reference)
- [ ] Math (inline and block, MathJax), Mermaid diagrams, code blocks with syntax highlighting
- [ ] Task lists, tables (with editing helpers), horizontal rules, HTML (sanitized)
- [ ] Attachments: drag and drop, paste images, configurable attachment folder
- [ ] Automatically update internal links on rename/move
- [ ] Folding headings and lists, indentation guides, multiple cursors
- [ ] Vim mode, spellcheck (browser), readable line length

## Phase 2 — Navigation and panels
- [ ] Tabs, splits, stacked tabs, linked panes, pinning, back/forward history
- [ ] Left/right sidebars, ribbon, status bar
- [ ] Command palette
- [ ] Quick switcher
- [ ] Customizable hotkeys
- [ ] Search with operators (`file:`, `path:`, `tag:`, `line:`, `block:`, `section:`, `task:`, regex, boolean)
- [ ] Backlinks (linked and unlinked mentions)
- [ ] Outgoing links
- [ ] Outline
- [ ] Page preview (hover)
- [ ] Bookmarks (notes, headings, blocks, searches, folders, groups)
- [ ] Tags view
- [ ] Properties view
- [ ] Footnotes view
- [ ] Word count
- [ ] Random note

## Phase 3 — Workflows
- [ ] Daily notes
- [ ] Templates (with date/time variables)
- [ ] Unique note creator
- [ ] Note composer (merge, extract)
- [ ] Slash commands
- [ ] File recovery (snapshots)
- [ ] Workspaces (save/restore layouts)
- [ ] Audio recorder
- [ ] Slides
- [ ] Importer (Markdown and other apps' export formats)
- [ ] Deep links (Nectar URL equivalent of `obsidian://` actions)

## Phase 4 — Visual views
- [ ] Graph view: global and local, filters, groups, display and force settings
- [ ] Canvas (JSON Canvas): notes, files, text cards, links, groups, edges
- [ ] Bases: table, cards and list views, filters, sorting, formulas, editing properties inline
- [ ] Web viewer (sandboxed; sites that forbid iframes open in a new browser tab)

## Phase 5 — Appearance and extensibility
- [ ] Light/dark mode, accent color, fonts, font size, zoom
- [ ] Third-party themes and CSS snippets (Obsidian CSS variable names mapped)
- [ ] Interface languages: English, Turkish
- [ ] Nectar plugin API (disabled by default, restricted mode warning)
- [ ] Export to static site (local replacement for Publish)

## After feature-complete
Start only when every item above is ticked.
- [ ] Code signing and notarization for macOS; code signing for Windows; add to the release workflow
- [ ] Remove the unsigned-build section from the README
