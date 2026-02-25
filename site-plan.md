# Site Plan: Gimena Blanco — Personal Landing Page
*Based on research.md · February 2026*

---

## Core Narrative

The page has one job: communicate that Gimena is a highly experienced senior product designer who is now actively learning to build what she designs. Not a junior developer. Not an ex-designer. A designer who closed the gap between herself and the medium.

Every section should serve one of these two truths:
- **Credibility:** 10 years, real metrics, real companies, real impact.
- **Momentum:** She is learning in public, right now, and showing her work.

The tone is **conversational but credible** — human enough to feel approachable, specific enough to feel earned. No corporate speak. No "passionate about creating impactful user-centric solutions." Plain sentences. Dry wit where it fits. Honest about being mid-journey on the dev side.

---

## Tone Reference Card

| DO | DON'T |
|---|---|
| "I know what good looks like" | "I'm passionate about UX" |
| "now I'm learning to code it myself" | "transitioning into development" |
| "80% of users adopted it in 6 months" | "delivered impactful results" |
| "the unglamorous details" | "end-to-end design thinking" |
| Lowercase CTAs: `say_hello`, `view_work` | UPPERCASE BUTTON TEXT |
| Short sentence. Then a longer one that earns it. | Long sentences that list everything at once. |

---

## Locked Copy (Use Exactly As Written)

These are decided — do not paraphrase or rewrite:

```
Hero label:     // product_designer
Hero headline:  DESIGNING PRODUCTS.
                LEARNING TO BUILD THEM TOO.
Hero tagline:   Senior designer. Emerging builder.
About opener:   "I know what good looks like —
                 now I'm learning to code it myself."
```

---

---

## Section 1 — NAV

**Layout:** Name left · Links right · Sticky on scroll

**Left:**
```
Gimena Blanco
```

**Right links:**
```
work    about    code_lab   contact

```
- toggle button for the three themes - light - blue and dark
the current css applies to light theme 
**Notes:**
- All lowercase, consistent with existing site voice
- `code_lab` is a named anchor to the Code Lab section — should feel like its own destination, not an afterthought
- On mobile: hamburger → full-screen overlay with same 4 links
- No logo/icon needed — name is the brand
- On scroll: subtle background fill or border-bottom to separate from page content

**Links:**
| Label | Target |
|---|---|
| `work` | `#work` |
| `about` | `#about` |
| `code_lab` | `#code-lab` |
| `contact` | `#contact` |

---

## Section 2 — HERO

**Layout:** Single column, vertically centred, generous whitespace

```
// product_designer                    ← small monospace label, muted

DESIGNING PRODUCTS.                    ← large, bold, all caps, split across lines
LEARNING TO BUILD THEM TOO.

Senior designer. Emerging builder.    ← smaller, regular weight, directly below headline

[view_work]   [code_lab]              ← two CTAs side by side
```

**CTA details:**

| Button | Style | Target |
|---|---|---|
| `view_work` | Primary (filled) | `#work` |
| `code_lab` | Ghost (outlined) | `#code-lab` |

**Notes:**
- The label `// product_designer` works as a code comment — nods to the dev learning arc without overstating it. Keep it subtle and small.
- Headline rhythm matters: "DESIGNING PRODUCTS." lands as the statement of existing identity. "LEARNING TO BUILD THEM TOO." lands as the pivot. The line break is the pause between them.
- Tagline "Senior designer. Emerging builder." is deliberately asymmetric — one confident noun, one honest one. Do not swap the order.
- No hero image or illustration needed. The typography IS the design statement.
- Optional: subtle animated cursor or blinking element after the label to lean into the developer aesthetic — only if it doesn't slow the page.

**Status:** ✅ All copy real and confirmed

---

## Section 3 — STATS BAR

**Layout:** 3 cards in a horizontal row, full width, dark or accent background to break page rhythm

**Recommended stats:**

| Stat | Label | Source | Real? |
|---|---|---|---|
| `10+` | years of experience | Research, portfolio | ✅ Real |
| `5+` | products shipped | Existing personal site | ✅ Real |
| `17` | repos and counting | GitHub (GimeVerdant) | ✅ Real |

**Alternative option for stat 3** (if GitHub repo count feels too "learning-in-progress" for a stats bar):

| Stat | Label | Source | Real? |
|---|---|---|---|
| `50%` | fewer support tickets — Label Editor | Research | ✅ Real |

**Recommendation:** Use the GitHub `17 repos` stat. It directly mirrors the narrative ("learning to build") and is an honest, specific number. A vague "4+ companies" is less interesting than a live counter that shows active work.

**Notes:**
- Stats bar should feel lightweight and factual — not a victory lap. Short labels, big numbers, clean grid.
- Consider making the `17 repos` stat link directly to `#code-lab` as a subtle affordance.

**Status:** ✅ All real numbers

---

## Section 4 — ABOUT

**Layout:** Two-column sticky layout. Left: large heading. Right: copy + skills grid.

---

### Left column — large display heading

```
FROM
DESIGN
TO CODE
```

Or single-line variant:
```
DESIGN.
THEN CODE.
```

**Notes:** This heading should be large, stacked, and typographically confident. It's the visual anchor. It does not need to be literally true yet — it's a direction of travel, not a completed state.

---

### Right column — body copy

**Paragraph 1 — The hook:**
```
<p class="reveal">
  My approach draws on user research, data, and creative problem-solving —
  not as a formula, but as a way of making sure the solution that ships
  is the one that <strong>actually needed to exist.</strong>
</p>

**Paragraph 2 — The experience:**
```
I started as a visual designer, but the surface was never enough.
              I moved into UX research, information architecture, and service
              design — following the work wherever it led to find the
              <strong>right problem before the right solution.</strong> More
              recently, that curiosity has extended into frontend code.
            </p>
            <p class="reveal">
              I've worked across fintech, SaaS, and eCommerce. The industries
              shift; the work stays consistent: understand what people genuinely
              need, then design something that serves them
              <strong>and</strong> makes sense for the business.
```
*(Sourced from existing personal-website/index.html — confirmed real)*

**Paragraph 3 — The transition (new, honest, on-narrative):**
```
I started as a printmaker. Then I studied web development. Then I
spent a decade designing interfaces — and somewhere in there I
realised I wanted to build them too. So now I am. Slowly, publicly,
one repo at a time.
```

**Notes on paragraph 3:**
- This is the most important paragraph on the page for the "learning to build" narrative. It surfaces the education backstory (printmaker → multimedia programming → design → front-end) without making it sound like a crisis or a career change.
- "Slowly, publicly, one repo at a time." — honest, self-aware, not defensive. Matches her voice exactly.
- **Do not say "transitioning into development."** That sounds like leaving design. She isn't leaving design. She's expanding into building.

**Paragraph 3 — Shorter variant (if space is tight):**
```
I started as a printmaker, then studied web development, then spent
a decade designing interfaces. Now I'm learning to build them.
One repo at a time.
```

---

### Skills grid

**Layout:** Stacked rows, skill name left, badge right

```
// SKILLS

Product Design              [ EXPERT ]
Design Systems              [ EXPERT ]
UX Research & Strategy      [ EXPERT ]
Service Design              [ EXPERT ]
Accessibility               [ EXPERT ]
Figma & Prototyping         [ EXPERT ]
──────────────────────────────────────
HTML & CSS                  [ LEARNING ]
JavaScript                  [ LEARNING ]
Motion Design               [ LEARNING ]
```

**Notes:**
- The `LEARNING` badge should not look apologetic — style it as a positive state, maybe a different color (accent) rather than a muted/grey one
- The horizontal rule between EXPERT and LEARNING rows is a clean way to separate the two tiers without a heading
- Keep `// SKILLS` in monospace as a section micro-label, consistent with `// product_designer`

**Status:** ✅ All real, sourced from existing site + GitHub evidence

---

## Section 5 — CASE STUDIES

**Layout:** Vertical stack of 3 cards. Each card: category label · title · description · tags · optional metric callout. One small image

**Selected works (as instructed):** Farm Timeline · Label Editor · Scaling Up at Zivver

---

### Card 1 — Farm Timeline

```
AgriTech · SaaS · Lead UX Designer

FARM TIMELINE

Farmers were tracking ration changes and health events on paper.
We built them a digital timeline that connected those events to
real farm metrics — so they could finally see what was working
and what wasn't.

15+ user interviews. Field studies on US farms. Two rounds of
prototype testing with real farm data before a single line shipped.

[ UX Research ]  [ Data Visualisation ]  [ AgriTech ]  [ Mobile ]
```

**Metric callout (pull out visually):**
```
80% adoption in 6 months
30% lift in free-to-paid conversion
2–3 hrs/week saved per user
```

**User quote (optional — use one):**
```
"I can't overstate the value of the Farm Timeline, it has been huge."
— Wyatt, Feed Advisor
```

**CTA:** `read case study →` → [gimenablanco.com/farm-timeline](https://www.gimenablanco.com/farm-timeline) *(external, real)*

**Notes:**
- Lead with the human problem ("tracking on paper"), not the product feature
- The metric callout is the strongest on the page — give it visual weight, maybe a highlighted block or pull-quote treatment
- The Wyatt quote is the best of the three — specific job title, specific language

---

### Card 2 — Label Editor

```
eCommerce · Retail POS · Product Designer

LABEL EDITOR

Merchants were editing product labels through raw code. Half of
all support tickets were about label layouts. We built them a
visual editor — live preview, drag-and-drop, no code required.

Support tickets about label layouts dropped by over 50%.

[ Product Design ]  [ Figma ]  [ eCommerce ]  [ Retail ]
```

**Stakeholder quote (optional):**
```
"Questions about label support now have a simple answer
instead of lengthy explanations."
— Hudson, Escalation Team, Lightspeed
```

**CTA:** `read case study →` → [gimenablanco.com/label-editor](https://www.gimenablanco.com/label-editor) *(external, real)*

**Notes:**
- "Half of all support tickets" is a striking framing — lead with it or use it in the metric callout
- The Hudson quote is unusual (internal escalation team, not a user) and therefore more credible for a business audience. Use it if space allows.
- Shorter card than Farm Timeline — that's fine. Not every case study needs equal weight.

---

### Card 3 — Scaling Up at Zivver

```
Design Systems · SaaS · Senior UX Designer

SILK DESIGN SYSTEM

Zivver had no shared design language, no user research budget,
and no process for any of it. I came in to fix that — not just
the components, but the culture around them.

We named the design system SILK. Before it existed, changing
one colour took 6 hours and touched 600+ lines of code.
After: 2 minutes. One source of truth.

[ Design Systems ]  [ Accessibility ]  [ Strategy ]  [ Scale-up ]
```

**Metric callout:**
```
600+ code references → 1 source of truth
Colour changes: 6 hours → 2 minutes
```

**CTA:** `read case study →` → [gimenablanco.com/scaling-up-at-zivver](https://www.gimenablanco.com/scaling-up-at-zivver) *(external, real)*

**Notes:**
- The SILK naming anecdote (hummingbirds weave nests from silk — one of the strongest natural threads) is a warm human detail. Optional to include in card copy, but worth adding if there's a tooltip or expanded state.
- Lead with the org problem ("no shared design language, no budget"), not the deliverable — the deliverable lands harder when the problem is established first.
- "Not just the components, but the culture around them" — this is the line that differentiates her from a component-builder. It should be in the card.

---

### Section-level notes:
- Section heading: `// SELECTED_WORK` (monospace label) + `SELECTED WORK` (large display)
- Cards should have a clear visual hierarchy: category label (small, muted) → title (large) → body → tags → metric → CTA
- Metrics should be the most visually prominent element after the title — they're the proof
- All 3 case study links go to existing gimenablanco.com pages — ✅ all real

---

## Section 6 — CODE LAB

**Layout:** Section intro + grid of project cards. Each card: name · description · tags · GitHub link.

**Section heading:**
```
// CODE_LAB
```

**Section intro copy:**
```
This is where the learning happens in public. Every project here
is a Frontend Mentor challenge or a self-directed build — HTML,
CSS, a bit of JavaScript. Not production. Not polished.
Just a designer figuring out how the thing actually works.
```

**Notes on intro:**
- "Not production. Not polished." — sets expectations honestly and disarms any "but it's not impressive enough" anxiety
- "a designer figuring out how the thing actually works" — this is the narrative. Don't bury it in a tooltip.

---

### Project cards (real repos from GitHub — GimeVerdant)

| Project | Description | Tags | Link |
|---|---|---|---|
| `meet-landing` | Landing page layout challenge | HTML · CSS | github.com/GimeVerdant/meet-landing |
| `newsletter-signup` | Sign-up form with validation states | HTML · CSS | github.com/GimeVerdant/newsletter_signup |
| `article-preview` | Interactive component with JS share toggle | HTML · CSS · JS | github.com/GimeVerdant/article-preview-component |
| `blog-preview-card` | Card component — typography and spacing | HTML · CSS | github.com/GimeVerdant/blog_preview_card |
| `testimonials` | Testimonial grid layout | HTML · CSS | github.com/GimeVerdant/testimonials |
| `product-preview-card` | Responsive product display card | HTML · CSS | github.com/GimeVerdant/product-preview-card |

**Which to feature (recommend 4–6):** Prioritise by recency and complexity:
1. `meet-landing` — most recent, Feb 23 2026
2. `newsletter-signup` — recognisable UI pattern
3. `article-preview` — only one with JavaScript; shows progression
4. `testimonials` — grid layout, shows layout thinking
5. `blog-preview-card` — clean, polished looking

**Card copy template:**
```
[PROJECT NAME]                ← monospace or code-style name
[One-line description]        ← plain english, what it does
[tag] [tag] [tag]
[ view on github → ]
```

**Status:** ✅ All real repos, all public on GitHub

---

### Optional CTA at bottom of Code Lab:
```
See everything I'm building →     [github.com/GimeVerdant]
```

---

## Section 7 — CONTACT / CTA

**Layout:** Full-width section, large centred text, two buttons

**Section label:**
```
// GET_IN_TOUCH
```

**Headline:**
```
LET'S BUILD
SOMETHING
REAL.
```

*(Variant from existing site — keep it. It's strong.)*

**Or, leaning into the dual identity:**
```
LET'S MAKE
SOMETHING
TOGETHER.
```

**Recommendation:** Keep `LET'S BUILD SOMETHING REAL.` from the existing site. "Build" now does double duty — it means both product work and literally writing code.

**Supporting copy:**
```
No pitch decks required.
Just good work and honest conversation.
```
*(From existing site — confirmed as her voice. Keep it exactly.)*

**CTAs:**

| Button | Label | Style | Target |
|---|---|---|---|
| Primary | `say_hello` | Filled | `mailto:hello@gimenablanco.com` |
| Ghost | `github` | Outlined | `https://github.com/GimeVerdant` |

**Notes:**
- Two CTAs here serve two different audiences: someone wanting to hire/collaborate (email) and someone wanting to see the dev work (GitHub)
- LinkedIn is not a CTA here — it's in the footer. The contact section should feel direct and personal, not networky.
- `say_hello` is lowercase intentionally — matches existing site voice

**Status:** ✅ All real links

---

## Section 8 — FOOTER

**Layout:** Single row, name left, links right (or stacked on mobile)

**Left:**
```
© Gimena Blanco 2025
```

**Right:**
```
LinkedIn    GitHub    Portfolio    Email
```

| Link | Target |
|---|---|
| LinkedIn | `https://linkedin.com/in/gimenablanco` |
| GitHub | `https://github.com/GimeVerdant` |
| Portfolio | `https://www.gimenablanco.com` |
| Email | `mailto:hello@gimenablanco.com` |

**Notes:**
- Footer is functional, not expressive — keep it clean and minimal
- "Portfolio" link goes to old gimenablanco.com until this site replaces it
- No tagline or secondary copy needed in the footer

**Status:** ✅ All real links

---

---

## Content Audit — Real vs. Placeholder

| Section | Content | Status |
|---|---|---|
| Nav | All links and labels | ✅ Real |
| Hero | All copy locked | ✅ Real |
| Stats: 10+ years | Confirmed | ✅ Real |
| Stats: 5+ products | From existing site | ✅ Real |
| Stats: 17 repos | GitHub count, Feb 2026 | ✅ Real |
| About: paragraphs 1 & 2 | From existing site copy | ✅ Real |
| About: paragraph 3 (transition) | Drafted from research | ⚠️ Needs Gimena review |
| Skills grid | From existing site | ✅ Real |
| Farm Timeline card | From case study | ✅ Real |
| Label Editor card | From case study | ✅ Real |
| Scaling Up at Zivver card | From case study | ✅ Real |
| Code Lab intro | Drafted | ⚠️ Needs Gimena review |
| Code Lab project cards | Real GitHub repos | ✅ Real |
| Contact copy | From existing site | ✅ Real |
| Contact email | Confirmed | ✅ Real |
| Footer links | All confirmed | ✅ Real |

**Items needing Gimena's sign-off:**
1. About paragraph 3 — the transition paragraph. Tone and facts are right; she should read it and adjust the voice to match her own.
2. Code Lab intro — honest and matches her voice, but she should confirm she's comfortable describing the projects as "not polished."
3. Award name for Aegon — not in this site plan (Aegon not in selected works), but if added later it needs the real award name.

---

## What Is Not In This Plan (By Design)

- **Aegon Risk Assessment** — not in the selected 3 case studies as instructed. If added later, it's the strongest credibility piece and should lead the work section. → [gimenablanco.com/aegon-risktool](https://www.gimenablanco.com/aegon-risktool)
- **Lightspeed Shipping** — not in the selected 3. Could replace Label Editor if more eCommerce depth is needed. → [gimenablanco.com/shipping](https://www.gimenablanco.com/shipping)
- **RAD Property Management** — early-career work, correctly excluded from main portfolio. → [gimenablanco.com/rad](https://www.gimenablanco.com/rad)
- **Timeline / work history section** — not requested; not recommended for a landing page format.
- **Blog or writing** — no published articles found in research. If she writes in future, a "writing" section could go between Code Lab and Contact.
