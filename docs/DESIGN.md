# Şeftali — Nectar design system

Warm neutrals instead of grey, one peach accent, the note itself front and center.
Origin color: Pantone Peach Fuzz `#FFBE98`. All text colors meet WCAG AA (4.5:1).

## Tokens
| Token | Light | Dark | Use |
| --- | --- | --- | --- |
| `--bg-base` | `#FFF9F5` | `#17120F` | Editor background |
| `--bg-surface` | `#FFFFFF` | `#211915` | Cards, popovers, modals |
| `--bg-sunken` | `#FFF1E8` | `#1B1411` | Sidebars |
| `--border` | `#F3DDCF` | `#3A2C25` | Lines, dividers |
| `--text-normal` | `#2E1F18` | `#F7EBE3` | Body text |
| `--text-muted` | `#7A5E51` | `#B89C8D` | Secondary text |
| `--peach-soft` | `#FFE0CC` | `#4A3026` | Selection, hover, tag background |
| `--peach` | `#FFBE98` | `#FFBE98` | Active tab indicator, highlights |
| `--accent` | `#B4471F` | `#FFB38A` | Links, primary buttons, focus ring |
| `--leaf` | `#4F7A3D` | `#9CC48A` | Success, completed tasks |

Map every token to Obsidian's variable names too (`--background-primary`, `--background-secondary`,
`--text-normal`, `--text-muted`, `--interactive-accent`, `--text-accent`, …) so community themes work.

## Type
- UI and editor: Inter. Optional reading font: Literata. Code: JetBrains Mono. All OFL, bundled locally.
- Scale: 12 / 13 / 14 (UI) · 16 (editor body) · 1.6 line height in the editor.

## Shape and motion
- Radius: 10 px cards, 8 px buttons, 6 px chips.
- Shadow: `0 1px 2px rgba(122, 62, 30, 0.06), 0 4px 16px rgba(122, 62, 30, 0.08)`.
- Transitions 150–200 ms ease-out. Respect `prefers-reduced-motion`.

## Rules
- Peach is for interaction and focus only. If a screen is mostly peach, the accent stops working.
- Never hard-code a color in a component. Use tokens.
- Every interactive element has a visible focus state and works with the keyboard.
- Light and dark are designed together; check both before a PR.
