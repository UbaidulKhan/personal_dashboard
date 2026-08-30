# PCC v2.2 — DESIGN.md
> UI & Design Specification — Personal Command Center
> Last updated: April 2026

---

## 1. Design Philosophy

PCC is a **personal life operating system** — it must feel like a thoughtfully crafted tool, not a product dashboard. The guiding principles:

| Principle | What it means in practice |
|---|---|
| **Calm clarity** | Information is always visible, never overwhelming. Whitespace is a feature. |
| **Purposeful density** | Markets is dense like Bloomberg. Spiritual is spacious like a journal. Each pillar earns its density level. |
| **Earth-grounded** | The palette is warm, organic, and rooted — not clinical SaaS blue. |
| **Alive but not restless** | Rich animations reward interaction without distracting from focus. |
| **Responsive by context** | iPhone gets a bottom tab bar and full-screen cards. iPad gets a sidebar. MacBook gets the full layout. Same SPA, different shell. |

**Primary design reference:** Notion — clean card surfaces, generous whitespace, subtle borders, no visual noise.

---

## 2. Color System

### 2.1 Base Palette (Light Mode)

| Token | Value | Usage |
|---|---|---|
| `--bg-page` | `#F9F7F4` | App background (warm off-white) |
| `--bg-card` | `#FFFFFF` | Card surfaces |
| `--bg-sidebar` | `#F4F1EE` | Left sidebar background |
| `--border-subtle` | `#E8E4DF` | Card borders, dividers |
| `--text-primary` | `#1A1612` | Headings, primary labels |
| `--text-secondary` | `#6B6560` | Subtext, metadata, timestamps |
| `--text-tertiary` | `#A09890` | Placeholder, disabled |
| `--shadow-card` | `0 1px 4px rgba(0,0,0,0.06), 0 4px 16px rgba(0,0,0,0.04)` | Default card shadow |
| `--shadow-elevated` | `0 4px 12px rgba(0,0,0,0.10), 0 12px 32px rgba(0,0,0,0.07)` | Modals, popovers |

### 2.2 Pillar Accent Colors

Each pillar has a primary accent, a lighter tint (for backgrounds/chips), and a dark shade (for text on tint).

| Pillar | Accent | Tint (10% opacity bg) | Dark shade | Emoji |
|---|---|---|---|---|
| **Markets** | `#2D6A4F` Forest Green | `#EAF2EE` | `#1A3D2E` | 💹 |
| **Health** | `#C1440E` Terracotta | `#FAEEE9` | `#7A2A08` | 💚 |
| **Spiritual** | `#B5862A` Warm Gold | `#FBF4E6` | `#7A5A1A` | 🕋 |
| **Family** | `#D4883A` Amber | `#FDF2E7` | `#8A5520` | 👪 |
| **Morning** | `#E09B3D` Sunrise Gold | `#FDF4E3` | `#905F1E` | ☀️ |
| **Entertainment** | `#4A5C7A` Slate Blue | `#EDF0F5` | `#2B3648` | 🎙 |

### 2.3 Semantic / Status Colors

| Token | Value | Usage |
|---|---|---|
| `--color-success` | `#2D6A4F` | Gains, on-time, completed |
| `--color-danger` | `#C1440E` | Losses, missed, urgent |
| `--color-warning` | `#E09B3D` | Caution, approaching deadline |
| `--color-neutral` | `#6B6560` | Neutral state, pending |

### 2.4 Prayer Countdown Color States

The prayer countdown card animates color based on time remaining. This is one of the most important real-time UI behaviors in the app.

| Time Remaining | Color | Behavior |
|---|---|---|
| > 60 min | `#2D6A4F` Forest Green | Steady, no urgency |
| 30–60 min | `#D4883A` Amber | Slow pulse animation begins |
| 10–30 min | `#E09B3D` Sunrise Orange | Medium pulse, countdown bolder |
| < 10 min | `#C1440E` Terracotta Red | Fast pulse + ring flashes |
| < 5 min | Red + white strobe-glow | Ring arc animates rapidly, label weight 800 |
| Prayer time now | Gold flash burst | Celebratory `prayerBurst` keyframe, adhan plays |

---

## 3. Typography

### 3.1 Font Stack

| Role | Font | Fallback |
|---|---|---|
| **UI / Body** | `Inter` (Google Fonts) | `system-ui, sans-serif` |
| **Headings** | `Inter` weight 600–700 | Same |
| **Data / Mono** | `JetBrains Mono` | `monospace` |
| **Arabic text** | `Amiri` (Google Fonts) | `Noto Naskh Arabic, serif` |

```html
<!-- Google Fonts import -->
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=JetBrains+Mono:wght@400;500&family=Amiri:wght@400;700&display=swap" rel="stylesheet">
```

### 3.2 Type Scale

| Token | Size | Weight | Line height | Usage |
|---|---|---|---|---|
| `--text-xs` | 11px | 400 | 1.4 | Timestamps, badges |
| `--text-sm` | 13px | 400 | 1.5 | Secondary body, metadata |
| `--text-base` | 15px | 400 | 1.6 | Primary body, card content |
| `--text-md` | 17px | 500 | 1.5 | Card titles, list items |
| `--text-lg` | 20px | 600 | 1.3 | Section headings |
| `--text-xl` | 24px | 700 | 1.2 | Page headings |
| `--text-2xl` | 32px | 700 | 1.1 | Hero values (P&L, sleep score) |
| `--text-display` | 48px | 700 | 1.0 | Prayer countdown timer |

### 3.3 Typography Rules

- Headings always `--text-primary`. Never bold body text unless it's a data value.
- Data values (prices, scores, countdowns) use `JetBrains Mono` for alignment clarity.
- Arabic text uses `Amiri`, right-to-left, always in its own layout block — never mixed inline with Latin.
- Avoid ALL CAPS except for very short UI labels (2–3 chars max, e.g., "VIX", "AM", "PM").

---

## 4. Layout System

### 4.1 Spacing Scale (8px base grid)

| Token | Value |
|---|---|
| `--space-1` | 4px |
| `--space-2` | 8px |
| `--space-3` | 12px |
| `--space-4` | 16px |
| `--space-5` | 20px |
| `--space-6` | 24px |
| `--space-8` | 32px |
| `--space-10` | 40px |
| `--space-12` | 48px |
| `--space-16` | 64px |

### 4.2 Border Radius

| Token | Value | Usage |
|---|---|---|
| `--radius-sm` | 6px | Chips, badges, small buttons |
| `--radius-md` | 10px | Cards, inputs |
| `--radius-lg` | 16px | Modal panels, drawer |
| `--radius-xl` | 24px | Full-screen overlays, bottom sheets |
| `--radius-full` | 9999px | Pills, avatar circles, ring arcs |

---

## 5. Responsive Breakpoints & Shell Layout

PCC adapts its navigation shell across three device contexts. The SPA content area is identical — only the chrome changes.

### 5.1 Breakpoints

| Name | Min width | Device |
|---|---|---|
| `mobile` | 0px | iPhone |
| `tablet` | 768px | iPad |
| `desktop` | 1200px | MacBook Pro |

### 5.2 Shell Layout per Device

#### iPhone (mobile)
- **No sidebar.** Navigation is a **bottom tab bar** with 6 pillar icons + labels.
- Content fills the full width above the tab bar.
- Cards are full-width, stacked vertically.
- Today Dashboard: Prayer hero card full-width, Morning card below, then 1-column card stack.
- Drawer/modal overlays slide up from bottom (iOS sheet feel).
- Safe area insets respected for notch and home indicator.

#### iPad (tablet)
- **Collapsible left sidebar** (240px wide, collapses to 60px icon-only rail).
- Toggle with arrow button at the sidebar top.
- Content area fills remaining width.
- Today Dashboard: Prayer hero card + right column of pillar summaries visible simultaneously.
- Modals are centered overlays, not full-screen.

#### MacBook Pro (desktop)
- **Always-visible left sidebar** (240px fixed).
- Sidebar shows pillar icons + labels. No collapse needed.
- Content area: max-width 1200px, centered, `--space-8` padding on each side.
- Today Dashboard: Hero prayer card (60% width) + right column of pillar summary cards (40%).
- Hover states and keyboard shortcuts active.

---

## 6. Navigation & Sidebar

### 6.1 Sidebar Structure (Desktop / iPad)

```
┌─────────────────────────┐
│  ⬡ PCC                  │  ← Wordmark: Inter 700, 18px
│  Personal Command Center│  ← Subtext: Inter 400, 11px, --text-tertiary
├─────────────────────────┤
│  ☀️  Today              │  ← Always first
│  💹  Markets            │
│  💚  Health             │
│  🕋  Spiritual          │
│  👪  Family             │
│  🎙  Entertainment      │
│  ☀️  Morning Routine    │
├─────────────────────────┤
│  ⚙️  Settings           │  ← Pinned at bottom
└─────────────────────────┘
```

### 6.2 Sidebar Item States

| State | Style |
|---|---|
| Default | `--text-secondary`, no background |
| Hover | Pillar accent tint background, `--text-primary` |
| Active | Pillar accent tint background, 3px left border in accent, `--text-primary` weight 600 |

### 6.3 SPA Page Transitions

All navigation between pillars uses a **fade + slide** transition:
- Outgoing view: opacity 1→0, translateX(0→-20px), 180ms
- Incoming view: opacity 0→1, translateX(20px→0), 180ms
- Easing: `cubic-bezier(0.4, 0, 0.2, 1)`

Intra-pillar navigation (e.g., Today card → Morning Routine screen):
- Mobile: bottom sheet slides up
- Desktop: right panel slides in from the right

---

## 7. Today Dashboard (Landing Page)

The Today Dashboard is the most critical screen. It must feel **alive and dynamic** — immediately surfacing what matters right now across all pillars.

### 7.1 Layout (Desktop)

```
┌───────────────────────────────────────────────────────────────────┐
│  Good morning, Ubaid   ·   Wednesday, April 23  ·  Sterling, VA  │
├────────────────────────────────┬──────────────────────────────────┤
│                                │  💚 Health                       │
│   🕌 PRAYER HERO CARD         │  2,340 steps · 1,840 kcal        │
│   (60% width — ring arc,      ├──────────────────────────────────┤
│    live countdown, 5 prayers) │  💹 Markets                      │
│                                │  S&P +0.4%  ·  VIX 18.2         │
├────────────────────────────────┴──────────────────────────────────┤
│  ☀️  Morning Routine Card  (full width, compact)                  │
├──────────────────┬──────────────────┬─────────────────────────────┤
│  🕋 Spiritual    │  👪 Family       │  🎙 Entertainment            │
│  Hifz streak     │  Active project  │  Queue: 3 items              │
└──────────────────┴──────────────────┴─────────────────────────────┘
⚡ RIGHT NOW STRIP (dynamic urgency feed, auto-refreshing)
```

### 7.2 Right Now Strip (Dynamic Urgency Feed)

This strip lives below all cards and surfaces the highest-priority time-sensitive items from every pillar in real time.

- Items ranked by urgency: prayer times first, then hard deadlines, then soft goals
- Auto-refreshes every 60 seconds
- Each chip is tappable and deep-links to the relevant pillar/screen
- New chips animate in with a spring `chipSlideDown` keyframe
- Examples:

```
⚡ RIGHT NOW
[ 🕌 Asr in 23 min ]  [ 📋 Task due: Milestone X ]  [ 💹 Signal alert: AAPL ]  [ 💚 340 kcal remaining ]
```

### 7.3 Prayer Hero Card

The #1 element on the page. Must be immediately readable and emotionally grounding.

**Contents:**
- Current/next prayer name — large, `--text-xl`, shown in both transliteration + Arabic (`Amiri` font)
- **Animated ring arc** — SVG circular progress arc counting down time until next prayer
- **Live countdown** — `JetBrains Mono --text-display` (HH:MM:SS), updates every second
- Color + pulse animation transitions through urgency states (see Section 2.4)
- All 5 prayers listed in a compact row below with status badges (✅ On Time · 🟡 Qada · ❌ Missed · ⬜ Upcoming)
- **Friday:** Jumu'ah banner replaces the Dhuhr row with location (Adams Center), imam, and departure countdown

**Prayer countdown animation behavior:**
- Ring arc depletes clockwise as time passes
- Color transitions smoothly via CSS custom property interpolation
- < 10 min: ring pulses with `pulseGlow` keyframe
- < 5 min: countdown font-weight increases to 800, ring arc speed increases
- At prayer time: `prayerBurst` gold flash keyframe plays across card background, adhan audio triggers

### 7.4 Morning Routine Card (Today version — compact)

Full-width card below the hero row. Warm sunrise gold accent.

**Contents (left to right on desktop, stacked on mobile):**
1. Sleep badge (colored pill: Excellent / Good / Poor / Overslept) + duration in hours
2. Mood selector — 5 emoji icon tiles, selected highlighted in sunrise gold
3. Recommendation chips — music genre + caffeine + breakfast (tappable)
4. Claude 1-sentence narrative — italic, `--text-secondary`
5. "See full routine →" link in sunrise gold

---

## 8. Per-Pillar Design Rules

### 8.1 💹 Markets — Bloomberg-lite Density

**Goal:** Dense, data-forward, every pixel earns its place.

- Full-width data tables with tight 40px rows, monospaced values, red/green delta badges
- Charts use a **dark background** (`#1A1612`) even in light mode — intentional contrast for financial readability
- VIX / Macro strip: horizontal scrollable pill row pinned at top of Markets view
- Signal engine: large `--text-2xl` score number + color ring + Claude narrative paragraph below
- News feed: compact list — publication + title + sentiment chip. No thumbnails.
- All chrome accented in Forest Green `#2D6A4F`

### 8.2 💚 Health — Rings + Charts

**Goal:** Motivated, visual, Apple Health-inspired but warmer.

- Today card: large calorie ring (center) + steps arc + sleep badge — horizontal trio
- Rings: SVG `stroke-dasharray` circles, terracotta accent, spring-animated fill on load
- Sleep chart: 30-day sparkline with 10PM–6AM target band softly shaded in tint
- Exercise chart: bar chart per type (swim / walk / weights) with weekly completion
- Weight chart: line chart actual vs. goal trajectory
- All chrome accented in Terracotta `#C1440E`

### 8.3 🕋 Spiritual — Warm, Reverent, Spacious

**Goal:** The most visually distinct pillar. Calm, classical, unhurried.

- Screen background tint: `#FEFBF5` (warmer than standard `--bg-page`)
- Arabic text: `Amiri` font, `--text-xl` minimum, right-aligned, `dir="rtl"`, `lang="ar"`
- Quran reader: two-column layout — Arabic right (large) + transliteration/translation left (smaller). Tap-to-highlight words.
- Arabic letter guide: canvas tracing area with cream background, stroke in warm gold
- Prayer history rings: 5-segment daily ring × 7 days in a row. Green = on time, amber = qada, red = missed, gray = upcoming.
- Hifz flashcard: card-based UI, progress bar in warm gold, streak flame icon
- All chrome accented in Warm Gold `#B5862A`

### 8.4 👪 Family — Kanban with Warmth

**Goal:** Warm and organized. A family planner, not a PM tool.

- Activity Planner: two columns (Daughter | Wife), Kanban lanes (Planned / In Progress / Done)
- Activity cards: larger padding, category chip, photo thumbnail on completed items
- AI suggestion cards: amber tint background, `✨` icon prefix, Approve / Skip CTAs
- Side Hustle PM: Trello-style board + Gantt timeline toggle. Dependency lines in amber.
- Claude weekly summary: pinned banner at top of Side Hustle view, soft amber callout card
- All chrome accented in Amber `#D4883A`

### 8.5 ☀️ Morning Routine — Full Detail Screen

**Goal:** Warm and motivating. A personal morning briefing.

- Top of screen: sunrise gradient `linear-gradient(180deg, #FDF4E3 0%, #F9F7F4 200px)`
- Sleep banner: duration + quality score + tier badge + deviation from 10PM–6AM target
- Mood picker: 5 large emoji + label tiles in a horizontal row. Selected = sunrise gold border + tint.
- Music section: recommended genre card (large, Play button opens YouTube). 6 alternate genre tiles in 3×2 grid below. Quran shortcut always at top.
- Caffeine + Breakfast cards: side-by-side on desktop, stacked on mobile. Icon + recommendation + reasoning + ✓ Log / Skip buttons.
- Claude narrative: italic blockquote, soft 3px left border in sunrise gold
- Rating prompt: at the bottom — "How was yesterday?" with 👍 👎 + optional note field
- All chrome accented in Sunrise Gold `#E09B3D`

### 8.6 🎙 Entertainment — Queue-focused

**Goal:** Clean media browser feel.

- Daily queue: ordered list of podcast episodes + YouTube videos with Play / Open buttons
- Mini-player bar: pinned at screen bottom when audio is playing (above tab bar on mobile). Shows title, thumbnail, speed control, 15s skip, scrub bar.
- YouTube items: thumbnail + title + channel + duration chip
- Interest tag filters: colored chip row at top to filter queue by topic
- All chrome accented in Slate Blue `#4A5C7A`

---

## 9. Component Library

### 9.1 Cards

All cards share:
- Background: `--bg-card` (`#FFFFFF`)
- Border: `1px solid var(--border-subtle)`
- Border-radius: `--radius-md` (10px)
- Box-shadow: `--shadow-card`
- Padding: `--space-6` (24px)

| Variant | Difference |
|---|---|
| `card-hero` | Padding 32px, `--shadow-elevated` |
| `card-compact` | Padding 12px, smaller type |
| `card-pillar` | 4px left border in pillar accent color |
| `card-urgent` | 4px left border red + subtle red tint background |
| `card-ai` | Dashed border, `✨` icon, pillar tint background |

### 9.2 Badges & Chips

- **Sleep tier:** colored pill — Excellent (green), Good (amber), Poor (red), Overslept (gray)
- **Prayer status:** small color dot + label
- **Signal score:** large colored circle badge
- **Mood:** emoji + label pill, selected = accent border + tint
- **Urgency chip:** icon + label, accent tint fill, tappable

### 9.3 Buttons

| Variant | Style |
|---|---|
| `btn-primary` | Pillar accent fill, white text, `--radius-sm` |
| `btn-secondary` | Accent tint fill, accent text, subtle border |
| `btn-ghost` | No fill, accent text, hover shows tint |
| `btn-icon` | Square, ghost, icon only |
| `btn-danger` | Terracotta fill, white text |

All buttons: `transition: all 150ms ease`, `transform: scale(0.97)` on `:active`.

### 9.4 Inputs

- Height: 40px
- Border: `1px solid var(--border-subtle)`, focus: `2px solid pillar-accent`
- Background: white
- Border-radius: `--radius-sm`
- Placeholder: `--text-tertiary`

### 9.5 Ring / Arc Progress Components

Used in: Prayer countdown, Health calorie ring, Exercise rings, Hifz progress.

- SVG `<circle>` with `stroke-dasharray` / `stroke-dashoffset`
- `stroke-linecap: round`
- Fill animation: `transition: stroke-dashoffset 800ms cubic-bezier(0.4, 0, 0.2, 1)` on mount
- Prayer ring additionally applies `pulseGlow` keyframe for urgency states

---

## 10. Animation System

### 10.1 Core Keyframes

```css
/* Page transition */
@keyframes slideInRight {
  from { opacity: 0; transform: translateX(20px); }
  to   { opacity: 1; transform: translateX(0); }
}

/* Card entrance */
@keyframes cardEntrance {
  from { opacity: 0; transform: translateY(12px) scale(0.98); }
  to   { opacity: 1; transform: translateY(0) scale(1); }
}

/* Prayer urgency pulse */
@keyframes pulseGlow {
  0%, 100% { box-shadow: 0 0 0 0 rgba(193, 68, 14, 0); }
  50%       { box-shadow: 0 0 0 14px rgba(193, 68, 14, 0.15); }
}

/* Prayer time gold burst */
@keyframes prayerBurst {
  0%   { background-color: var(--bg-card); }
  20%  { background-color: #FBF4E6; }
  100% { background-color: var(--bg-card); }
}

/* Right Now strip chip entrance */
@keyframes chipSlideDown {
  from { opacity: 0; transform: translateY(-8px); }
  to   { opacity: 1; transform: translateY(0); }
}

/* Bottom sheet slide-up */
@keyframes sheetSlideUp {
  from { transform: translateY(100%); }
  to   { transform: translateY(0); }
}
```

### 10.2 Timing Standards

| Interaction | Duration | Easing |
|---|---|---|
| Hover state | 120ms | `ease` |
| Button press | 100ms | `ease` |
| Card entrance (per card) | 220ms | `cubic-bezier(0.4, 0, 0.2, 1)` |
| Pillar transition | 180ms | `cubic-bezier(0.4, 0, 0.2, 1)` |
| Bottom sheet / right panel | 300ms | `cubic-bezier(0.2, 0, 0, 1)` |
| Ring arc fill (on load) | 800ms | `cubic-bezier(0.4, 0, 0.2, 1)` |
| Prayer urgency pulse | 1.8s infinite | `ease-in-out` |
| Prayer burst | 600ms | `ease` |

### 10.3 Card Entrance Stagger

Cards on the Today Dashboard animate in sequentially:

```
Card 1: delay 0ms
Card 2: delay 60ms
Card 3: delay 120ms
Card N: delay min(N × 60ms, 360ms)
```

### 10.4 Reduced Motion

All non-functional animations must respect `prefers-reduced-motion`:

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
```

The prayer countdown timer itself (seconds ticking) is always active regardless of this preference — it is functional, not decorative.

---

## 11. Iconography

- **Icon library:** [Lucide Icons](https://lucide.dev/) — consistent stroke weight, open source
- **Pillar identity:** Emoji in nav (matches the plan doc). Lucide for functional UI icons (chevron, close, settings, check, etc.)
- **Icon sizes:** 16px inline, 20px buttons/nav, 24px card headers, 32px hero
- **Custom SVG assets needed:**
  - Mosque silhouette (prayer hero card)
  - Crescent moon (Spiritual nav icon alternative)
  - Quran book icon
  - These are not available in Lucide and should be custom SVG

---

## 12. Responsive Behavior Summary

| Element | iPhone | iPad | MacBook |
|---|---|---|---|
| Navigation | Bottom tab bar | Collapsible left sidebar | Always-visible left sidebar |
| Today layout | Full-width stacked | Prayer hero full-width + scroll | Hero 60% + cards 40% |
| Card columns | 1 | 2 | 3 |
| Morning Routine | Full-screen overlay | Centered modal | Right panel slide-in |
| Prayer card | Full-width hero | Full-width hero | 60% width hero |
| Pillar sub-pages | Bottom sheet | Centered modal | Right panel |
| Markets table | Horizontal scroll | Full width | Full width |
| Quran reader | Single column | Two column | Two column |
| Sidebar width | — (bottom tabs) | 240px collapsible | 240px fixed |

---

## 13. Accessibility

- Minimum contrast: 4.5:1 for body text, 3:1 for large text (WCAG AA)
- All interactive elements have a visible focus ring: `outline: 2px solid pillar-accent; outline-offset: 2px`
- Arabic text: always `lang="ar"` and `dir="rtl"` on containing elements
- Prayer countdown: urgency never communicated by color alone — always paired with text countdown and pulse animation
- Prayer adhan: mute button always visible in the prayer hero card

---

## 14. Open Questions

> Items to resolve before frontend implementation begins.

1. **iPad sidebar collapse** — collapsed state: icon-only 60px rail, or fully hidden with swipe-to-open gesture?
2. **Adhan audio** — does it interrupt morning music playback, or duck the volume and play over it?
3. **Markets chart theme** — dark chart backgrounds confirmed even in light mode app? Or match the warm light theme?
4. **App logo/wordmark** — custom icon for PCC, or just `PCC` text in Inter 700?
5. **Jumu'ah card** — distinct visual treatment (e.g., teal or gold accent, special banner) to differentiate Friday's card from the standard prayer card?
