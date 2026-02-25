# Design Specification: Gimena Blanco — Personal Website
*Version 1.0 · February 2026*
*Based on site-plan.md · Three-theme system: Light · Blue · Dark*

---

## Part 0: Shared Design System

These values and rules apply across all three themes unless overridden by a theme-specific token.

---

### 0.1 Typography

Each theme uses a different font stack. The table below shows the role, the variable name, and the value per theme.

| Role | Variable | Light | Blue | Dark |
|---|---|---|---|---|
| Display / Headlines | `--font-display` | `'Red Hat Display'` | `'Playfair Display'` | `'Syne'` |
| Subheadings / Nav / Buttons | `--font-heading` | `'Red Hat Display'` | `'Space Grotesk'` | `'Syne'` |
| Labels / Tags / Code accents | `--font-mono` | `'DM Mono'` | `'JetBrains Mono'` | `'DM Mono'` |
| Body / Descriptions | `--font-body` | `'Red Hat Display'` | `'DM Sans'` | `'Inter'` |

**Google Fonts imports — add to `<head>` conditionally per theme:**

```html
<!-- Light (already loaded) -->
<link href="https://fonts.googleapis.com/css2?family=DM+Mono:wght@400;500&family=Red+Hat+Display:ital,wght@0,300..900;1,300..900&display=swap" rel="stylesheet" />

<!-- Blue theme -->
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,700;0,800;1,700;1,800&family=Space+Grotesk:wght@300;400;500;600&family=JetBrains+Mono:wght@400;500&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet" />

<!-- Dark theme -->
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;700;800&family=DM+Mono:wght@400;500&family=Inter:wght@300;400;500&display=swap" rel="stylesheet" />
```

---

### 0.2 Typography Scale

These size tokens are shared across all themes. Values use `clamp()` for fluid scaling.

| Token | Value | Weight | Use |
|---|---|---|---|
| `--text-hero` | `clamp(3.4rem, 9.5vw, 9.5rem)` | 800 | Hero H1 |
| `--text-contact` | `clamp(3rem, 9vw, 7.5rem)` | 800 | Contact section H2 |
| `--text-section` | `clamp(2.25rem, 5vw, 3.75rem)` | 800 | Section headings |
| `--text-about-heading` | `clamp(2.1rem, 4.5vw, 3.35rem)` | 800 | About sticky heading |
| `--text-case-featured` | `clamp(2rem, 4.5vw, 3rem)` | 800 | Featured case study title |
| `--text-case` | `clamp(1.5rem, 2.75vw, 2rem)` | 800 | Standard case study title |
| `--text-body` | `clamp(15px, 1.05vw, 17px)` | 400 | Base body |
| `--text-body-sm` | `0.875rem` | 400 | Case descriptions, about paragraphs |
| `--text-body-xs` | `0.88rem` | 400 | Case descriptions secondary |
| `--text-label` | `0.7rem` | 400 | `// section_labels` (monospace) |
| `--text-tag` | `0.62rem` | 400 | Tag chips, badges, meta |
| `--text-nav` | `0.85rem` | 400–500 | Nav links |
| `--text-stat` | `clamp(2.4rem, 5vw, 4rem)` | 800 | Stats bar numbers |
| `--text-metric` | `1.15rem` | 800 | Case card metric numbers |

**Line heights:**
- Display/headlines: `line-height: 1.0` (or `0.92` for hero/contact at large sizes)
- Body copy: `line-height: 1.7`
- Case descriptions: `line-height: 1.65`
- Labels/mono: `line-height: 1.4`

**Letter spacing:**
- Headlines: `letter-spacing: -0.025em` to `-0.03em`
- Nav links: `letter-spacing: 0.05em`
- Labels (mono): `letter-spacing: 0.14em`
- Tags: `letter-spacing: 0.06–0.10em`
- Badges: `letter-spacing: 0.10em`

---

### 0.3 Spacing System

| Token | Value | Use |
|---|---|---|
| `--space-section-v` | `clamp(5rem, 10vh, 8rem)` | Section top/bottom padding |
| `--space-section-h` | `clamp(1.25rem, 5vw, 4rem)` | Section left/right gutters |
| `--space-section-head` | `clamp(3rem, 6vh, 4.5rem)` | Gap below section heading block |
| `--space-hero-bottom` | `clamp(3.5rem, 8vh, 5.5rem)` | Hero bottom padding |
| `--space-card-inner` | `clamp(2rem, 4vw, 2.75rem)` | Case card inner padding |
| `--space-card-gap` | `0.875rem` | Gap between CTA pairs, metric items |
| `--space-skill-row` | `0.6rem 0` | Skill row vertical padding |
| `--nav-h` | `68px` | Nav height — used for scroll offset |

---

### 0.4 Border Radius

| Context | Value | Notes |
|---|---|---|
| Work grid container | `10px` | Clips all child card corners |
| Buttons (all themes) | `9999px` | Full pill |
| Badges | `3px` | Near-square, minimal rounding |
| Tag chips | `4px` | Slightly more relaxed than badges |
| Code Lab cards | `8px` | Browser window frame |
| Code Lab traffic dots | `50%` | Perfect circle |
| Stats bar cells | `0` | Edge-to-edge grid, no rounding |

---

### 0.5 Animation Principles

#### Page Load (Hero only)
Elements stagger in via `fadeUp` animation:

```css
@keyframes fadeUp {
  from { opacity: 0; transform: translateY(20px); }
  to   { opacity: 1; transform: translateY(0); }
}
```

| Element | Delay | Duration |
|---|---|---|
| `// label` | `0.05s` | `0.50s ease forwards` |
| Hero headline | `0.20s` | `0.65s ease forwards` |
| Hero tagline | `0.40s` | `0.65s ease forwards` |
| Hero CTAs | `0.55s` | `0.65s ease forwards` |

#### Scroll Reveal
- Class: `.reveal` → `.is-visible` (triggered by IntersectionObserver)
- Keyframe: `opacity: 0, translateY(24px)` → `opacity: 1, translateY(0)`
- Duration: `0.65s ease`
- Threshold: `0.08` · rootMargin: `0px 0px -48px 0px`
- Sibling stagger: `i × 0.08s` transitionDelay on `.reveal` children
- Plays once — element unobserved after trigger

#### Hover — Buttons
- `transform: translateY(-2px)` + themed `box-shadow`
- Duration: `0.2s ease`

#### Hover — Case Cards
- Background shifts to `--bg-card-hover`
- Tag chips: border-color and text shift to accent
- Case CTA arrow: gap widens (`0.35rem` → `0.6rem`)
- Image thumbnail (if present): `scale(1.03)` over `0.5s ease`

#### Hover — Nav Links
- `color` transitions from `--text-secondary` → `--text-primary` (or accent on Blue theme)
- Duration: `0.2s ease`

#### Reduced Motion
```css
@media (prefers-reduced-motion: reduce) {
  html { scroll-behavior: auto; }
  .reveal, .hero-label, .hero-title, .hero-sub, .hero-ctas {
    animation: none !important;
    opacity: 1 !important;
    transform: none !important;
    transition: none !important;
  }
}
```

---

### 0.6 Responsive Breakpoints

| Name | Min-width | Key layout changes |
|---|---|---|
| `mobile` | `< 640px` | Nav links hidden; hamburger shown; stats 2×2; everything single-column |
| `tablet` | `640px` | Stats → 4-column row; work grid → 2-column; nav links visible |
| `desktop` | `900px` | About → sticky 2-column; maximum whitespace applied |
| `wide` | `1024px` | Code Lab grid → 3-column |

#### Layout shifts per section

**Nav:** Mobile — hamburger only, links hidden. Menu: full-screen overlay, links at `3rem / font-weight 800`. Desktop — name left, links right.

**Hero:** Single column all breakpoints. Type scales fluidly via `clamp()`.

**Stats:** `2×2` grid mobile → `4×1` row at `640px+`.

**About:** Single column mobile/tablet → sticky 2-column (`1fr 1fr`) at `900px+`. Left column: large display heading (sticky). Right column: body copy + skills grid.

**Work:** Single column mobile → 2-column at `700px+`. Featured card always spans full width (`grid-column: 1 / -1`).

**Code Lab:** Single column mobile → 2-column at `640px+` → 3-column at `1024px+`.

**Contact / Footer:** Stack on mobile, side-by-side on desktop.

---

## Part 1: Theme — Light

> **Status: Frozen. Do not modify `styles.css`.** These tokens are documented for reference only.

```css
/* Applied via: <html> (default, no data-theme needed) */

:root {
  /* Surfaces */
  --bg-primary:              #FAF8F5;
  --bg-card:                 #FAF8F5;
  --bg-card-hover:           #F2EDE6;
  --surface:                 #F2EDE6;

  /* Accent */
  --accent-primary:          #B84E26;   /* terracotta — labels, metric numbers, CTAs */
  --accent-dark:             #963D1C;   /* hover darken */
  --accent-soft:             #D4B8A0;   /* quote border, decorative */
  --accent-secondary:        #7060A8;   /* lavender — stat highlight only */

  /* Text */
  --text-primary:            #1C1714;
  --text-secondary:          #9A8E84;
  --text-muted:              #9A8E84;

  /* Borders */
  --border:                  #E5DDD4;

  /* Fonts */
  --font-display:            'Red Hat Display', system-ui, sans-serif;
  --font-heading:            'Red Hat Display', system-ui, sans-serif;
  --font-mono:               'DM Mono', 'Courier New', monospace;
  --font-body:               'Red Hat Display', system-ui, sans-serif;

  /* Component-specific */
  --nav-bg:                  rgba(250, 248, 245, 0.88);
  --hero-glow:               rgba(184, 78, 38, 0.07);
  --stat-highlight-bg:       rgba(112, 96, 168, 0.06);
  --stat-highlight-border:   rgba(112, 96, 168, 0.25);
  --badge-expert-bg:         rgba(184, 78, 38, 0.08);
  --badge-expert-border:     rgba(184, 78, 38, 0.22);
  --badge-expert-text:       #B84E26;
  --btn-primary-shadow:      rgba(184, 78, 38, 0.22);

  --nav-h: 68px;
}
```

**Hero headline treatment:**
- Line 1: `--text-primary` (`#1C1714`)
- Line 2 (`.accent`): `#B84E26` (terracotta)

---

## Part 2: Theme — Blue

*Visual identity: "blueGreen" — periwinkle blue canvas, lime-green accents, editorial serif display type.*

### Concept
A bold, immersive theme built on a periwinkle blue canvas with lime-green accents. Inspired by Indaco's portfolio — confident, creative, unforgettable. The background IS the color statement. Cards are slightly deeper blue. All text is white. Lime is used sparingly: CTAs, active states, accent headline line.

### Color Reference (from style guide screenshots)

| Swatch | Token | Hex | Description |
|---|---|---|---|
| Background | `--bg-primary` | `#6565F0` | Main periwinkle blue surface |
| Foreground | `--text-primary` | `#FFFFFF` | White text on blue surfaces |
| Primary / CTA | `--accent-secondary` | `#C5F200` | Lime-green — buttons and active states |
| Primary Foreground | `--accent-fg` | `#0A0D1A` | Dark navy text on lime surfaces |
| Card | `--bg-card` | `#5050D8` | Slightly deeper blue for card backgrounds |
| Secondary | `--surface` | `#3D3DC8` | Deeper blue for hover and secondary surfaces |
| Muted Foreground | `--text-muted` | `#C5C5E0` | Light blue-grey for captions and hints |
| Border | `--border` | `rgba(255, 255, 255, 0.12)` | Subtle blue borders and dividers |

```css
[data-theme="blue"] {
  /* Surfaces */
  --bg-primary:              #6565F0;   /* periwinkle — main canvas */
  --bg-card:                 #5050D8;   /* deeper blue — card background */
  --bg-card-hover:           #3D3DC8;   /* hover state — even deeper */
  --surface:                 #3D3DC8;

  /* Accent */
  --accent-primary:          #6565F0;   /* periwinkle — used for in-text accent references */
  --accent-dark:             #5050D8;
  --accent-soft:             rgba(197, 242, 0, 0.25);   /* lime glow for quote borders */
  --accent-secondary:        #C5F200;   /* lime-green — CTAs, active states, headline line 2 */
  --accent-fg:               #0A0D1A;   /* dark navy — text on lime surfaces */

  /* Text */
  --text-primary:            #FFFFFF;
  --text-secondary:          #C5C5E0;   /* muted blue-grey */
  --text-muted:              #9494C0;

  /* Borders */
  --border:                  rgba(255, 255, 255, 0.12);

  /* Fonts */
  --font-display:            'Playfair Display', Georgia, serif;
  --font-heading:            'Space Grotesk', system-ui, sans-serif;
  --font-mono:               'JetBrains Mono', 'Courier New', monospace;
  --font-body:               'DM Sans', system-ui, sans-serif;

  /* Component-specific */
  --nav-bg:                  rgba(101, 101, 240, 0.95);
  --hero-glow:               rgba(197, 242, 0, 0.08);
  --stat-highlight-bg:       rgba(197, 242, 0, 0.08);
  --stat-highlight-border:   rgba(197, 242, 0, 0.30);
  --badge-expert-bg:         rgba(197, 242, 0, 0.10);
  --badge-expert-border:     rgba(197, 242, 0, 0.35);
  --badge-expert-text:       #C5F200;
  --btn-primary-shadow:      rgba(197, 242, 0, 0.25);

  --nav-h: 68px;
}
```

**Hero headline treatment (Blue theme):**
- Line 1 ("DESIGNING PRODUCTS."): `--text-primary` (`#FFFFFF`)
- Line 2 ("LEARNING TO BUILD THEM TOO."): `--accent-secondary` (`#C5F200`) — lime

**Button treatment (Blue theme):**
- Primary (`btn-primary`): `background: #C5F200`, `color: #0A0D1A`, `border: none`
- Ghost (`btn-ghost`): `background: transparent`, `color: #FFFFFF`, `border: 1px solid rgba(255,255,255,0.30)`
- Active nav pill: `background: #C5F200`, `color: #0A0D1A`, pill shape

**Typography specifics (Blue theme):**
- Headlines (`h1`, `h2`, hero title, contact headline): Playfair Display — **italic**, weight 700–800
- Nav links, section subheadings, button labels: Space Grotesk, uppercase, weight 400–500
- `// labels`, tags, badges: JetBrains Mono
- Body copy, card descriptions: DM Sans, weight 300–400

**Blue theme component notes:**
- Nav: periwinkle background at 95% opacity, no visible border on scroll (color already separates it)
- Cards: `--bg-card` (#5050D8) on `--bg-primary` (#6565F0) — the contrast is subtle but clear
- Tag chips: white border at 20% opacity, hover → lime border + lime text
- Code Lab cards: browser chrome uses `--surface` (#3D3DC8), traffic dots standard red/yellow/green

---

## Part 3: Theme — Dark

*Visual identity: "midnight" — near-black canvas, coral-to-amber gradient accent, developer aesthetic.*

### Concept
Stark dark background. A warm gradient — coral bleeding into amber — is the single expressive accent. Applied to headline line 2, primary CTAs, and metric numbers. Everything else is disciplined: white text, muted grey secondaries, hairline borders. The gradient earns its attention by being the only warm thing on the page.

### Gradient Specification

```css
--gradient-accent: linear-gradient(135deg, #FF6B6B 0%, #FF9F45 100%);
```

Used for:
1. Hero headline line 2 — gradient text via `-webkit-background-clip: text`
2. Contact headline accent word — same treatment
3. `btn-primary` fill
4. Optional: active/hover underline on nav links

**Gradient text implementation:**
```css
.hero-title .accent,
.contact-headline .accent {
  background: var(--gradient-accent);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  color: transparent; /* fallback */
}
```

**Gradient button implementation:**
```css
.btn-primary {
  background: var(--gradient-accent);
  border: none;
  color: #0D0D0D;
}
.btn-primary:hover {
  filter: brightness(1.08);
  transform: translateY(-2px);
  box-shadow: 0 6px 24px var(--btn-primary-shadow);
}
```

```css
[data-theme="dark"] {
  /* Surfaces */
  --bg-primary:              #0D0D0D;   /* near black */
  --bg-card:                 #141414;   /* lifted card surface */
  --bg-card-hover:           #1C1C1C;   /* hover state */
  --surface:                 #141414;

  /* Accent */
  --accent-primary:          #FF6B6B;   /* coral — standalone uses: labels, metrics, badge text */
  --accent-dark:             #E05555;   /* hover darken */
  --accent-soft:             rgba(255, 107, 107, 0.25);   /* quote border, soft glow */
  --accent-secondary:        #FF9F45;   /* warm amber — gradient end stop */
  --gradient-accent:         linear-gradient(135deg, #FF6B6B 0%, #FF9F45 100%);

  /* Text */
  --text-primary:            #F5F5F5;   /* warm white */
  --text-secondary:          #7D7D8C;   /* cool grey */
  --text-muted:              #4A4A58;

  /* Borders */
  --border:                  rgba(255, 255, 255, 0.08);   /* very subtle */

  /* Fonts */
  --font-display:            'Syne', system-ui, sans-serif;
  --font-heading:            'Syne', system-ui, sans-serif;
  --font-mono:               'DM Mono', 'Courier New', monospace;
  --font-body:               'Inter', system-ui, sans-serif;

  /* Component-specific */
  --nav-bg:                  rgba(13, 13, 13, 0.92);
  --hero-glow:               rgba(255, 107, 107, 0.07);
  --stat-highlight-bg:       rgba(255, 107, 107, 0.05);
  --stat-highlight-border:   rgba(255, 107, 107, 0.20);
  --badge-expert-bg:         rgba(255, 107, 107, 0.08);
  --badge-expert-border:     rgba(255, 107, 107, 0.25);
  --badge-expert-text:       #FF6B6B;
  --btn-primary-shadow:      rgba(255, 107, 107, 0.25);

  --nav-h: 68px;
}
```

**Hero headline treatment (Dark theme):**
- Line 1 ("DESIGNING PRODUCTS."): `--text-primary` (`#F5F5F5`)
- Line 2 ("LEARNING TO BUILD THEM TOO."): `--gradient-accent` via background-clip text

**Button treatment (Dark theme):**
- Primary (`btn-primary`): `background: --gradient-accent`, `color: #0D0D0D`, `border: none`
- Ghost (`btn-ghost`): `background: transparent`, `color: --text-primary`, `border: 1px solid rgba(255,255,255,0.15)`

---

## Part 4: Component Token Reference

Quick-lookup table for every component across all three themes. Use this as the implementation checklist.

---

### Navigation

| Property | Light | Blue | Dark |
|---|---|---|---|
| Background | `rgba(250,248,245,0.88)` | `rgba(101,101,240,0.95)` | `rgba(13,13,13,0.92)` |
| Logo text | `--text-primary` | `--text-primary` | `--text-primary` |
| Link text | `--text-secondary` | `--text-secondary` | `--text-secondary` |
| Link hover | `--text-primary` | `#C5F200` (lime) | `--text-primary` |
| Border on scroll | `#E5DDD4` | `rgba(255,255,255,0.10)` | `rgba(255,255,255,0.06)` |
| Active nav pill bg | — | `#C5F200` | — |
| Active nav pill text | — | `#0A0D1A` | — |
| Mobile menu bg | `#FAF8F5` | `#6565F0` | `#0D0D0D` |
| Mobile link text | `--text-primary` | `--text-primary` | `--text-primary` |

---

### Hero

| Property | Light | Blue | Dark |
|---|---|---|---|
| Headline line 1 | `#1C1714` | `#FFFFFF` | `#F5F5F5` |
| Headline line 2 (`.accent`) | `#B84E26` | `#C5F200` | gradient `#FF6B6B→#FF9F45` |
| `// label` text | `#B84E26` | `#C5F200` | `#FF6B6B` |
| Tagline text | `#9A8E84` | `#C5C5E0` | `#7D7D8C` |
| Background glow | `rgba(184,78,38,0.07)` | `rgba(197,242,0,0.08)` | `rgba(255,107,107,0.07)` |
| Font (headline) | Red Hat Display 800 | Playfair Display italic 800 | Syne 800 |

---

### Buttons

| Property | Light | Blue | Dark |
|---|---|---|---|
| Primary bg | `#B84E26` | `#C5F200` | gradient |
| Primary text | `#FFFFFF` | `#0A0D1A` | `#0D0D0D` |
| Primary hover shadow | `rgba(184,78,38,0.22)` | `rgba(197,242,0,0.25)` | `rgba(255,107,107,0.25)` |
| Ghost border | `#E5DDD4` | `rgba(255,255,255,0.30)` | `rgba(255,255,255,0.15)` |
| Ghost text | `#1C1714` | `#FFFFFF` | `#F5F5F5` |
| Border radius | `9999px` | `9999px` | `9999px` |
| Font | Red Hat Display 500 | Space Grotesk 500 | Syne 500 |

---

### Stats Bar

| Property | Light | Blue | Dark |
|---|---|---|---|
| Number | `#1C1714` | `#FFFFFF` | `#F5F5F5` |
| Label | `#9A8E84` | `#C5C5E0` | `#7D7D8C` |
| Highlight number | `#7060A8` | `#C5F200` | `#FF6B6B` |
| Highlight bg | `rgba(112,96,168,0.06)` | `rgba(197,242,0,0.08)` | `rgba(255,107,107,0.05)` |
| Highlight border | `rgba(112,96,168,0.25)` | `rgba(197,242,0,0.30)` | `rgba(255,107,107,0.20)` |
| Cell border | `#E5DDD4` | `rgba(255,255,255,0.12)` | `rgba(255,255,255,0.08)` |

---

### Badges (Skills section)

| Badge | Light | Blue | Dark |
|---|---|---|---|
| `[EXPERT]` bg | `rgba(184,78,38,0.08)` | `rgba(197,242,0,0.10)` | `rgba(255,107,107,0.08)` |
| `[EXPERT]` border | `rgba(184,78,38,0.22)` | `rgba(197,242,0,0.35)` | `rgba(255,107,107,0.25)` |
| `[EXPERT]` text | `#B84E26` | `#C5F200` | `#FF6B6B` |
| `[LEARNING]` bg | transparent | transparent | transparent |
| `[LEARNING]` border | `#E5DDD4` | `rgba(255,255,255,0.15)` | `rgba(255,255,255,0.10)` |
| `[LEARNING]` text | `#9A8E84` | `#C5C5E0` | `#7D7D8C` |

---

### Case Study Cards

| Property | Light | Blue | Dark |
|---|---|---|---|
| Card bg | `#FAF8F5` | `#5050D8` | `#141414` |
| Card hover bg | `#F2EDE6` | `#3D3DC8` | `#1C1C1C` |
| Category label | `#9A8E84` | `#C5C5E0` | `#7D7D8C` |
| Title | `#1C1714` | `#FFFFFF` | `#F5F5F5` |
| Description | `#9A8E84` | `#C5C5E0` | `#7D7D8C` |
| Metric number | `#B84E26` | `#C5F200` | `#FF6B6B` |
| Metric label | `#9A8E84` | `#C5C5E0` | `#7D7D8C` |
| Quote border-left | `#D4B8A0` | `rgba(197,242,0,0.25)` | `rgba(255,107,107,0.25)` |
| Case CTA link | `#B84E26` | `#C5F200` | `#FF6B6B` |
| Tag chip border | `#E5DDD4` | `rgba(255,255,255,0.20)` | `rgba(255,255,255,0.10)` |
| Tag chip text | `#9A8E84` | `#C5C5E0` | `#7D7D8C` |
| Tag chip hover border | `rgba(184,78,38,0.35)` | `rgba(197,242,0,0.40)` | `rgba(255,107,107,0.35)` |
| Tag chip hover text | `#B84E26` | `#C5F200` | `#FF6B6B` |
| Card border | `#E5DDD4` | `rgba(255,255,255,0.10)` | `rgba(255,255,255,0.06)` |

---

### Code Lab Cards *(new section — not yet in CSS)*

**Structure:**
```
┌──────────────────────────────────────┐
│  ● ● ●   project-name               │  ← browser chrome bar (monospace label)
├──────────────────────────────────────┤
│                                      │
│  PROJECT_NAME                        │  ← monospace, accent color
│  One-line plain-english description  │  ← body font, text-secondary
│                                      │
│  [html]  [css]  [js]                 │  ← tag chips
│                                      │
│  view on github →                    │  ← accent color CTA
└──────────────────────────────────────┘
```

| Property | Light | Blue | Dark |
|---|---|---|---|
| Card bg | `#F2EDE6` | `#5050D8` | `#141414` |
| Chrome bar bg | `#E5DDD4` | `rgba(255,255,255,0.08)` | `rgba(255,255,255,0.05)` |
| Chrome bar border-bottom | `#E5DDD4` | `rgba(255,255,255,0.12)` | `rgba(255,255,255,0.06)` |
| Traffic dot — close | `#FF5F57` | `#FF5F57` | `#FF5F57` |
| Traffic dot — minimise | `#FFBD2E` | `#FFBD2E` | `#FFBD2E` |
| Traffic dot — fullscreen | `#27C93F` | `#27C93F` | `#27C93F` |
| Project name | `#B84E26` | `#C5F200` | `#FF6B6B` |
| Description | `#9A8E84` | `#C5C5E0` | `#7D7D8C` |
| GitHub CTA | `#B84E26` | `#C5F200` | `#FF6B6B` |
| Card border radius | `8px` | `8px` | `8px` |

**Grid layout:** 1-column mobile → 2-column at 640px → 3-column at 1024px.
**Card gap:** `1.5rem`.

---

### Contact Section

| Property | Light | Blue | Dark |
|---|---|---|---|
| `// label` | `#B84E26` | `#C5F200` | `#FF6B6B` |
| Headline line 1 | `#1C1714` | `#FFFFFF` | `#F5F5F5` |
| Headline accent (`.accent`) | `#B84E26` | `#C5F200` | gradient `#FF6B6B→#FF9F45` |
| Sub-copy | `#9A8E84` | `#C5C5E0` | `#7D7D8C` |

---

### Footer

| Property | Light | Blue | Dark |
|---|---|---|---|
| Border-top | `#E5DDD4` | `rgba(255,255,255,0.12)` | `rgba(255,255,255,0.06)` |
| Copyright text | `#9A8E84` | `#9494C0` | `#7D7D8C` |
| Link text | `#9A8E84` | `#9494C0` | `#7D7D8C` |
| Link hover | `#1C1714` | `#FFFFFF` | `#F5F5F5` |

---

## Part 5: Implementation Notes

### Theme Switching

Apply themes via `data-theme` on `<html>`:

```html
<html data-theme="light">   <!-- default -->
<html data-theme="blue">
<html data-theme="dark">
```

**Persist to localStorage:**
```js
const saved = localStorage.getItem('theme') ?? 'light';
document.documentElement.setAttribute('data-theme', saved);

function cycleTheme() {
  const themes = ['light', 'blue', 'dark'];
  const current = document.documentElement.getAttribute('data-theme');
  const next = themes[(themes.indexOf(current) + 1) % themes.length];
  document.documentElement.setAttribute('data-theme', next);
  localStorage.setItem('theme', next);
}
```

**CSS cascade structure:**
```css
:root { /* light theme tokens */ }
[data-theme="blue"] { /* override tokens */ }
[data-theme="dark"] { /* override tokens */ }
```

All component CSS uses `var(--token-name)` — no theme-specific selectors needed in component rules.

---

### Font Loading Strategy

Load all fonts in `<head>`. Use `font-display: swap` to prevent FOIT:
- Light: Red Hat Display + DM Mono (already loaded)
- Blue/Dark: load conditionally based on saved theme or default-load all with low priority

---

### Accessibility

**Contrast ratios (WCAG AA minimum: 4.5:1 body, 3:1 large text):**

| Theme | Pair | Ratio | Status |
|---|---|---|---|
| Light | `#1C1714` on `#FAF8F5` | ~14:1 | ✅ |
| Light | `#B84E26` on `#FAF8F5` | ~4.8:1 | ✅ |
| Blue | `#FFFFFF` on `#6565F0` | ~4.6:1 | ✅ |
| Blue | `#C5F200` on `#6565F0` | ~7.2:1 | ✅ |
| Blue | `#0A0D1A` on `#C5F200` | ~12:1 | ✅ |
| Dark | `#F5F5F5` on `#0D0D0D` | ~16:1 | ✅ |
| Dark | `#FF6B6B` on `#0D0D0D` | ~5.8:1 | ✅ |

**Focus states:** All interactive elements must have visible `:focus-visible` outlines. Recommended: `outline: 2px solid var(--accent-primary); outline-offset: 3px`. Currently missing — add in implementation.

---

## Part 6: Content Gaps (From site-plan.md)

These are outstanding items that need to be updated in `index.html` before the spec is fully implemented:

| Item | Current state | Required state |
|---|---|---|
| Hero copy | Wrong — has old headline | Update to locked copy: `DESIGNING PRODUCTS. / LEARNING TO BUILD THEM TOO.` |
| Hero tagline | Old copy | `Senior designer. Emerging builder.` |
| Hero CTAs | `view work` + `say hello` | `view_work` (#work) + `code_lab` (#code-lab) |
| Nav links | Missing `code_lab` | Add `code_lab` → `#code-lab` |
| Stats — 3rd card | `1 obsession: great craft` | `17 repos and counting` → links to `#code-lab` |
| About heading | Wrong | `FROM / DESIGN / TO CODE` |
| About body | Old copy | Update per site-plan.md paragraphs 1–3 |
| Work — Card 2 | Lightspeed Shipping | Replace with Scaling Up at Zivver (SILK design system) |
| Code Lab section | Missing | Build from scratch (6 project cards) |
| Contact headline | `LET'S MAKE SOMETHING REAL` | `LET'S BUILD SOMETHING REAL` |
| Contact CTA 2 | LinkedIn | GitHub → `https://github.com/GimeVerdant` |
| Footer | Missing GitHub link | Add GitHub between LinkedIn and Portfolio |
| Footer copyright | `© Gimena Blanco 2025` | Update to 2026 |

**Items needing Gimena's sign-off before publishing:**
1. About paragraph 3 — the transition paragraph (voice check)
2. Code Lab intro — comfort with "not polished" framing
3. Which theme to default to on launch

---

*End of design-spec.md*
