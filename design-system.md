# Design System: Editorial Dark

A high-contrast, typographically-driven design that feels like a premium technical publication or design studio — clean, intellectual, minimal noise.

---

## Typography (3-font system)

| Role | Font | Use |
|------|------|-----|
| **Display** | Playfair Display (serif) | Hero titles, section headings — creates editorial gravitas |
| **Body** | Syne (sans-serif) | UI text, body copy — geometric, modern |
| **Code/Labels** | DM Mono (monospace) | Section labels, tags, nav pills — adds technical precision |

The interplay between the *serif headline* and the `monospace label` above it is the signature visual gesture.

---

## Color System

**Dark mode (default):** Near-black base (`#0a0a0f`) with a slight blue-violet tint — not pure black, which keeps it from feeling harsh.

**Three accent colors** serve distinct roles:
- `--accent` (gold `#e8c547`) — primary highlights, active states, emphasis
- `--accent2` (violet `#7c6af0`) — section labels, secondary UI
- `--accent3` (cyan `#47c5e8`) — tertiary highlights

**Light mode** uses a warm off-white (`#f5f4ef`) rather than pure white — avoids clinical harshness.

### Full palette

```css
/* Dark (default) */
--bg: #0a0a0f;
--surface: #111118;
--surface2: #1a1a25;
--border: #2a2a3a;
--accent: #e8c547;
--accent2: #7c6af0;
--accent3: #47c5e8;
--text: #e8e8f0;
--muted: #6b6b80;
--danger: #e84747;

/* Light */
--bg: #f5f4ef;
--surface: #fffffe;
--surface2: #eeecea;
--border: #d8d5ce;
--accent: #c4961a;
--accent2: #5b4fd4;
--accent3: #1a9dbf;
--text: #1a1a28;
--muted: #7a7870;
--danger: #c43030;
```

---

## Texture & Depth

- SVG **noise/grain overlay** on `body::before` at 40% opacity — adds a tactile, paper-like quality
- **Radial gradient glows** behind the hero (violet top-right, gold bottom-left) — create spatial depth without distraction
- **Three surface depth levels:** `--bg` → `--surface` → `--surface2`

```css
/* Noise overlay */
body::before {
  content: '';
  position: fixed;
  inset: 0;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
  pointer-events: none;
  z-index: 1000;
  opacity: 0.4;
  mix-blend-mode: multiply;
}

/* Hero glows */
.hero::before {
  /* violet, top-right */
  background: radial-gradient(circle, rgba(124,106,240,0.15) 0%, transparent 70%);
}
.hero::after {
  /* gold, bottom-left */
  background: radial-gradient(circle, rgba(232,197,71,0.08) 0%, transparent 70%);
}
```

---

## Layout Patterns

- **Full-viewport hero** with staggered fade-up animations on load
- **Max-width 1200px** sections with generous `6rem` vertical padding
- **Left-bordered definition blocks** (`border-left: 3px solid var(--accent)`) — newspaper/book quote convention
- **Numbered section labels** like `01 / Foundation` in DM Mono above Playfair section titles

---

## Interaction Details

- Scroll-triggered **fade-in animations** via Intersection Observer
- **Expandable cards** toggle an `.active` class
- **Pill navigation** with rounded borders that glow gold on hover
- **Scroll hint** at the bottom of the hero: animated sliding gold line + monospace label
- **Square theme toggle** (no `border-radius`) — deliberately architectural, not pill-shaped

---

## Minimum Viable Kit

To replicate this style on any new page:

1. Load the three Google Fonts:
   ```html
   <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;0,900;1,400;1,700&family=DM+Mono:wght@300;400;500&family=Syne:wght@400;600;700;800&display=swap" rel="stylesheet">
   ```
2. Apply the CSS variable palette (dark + light) to `:root` and `[data-theme="light"]`
3. Add the noise overlay SVG on `body::before`
4. Hero structure: DM Mono eyebrow label → Playfair Display title → Syne body text
5. Gold `border-left` on definition/blockquote elements
6. Staggered `fadeUp` animation on hero children using `animation-delay`

---

## The Vibe

**Brutalist Editorial** — grid-based structure, classical serif typography (Playfair), dark palette with colored glows. Avoids generic "dark mode SaaS" by leaning into serif type and warm gold rather than blue as the primary accent. Feels like a premium technical publication.
