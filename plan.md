# Plan: Gimena Blanco — Personal Website

_Architecture, copy, and design decisions before writing a line of code._

---

## Design Direction

### Aesthetic
Dark editorial. Art + logic duality. Not a dev portfolio, not a corporate deck — a designer who lives at the intersection. Inspired by the Alex Chen reference: near-black background, warm coral accent, lavender highlight, DM Mono section markers in `// CODE_STYLE` format.

### What makes it Gimena's (not generic)
- Warm coral (`#E8633A`) instead of cold blue — signals energy and art
- DM Mono section labels feel developer-curious without being a dev portfolio
- The "FEELING LIKE A FRAUD" headline is honest — disarms the corporate persona
- Stats include "1 obsession: great craft" — personality in data
- Copy is written in first person, present tense, like a very talented friend explaining their job

### Reference Takeaways
- **cemento.co.uk**: Editorial confidence, negative space as a design element, declarative copy
- **kaveenk.com**: Dark bg, monospaced labels, grid stat cards, skill bars with level labels
- **Alex Chen screenshot**: `//` section markers, large grotesque headlines, one highlighted stat card in lavender

---

## Color System

```css
:root {
  --bg: #111111;
  --surface: #1c1c1c;
  --border: #2e2e2e;
  --text-primary: #f0ede8;      /* warm white */
  --text-secondary: #8a8a8a;
  --accent: #E8633A;             /* warm coral */
  --accent-soft: #D4B8A0;        /* warm sand */
  --highlight: #C2B4E2;          /* soft lavender */
}
```

---

## Typography

| Usage | Font | Weight |
|-------|------|--------|
| Headlines | Syne | 800 |
| Body | DM Sans | 300–500 |
| Section markers / labels / tags | DM Mono | 400–500 |

All loaded from Google Fonts. No external JS dependencies.

---

## Site Sections

### 1. `<nav>` — Fixed Top
- Logo: "Gimena Blanco" in Syne 700, small, left-aligned
- Links: `work · about · contact` in DM Sans, right-aligned
- Background: `rgba(17,17,17,0.88)` + `backdrop-filter: blur(16px)`
- Mobile: hamburger toggle, links in overlay
- Scroll effect: border-bottom fades in after 50px scroll

---

### 2. Hero — Full Viewport Height
```
// PRODUCT_DESIGNER

DESIGNING WITH
HEART AND LOGIC.

10 years crafting products that solve real problems —
for people who actually have to use them.

[view work]  [say hello]
```
- Content aligned to bottom-left (magazine cover feel)
- Headline: Syne 800, `clamp(3.5rem, 9vw, 9rem)`, line-height 0.95
- "HEART" or "LOGIC" in `var(--accent)` for visual punch
- Subtle radial gradient blob behind headline (coral at 4% opacity)
- Staggered fadeUp animation on load (0.1s, 0.25s, 0.45s, 0.6s delays)
- Scroll indicator at bottom (small animated arrow)

---

### 3. Scrolling Ticker (between Hero and Stats)
```
PRODUCT DESIGN · UX STRATEGY · DESIGN SYSTEMS · SERVICE DESIGN · ACCESSIBILITY · FINTECH · SAAS · ECOMMERCE ·
```
- CSS `@keyframes` auto-scroll, duplicate text for seamless loop
- `aria-hidden="true"` — decorative only
- `prefers-reduced-motion: reduce` → animation paused

---

### 4. Stats Bar — 4 Cards in a Row
| Card | Number | Label |
|------|--------|-------|
| 1 | 10+ | years of experience |
| 2 | 5+ | products shipped _(highlighted in lavender)_ |
| 3 | 4+ | companies shaped |
| 4 | 1 | obsession: great craft |

- Minimal border grid: `1px solid var(--border)` between cards
- Numbers: Syne 800, `clamp(2.5rem, 5vw, 4rem)`
- Highlighted card: `background: rgba(194,180,226,0.08)`, `border-color: var(--highlight)`, number in `var(--highlight)`
- Mobile: 2×2 grid

---

### 5. About Section
```
// ABOUT_ME

[LEFT — sticky on desktop]          [RIGHT — scrolls]
FROM FEELING                        Paragraph 1: Systems thinker / artist at heart / 10 years
LIKE A FRAUD                        Paragraph 2: Lightspeed / Zivver / Aegon — industries change, job stays same
TO SHIPPING                         Paragraph 3: "access first, ease second, aesthetics third" — that third part
THINGS                              ...
PEOPLE LOVE.
                                    // SKILLS
                                    Product Design          [EXPERT]
                                    Design Systems          [EXPERT]
                                    UX Research & Strategy  [EXPERT]
                                    Service Design          [EXPERT]
                                    Accessibility           [EXPERT]
                                    Frontend (HTML & CSS)   [LEARNING]
                                    Motion Design           [LEARNING]
```

- Left column sticky on desktop (`position: sticky; top: nav-height + 2rem`)
- Skill badges: `EXPERT` in coral-tinted pill, `LEARNING` in border-only ghost pill
- DM Mono for badge text

---

### 6. Selected Work — Case Study Cards
```
// SELECTED_WORK
SELECTED WORK

[Full-width card: Lightspeed Shipping]
  eCommerce · SaaS · Lightspeed
  Lightspeed Shipping
  An omnichannel shipping platform for eCommerce merchants — built to make
  fulfillment fast, cost-effective, and actually bearable.
  [Product Design] [UX Research] [Prototyping] [eCommerce]

[Half card: SILK Design System]      [Half card: Aegon Risk Assessment]
  Design Systems · Zivver              Fintech · Aegon
  SILK Design System                   Aegon Risk Assessment
  Led a design system overhaul         An award-winning pension risk calculator
  that reduced palette change time     that made one of the most dreaded
  from 6 hours to 2 minutes.           financial decisions feel almost... okay.
  [Design Systems] [Strategy]          [UX Research] [Fintech] [Service Design]
  [Accessibility]                      [Award-Winning]
```

- Grid: first card full-width, two below in 2-column grid
- Card background: `var(--bg)`, hover → `var(--surface)`
- Border: `1.5px solid var(--border)` as grid lines between cards
- On hover: tags animate to coral accent color
- Transition: `background 0.25s ease`, `transform: translateY(-2px)`
- Category label in DM Mono above title

---

### 7. Contact / CTA
```
// GET_IN_TOUCH

LET'S MAKE
SOMETHING REAL.

No pitch decks required. Just good work and honest conversation.

[say hello]  [linkedin]
```
- "SOMETHING" or "REAL." in `var(--accent)`
- Sub-headline: short, direct, no filler
- `mailto:hello@gimenablanco.com` for primary CTA
- LinkedIn link opens in new tab

---

### 8. Footer
```
© Gimena Blanco 2025          LinkedIn · Portfolio · Email
```
- `border-top: 1px solid var(--border)`
- Footer name in DM Mono, muted
- Social links in DM Sans, muted → hover to primary

---

## Animation Strategy

| Element | Animation | Trigger |
|---------|-----------|---------|
| Hero content | `fadeUp` keyframes, staggered | Page load |
| All other sections | `opacity 0 → 1`, `translateY 28px → 0` | IntersectionObserver |
| Ticker | CSS scroll loop | Always |
| Nav bg | Border fade in | `scroll > 50px` |
| Cards | Hover lift (`translateY -4px`) | CSS `:hover` |

**Reduced motion:** All `@keyframes` and transitions wrapped in `prefers-reduced-motion: reduce` override — elements appear immediately, no motion.

---

## Copy Principles

- Short sentences. Lots of white space.
- First person. Present tense.
- No "passionate about", "leveraging", "results-driven"
- Honesty is a feature — "I still get that buzz" / "almost... okay. Almost."
- Let numbers speak where possible
- The voice: a talented friend who's done this for 10 years and can't be bothered pretending otherwise

---

## Technical Requirements

- Single `index.html` file with embedded CSS + minimal vanilla JS
- Google Fonts via `@import` — Syne, DM Sans, DM Mono
- Semantic HTML: `<nav>`, `<main>`, `<section>`, `<article>`, `<footer>`
- Heading hierarchy: `h1` (hero), `h2` (section titles), `h3` (card titles)
- `alt` text on all images (no images here, but placeholders noted)
- ARIA labels on nav, sections
- `rel="noopener noreferrer"` on all external links
- Mobile-first CSS, breakpoints at 640px and 900px
- Grain texture overlay via SVG `feTurbulence` filter in pseudo-element
- No external dependencies except Google Fonts

---

## Output

```
personal-website/
├── research.md     ← done
├── plan.md         ← this file
└── index.html      ← next
```
