# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A growing collection of standalone educational HTML pages on software engineering and design principles — aimed at engineers working with AI. Each page is self-contained (no build step, no package manager, no external dependencies beyond Google Fonts).

## Development

Open any page directly in a browser or serve the root via any static file server:

```bash
# Python
python -m http.server 8080

# Node (npx)
npx serve .
```

No build, lint, or test commands exist.

## Pages

| File | Topic |
|------|-------|
| `first-principles.html` | First Principles thinking applied to software engineering with AI |
| `occams-razor.html` | Occam's Razor applied to software design (planned) |

When adding a new page, follow the conventions established in `first-principles.html` (see below) and add a row to this table.

## Page Architecture

Each page is a self-contained HTML file. All CSS and JS are embedded — no external `.css` or `.js` files.

### CSS conventions

- CSS custom properties on `:root` for dark mode (default) and `[data-theme="light"]` for light mode
- `@media (prefers-color-scheme: light)` applied to `:root:not([data-theme="dark"])` for OS preference detection
- Standard variable names to reuse across pages: `--bg`, `--surface`, `--surface2`, `--border`, `--accent`, `--accent2`, `--accent3`, `--text`, `--muted`, `--danger`, `--toggle-bg`, `--toggle-border`
- Layout via CSS Grid and Flexbox; scroll-triggered animations via Intersection Observer

### JavaScript conventions

- Theme toggle: fixed `#theme-toggle` button, persists choice to `localStorage` under key `theme`
- Expandable cards: `togglePrinciple(el)` pattern — toggling an `.active` class
- Interactive quiz: `answer(btn, correct)` pattern — immediate inline feedback

### Shared UX patterns

- Sticky nav with section anchors (`#what`, `#principles`, etc.)
- Numbered section labels (e.g. `01/Foundation`, `02/Core Framework`)
- Expandable principle/concept cards
- Anti-pattern comparison table (wrong approach vs. right approach)
- Worked case study section
- Multiple-choice quiz (3 questions)
- Quick-reference cheatsheet grid

## Topic Guidelines

Each page should cover one mental model or principle from software engineering or design. Strong candidates for future pages:

- **Occam's Razor** — prefer simpler solutions; avoid over-engineering
- **Separation of Concerns** — isolating responsibilities to reduce coupling
- **Abstraction Layers** — when to abstract and when not to
- **The YAGNI Principle** — not building for hypothetical futures
- **Conway's Law** — how team structure shapes system architecture
- **Postel's Law** — be conservative in what you send, liberal in what you accept
- **The Pit of Success** — designing APIs and systems that make the right thing easy
- **Chesterton's Fence** — understand why something exists before removing it

Each topic should include: definition, core framework/principles, applied workflow, anti-patterns, a worked software case study, a quiz, and a cheatsheet.

### Theme System

Two complete color palettes defined as CSS variables on `:root` (dark, default) and `[data-theme="light"]`. Toggle persists to `localStorage` under key `theme`.
