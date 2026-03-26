# ImpactQ — Strategic Impact Visualization Platform

**Brand:** InsightQ Product Family
**Tagline:** *See your strategy bloom.*
**Audience:** C-Suite, Board of Directors, Department Heads (Director+), External Stakeholders

---

## Product Vision

ImpactQ is a high-level strategic planning visualization tool that connects **Strategic Objectives** to **Tactical Plans** — and stops there. No subtasks, no Gantt charts, no transactional minutiae. It exists to answer one question in under 3 seconds: *"Are we on track?"*

The visual metaphor is **botanical growth** — abstract, not literal. Strategic objectives are organic clusters on a living canvas. Tactical plans emerge as petals that unfurl as progress advances. Color warms from cool teal (dormant) to rich gold (complete). The canvas breathes with subtle particle animation, signaling live data.

It's a strategy dashboard that looks and feels like a world-class website, and presents like an Apple Keynote.

---

## Core Architecture

### Two-Layer Data Model (Non-Negotiable)

| Layer | What It Is | Limit |
|-------|-----------|-------|
| **Strategic Objective** | A high-level organizational goal (e.g., "Expand donor partnerships by 40%") | Max 7 per org |
| **Tactical Plan** | A named initiative under a strategic objective (e.g., "Launch corporate donation program") | Max 8 per objective |

Nothing below tactical plans. No subtasks, no action items, no dependencies. If you need that granularity, use a different tool. ImpactQ's discipline IS the feature.

### Three View Modes

1. **Garden View** — The landing screen. All strategic objectives visible as organic radial clusters on a living canvas. Particles drift gently. Board-room ambient.
2. **Bloom View** — Click a cluster to expand. The single objective fills the screen with its tactical petals radiating outward. Each petal shows status through shape and color.
3. **Present Mode** — Full-screen, zero chrome. Swipe/arrow to navigate objective by objective. Auto-narration option. The canvas breathes. This is the board meeting mode.

### Operating Toggle

From Bloom View, a single toggle switches to **Cascade View** — a clean, structured list format showing the same data as text cards. For directors who prefer scanning tables over visual metaphor.

---

## Visual Design System

### Color Palette (Extending InsightQ Brand)

| Token | Value | Usage |
|-------|-------|-------|
| Sage | `#8A9B8E` | InsightQ brand primary, secondary elements |
| Linen | `#EDEAE0` | Background surfaces, warmth |
| Charcoal | `#3D3835` | Primary text, headings |
| Warm Gold | `#D4A574` | Progress/completion accent, bloom state |
| **Deep Teal** | `#2A6B6B` | **ImpactQ accent** — dormant/seed state, growth |
| Amber Alert | `#C07A6B` | At-risk status |

### Status Encoding (Shape + Color, WCAG Compliant)

| Status | Petal Shape | Color | Icon |
|--------|------------|-------|------|
| Not Started | Hollow dotted outline | Deep Teal `#2A6B6B` | ○ Seed |
| In Progress | Partial fill, soft edges | Teal → Sage gradient | ◐ Sprouting |
| At Risk | Notched/cracked petal | Amber `#C07A6B` | ⚠ Wilting |
| Complete | Full rounded with sparkle | Warm Gold `#D4A574` | ✦ Bloomed |

### Typography

| Role | Font | Weight | Size |
|------|------|--------|------|
| Headlines (Strategic Objectives) | Instrument Serif | 500 | 32–48px |
| Subheads (Tactical Plans) | Inter | 600 | 18–24px |
| Body / Status Text | Inter | 400 | 14–16px |
| Data / Metrics | Inter | 700 (tabular) | 20–28px |

### Motion Principles

- **Entry:** Seeds drift onto canvas with wind-like easing (cubic-bezier 0.25, 0.1, 0.25, 1.0)
- **Bloom:** Petals unfurl radially from center over 600ms with staggered delay
- **Breathing:** Background particles move at 0.5px/s with 8s opacity cycle
- **Transitions:** View changes use morph animations (element position interpolation)
- **Reduced motion:** All animations respect `prefers-reduced-motion`, falling back to fade

---

## Moonchild.ai Studio Prompts

Use these prompts in sequence inside [studio.moonchild.ai](https://studio.moonchild.ai/). Start with the Design System prompt, then generate screens one at a time.

---

### PROMPT 1: Design System Foundation

```
Create a design system for a B2B strategic planning SaaS product called "ImpactQ"
by InsightQ. The design language is "abstract botanical" — inspired by organic
growth patterns (radial expansion, natural curves, warm color progressions) but
NOT literal flower illustrations. Think modern, premium, Linear.app-meets-nature.

Color tokens:
- Primary surface: #FAFAF7 (warm white)
- Card surface: #FFFFFF
- Primary text: #3D3835 (charcoal)
- Secondary text: #5A5550
- Brand primary: #8A9B8E (sage green)
- Brand dark: #6B7F70
- ImpactQ accent: #2A6B6B (deep teal — represents growth/seed state)
- Success/completion: #D4A574 (warm gold — represents full bloom)
- Warning/at-risk: #C07A6B (warm amber)
- Border: #E8E5DC
- Pale background: #E8EDE9

Typography: Instrument Serif for display headings (32-48px, weight 500).
Inter for all other text (14-24px, weights 400-700). Tabular numerals for
any metrics.

Spacing: 8px base unit. Border radius: 12px for cards, 8px for buttons,
24px for large containers.

Component variants needed:
- Status badge (4 states: Not Started, In Progress, At Risk, Complete) using
  BOTH shape and color differentiation for accessibility
- Objective card (large, radial/organic shape, contains title + health score
  + petal count)
- Tactical plan card (smaller, petal-shaped with rounded edges)
- Navigation bar (minimal, frosted glass effect, brand logo left)
- Toggle switch (Bloom View / Cascade View)
- Full-screen presentation controls (minimal, bottom-center, auto-hide)

Prioritize accessible contrast ratios (WCAG AA minimum). Include hover and
disabled states for all interactive components. This should feel like a
premium product — think Stripe, Linear, or Notion in visual polish, but with
warm organic energy instead of cold tech.
```

---

### PROMPT 2: Garden View (Landing / Dashboard)

```
Design the main landing screen for ImpactQ called "Garden View." This is a
strategic planning dashboard for C-suite executives and board members.

Layout: A living canvas showing 5 strategic objectives as abstract organic
clusters arranged in a balanced, asymmetric composition (NOT a grid). Each
cluster is a radial shape — like an abstract flower viewed from above — with
3-6 petal shapes radiating from a center node.

Each strategic objective cluster shows:
- Objective title in Instrument Serif (e.g., "Workforce Excellence")
- A circular health score badge at center (e.g., "78%")
- Petal shapes around it representing tactical plans, each filled/colored
  based on status (teal outline = not started, partial sage fill = in progress,
  warm gold full = complete, amber with notch = at risk)
- A subtle connecting line between clusters showing strategic alignment

Background: Warm white (#FAFAF7) with very subtle floating particle dots
(tiny, 2-3px, low opacity sage/teal, drifting slowly) that give the canvas
a living, breathing quality.

Top navigation: Frosted glass navbar with InsightQ logo (left), "ImpactQ"
product name, and minimal controls (search, present button, user avatar).

Bottom-right: Floating action button to add new strategic objective (organic
rounded shape, deep teal).

The overall feeling should be: calm authority. A board member walks into a
room, this is on the screen, and they immediately feel informed and
impressed. No clutter, no noise. Premium and alive.

Typography: Instrument Serif for objective titles, Inter for all other text.
Color palette: sage green primary, deep teal accent, warm gold for completion,
charcoal text on warm white background.
```

---

### PROMPT 3: Bloom View (Single Objective Expanded)

```
Design the "Bloom View" screen for ImpactQ — what users see when they click
into a single strategic objective from the Garden View.

Layout: The selected strategic objective is centered and expanded to fill
the canvas. The objective title is large at top-center in Instrument Serif
(e.g., "Expand Donor Partnerships by 40%"). Below it, a health score ring
(circular progress indicator, organic/thick, using teal-to-gold gradient
based on completion).

Radiating outward from the center ring are 6 tactical plan "petals" —
abstract rounded shapes arranged in a radial pattern. Each petal contains:
- Tactical plan name (Inter 600, e.g., "Corporate Donation Program")
- Status indicator using BOTH shape and color (hollow teal outline = not
  started, half-filled sage = in progress, full warm gold = complete,
  notched amber = at risk)
- A small percentage (e.g., "65%")
- Owner avatar (tiny, bottom of petal)

In the top-right corner: a toggle switch labeled "Bloom | Cascade" that
lets users switch to a list/table view of the same data.

Background: Same warm white with subtle particles, but particles are
slightly more concentrated around the center objective, as if drawn to it.

When a petal is hovered, it should subtly scale up (1.03x) with a soft
shadow increase, indicating it's clickable for detail.

Include breadcrumb navigation at top-left: "Garden > Workforce Excellence"

The overall feel: focused yet spacious. You're looking at one strategic
priority in depth, but it doesn't feel dense or overwhelming. Each tactical
plan is a visual element you can scan in 2 seconds.
```

---

### PROMPT 4: Cascade View (Structured Alternative)

```
Design the "Cascade View" for ImpactQ — the structured list alternative
that appears when users toggle from Bloom View. Same data, clean card layout.

Layout: Left sidebar showing all strategic objectives as a vertical list
(the one selected is highlighted with a sage left-border accent). The
selected objective's title appears as a large header in the main content area.

Main content: A vertical stack of tactical plan cards. Each card is a
clean, wide rectangle with generous padding (24px) and subtle border.
Cards contain:
- Tactical plan name (Inter 600, 18px)
- Status badge (using the 4-state shape+color system: seed, sprouting,
  wilting, bloomed)
- Progress bar (thin, organic rounded ends, teal-to-gold gradient fill)
- Owner name and avatar
- Last updated date (muted text)

Cards are sorted by status: At Risk first (amber highlight on left edge),
then In Progress, Not Started, Complete.

Top of content area: Summary bar showing "4 of 6 tactical plans on track"
with a small ring chart.

The toggle in top-right still shows "Bloom | Cascade" with Cascade active.

This view should feel like a premium version of Notion or Linear's list
view — clean, spacious, excellent typography, but with the warm InsightQ
color palette instead of cold grays. Card hover state: subtle lift with
shadow increase.
```

---

### PROMPT 5: Present Mode (Board Room / Full Screen)

```
Design the "Present Mode" for ImpactQ — a full-screen, zero-chrome
presentation view designed for live board meetings and executive reviews.

Layout: No navigation bar, no sidebar, no buttons visible by default.
The entire screen is one strategic objective presented beautifully.

Center of screen: The strategic objective title in large Instrument Serif
(48px, charcoal). Below it, the health score as a large, elegant ring
(120px diameter, thick stroke, teal-to-gold gradient fill based on
progress percentage, with the percentage in the center at 36px bold).

Below the ring: Tactical plan petals arranged in a horizontal row
(not radial — optimized for widescreen projection). Each petal is a
refined card showing plan name, status shape+color, and percentage.
Cards have generous spacing between them.

Background: Warm white with very subtle gradient (slightly warmer at
bottom). The floating particles are present but at lower density and
slower speed — ambient, professional, not distracting.

Bottom-center (appears on hover/mouse movement): Minimal presentation
controls — left arrow, dot indicators for each objective (like iOS
page dots), right arrow. Controls fade out after 2 seconds of no
interaction.

Top-right (appears on hover): "Exit Present" button (small, muted).

The vibe: This should look like an Apple Keynote slide that happens to
be connected to live data. Board members should feel like they're
watching a polished presentation, not looking at a software tool.
Premium, calm, authoritative. The kind of screen that makes people
ask "What tool is that?"

Include a subtle "ImpactQ by InsightQ" watermark in bottom-left
(very small, low opacity sage text).
```

---

### PROMPT 6: Mobile / Tablet View

```
Design a responsive mobile view (375px width) and tablet view (768px width)
for ImpactQ's Garden View.

Mobile (375px):
- The garden canvas converts to a vertical scroll of objective cards
- Each card is full-width with rounded corners (16px), showing the
  objective title, health score ring (smaller, 60px), and a row of
  small petal indicators (colored dots with shape variants for status)
- Tap a card to expand inline and reveal tactical plan list below it
- Bottom tab bar: Garden, Search, Present, Profile
- Top: Compact header with "ImpactQ" logo and notification bell
- Background particles are disabled on mobile for performance

Tablet (768px):
- Two-column grid of objective clusters
- Each cluster is a card-based version of the desktop organic shape
- Petals are shown as small radiating elements within each card
- Swipe gestures supported for horizontal navigation in Present Mode
- Sidebar is hidden by default, accessible via hamburger menu

Both should maintain the warm white background, sage/teal/gold color
system, and Instrument Serif headings. Touch targets minimum 44px.
Cards should have clear tap affordance (subtle shadow, arrow indicator).

The mobile experience should feel like a premium native app — think
Linear mobile or Notion mobile — not a shrunk desktop site. Every
element should feel intentional at this size.
```

---

### PROMPT 7: Onboarding / Empty State

```
Design the first-time user experience for ImpactQ — the empty state
when no strategic objectives have been created yet.

Layout: The Garden View canvas is visible but empty. In the center,
a beautiful illustration-style animation concept: a single abstract
seed shape (deep teal, organic rounded form) sitting on the warm white
canvas with a gentle pulsing glow. Tiny particle dots drift around it
like wind carrying potential.

Above the seed: "Plant your first strategic objective" in Instrument
Serif (32px, charcoal). Below: "ImpactQ connects your big-picture
goals to the tactical plans that make them real. No minutiae. No
noise. Just strategy in bloom." in Inter (16px, muted text).

Below the text: A primary CTA button in deep teal — "Plant an Objective"
with a subtle seed icon. Secondary link below: "Import from existing plan"

To the right of center: A subtle, semi-transparent preview showing what
a bloomed garden looks like — 3-4 ghosted objective clusters with petals,
giving a glimpse of the future state. Very low opacity (15-20%), almost
like a watermark of possibility.

Bottom of screen: Three small feature cards in a row:
1. "Strategic Focus" — "Only objectives and tactical plans. Nothing more."
2. "Living Canvas" — "Watch your strategy grow in real-time."
3. "Board Ready" — "Present Mode turns data into a story."

This should feel inspiring, not empty. The user should feel excited to
plant their first objective, not overwhelmed. Warm, inviting, premium.
```

---

## Implementation Roadmap (Post-Mockup)

### Phase 1: Core MVP
- Garden View with static data
- Bloom View with petal expansion
- Cascade View toggle
- Two-layer data model (create/edit objectives and plans)
- Basic status tracking (4 states)

### Phase 2: Presentation Layer
- Present Mode with swipe navigation
- Entry animations (seed drift, petal unfurl)
- Breathing canvas with particle system
- Auto-narrative generation

### Phase 3: Live Data & Collaboration
- Real-time status updates
- Multi-user presence indicators
- Health score algorithm
- Board member view-only sharing links

### Phase 4: Mobile & Polish
- Responsive tablet/mobile views
- Accessibility audit (WCAG AA full compliance)
- High contrast mode
- Keyboard navigation for all views

---

## Competitive Positioning

| Feature | ImpactQ | Cascade.app | Perdoo | Mooncamp |
|---------|---------|-------------|--------|----------|
| Strategic-only (no task noise) | ✅ Enforced | ❌ Has subtasks | ❌ Has KRs + tasks | ❌ Has nested goals |
| Botanical visual metaphor | ✅ Unique | ❌ Flat maps | ❌ Tree diagrams | ❌ Standard charts |
| Presentation mode | ✅ Full-screen, animated | ❌ None | ❌ Export only | ❌ Basic report |
| Live breathing canvas | ✅ Particle system | ❌ Static | ❌ Static | ❌ Static |
| Board-room ready | ✅ Designed for it | ⚠️ Requires formatting | ❌ Too dense | ❌ Too PM-focused |

---

*Document generated by InsightQ Expert Panel — March 26, 2026*
*Panel: Maya (WMS), Carlos (WFM), Sarah (Retail Ops), Devon (DataViz), Priya (Mobile), James (Accessibility)*
