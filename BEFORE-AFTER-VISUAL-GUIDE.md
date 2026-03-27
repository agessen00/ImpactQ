# ImpactQ v4.3 Phase/Season System
## Before & After Visual Guide

---

## OVERVIEW

This document shows the visual and textual changes recommended by the 3-round expert panel review.

**Total Changes:** 4 critical fixes + 3 medium-priority enhancements
**Estimated Impact:** 7.5/10 botanical coherence (improved from 6.5/10 in v4.0)

---

## BEFORE & AFTER: THE FOUR CRITICAL FIXES

---

### FIX #1: "Season" → "Wave" Terminology

#### BEFORE (Confusing)
```
Phase Label                  Dependency Text                   Section Label
┌─────────────────────┐      ┌─────────────────────────────┐
│ First Season        │      │ depends on First Season      │   Strategic Garden
│ Second Season       │      │ depends on Second Season     │
│ Third Season        │      │ depends on Third Season      │
│ Fourth Season       │      │ depends on Fourth Season     │
└─────────────────────┘      └─────────────────────────────┘

Problem:
  ❌ "Season" implies calendar-driven (spring, summer, fall, winter)
  ❌ Phases are actually abstract cycles (unrelated to calendar)
  ❌ Confuses nonprofit users familiar with fiscal/grant cycles
  ❌ Phenologically misleading for Southern Hemisphere users
```

#### AFTER (Clear)
```
Phase Label                  Dependency Text                   Section Label
┌─────────────────────┐      ┌─────────────────────────────┐
│ Wave 1              │      │ depends on Wave 1           │   Strategic Garden
│ Wave 2              │      │ depends on Wave 2           │
│ Wave 3              │      │ depends on Wave 3           │
│ Wave 4              │      │ depends on Wave 4           │
└─────────────────────┘      └─────────────────────────────┘

Benefit:
  ✓ "Wave" is agnostic about calendar time
  ✓ Aligns with nonprofit language (project waves, funding waves)
  ✓ Fits Agile/iterative mindset (sprint waves)
  ✓ Still botanical (natural rhythms)
```

---

### FIX #2: Phase 4 Icon & Color

#### BEFORE (Breaks Metaphor)
```
Phase 1    Phase 2    Phase 3    Phase 4
┌──────┐   ┌──────┐   ┌──────┐   ┌──────┐
│ 🌱   │ ╭→│ 🌿   │ ╭→│ 🌳   │ ╭→│ 🏛   │
│ Seed │ │ │Sprout│ │ │ Tree │ │ │Build │
└──────┘ ╰─┴──────┘ ╰─┴──────┘ ╰─┴──────┘
Green   Teal    Brown    Gold

Problem:
  ❌ Phases 1–3 are LIVING organisms (botanical progression)
  ❌ Phase 4 is an ARCHITECTURAL monument (non-botanical)
  ❌ Signals "we've stopped growing" (stasis)
  ❌ Feels exclusive/institutional (contradicts Goodwill's mission)
  ❌ In some cultures, monuments = colonial imposition

Phases 1–3 Message: "Natural growth, alive, dynamic"
Phase 4 Message: "Institutional, static, final"

Narrative breaks at the end.
```

#### AFTER (Complete Botanical Narrative)
```
Phase 1    Phase 2    Phase 3    Phase 4
┌──────┐   ┌──────┐   ┌──────┐   ┌──────┐
│ 🌱   │ ╭→│ 🌿   │ ╭→│ 🌳   │ ╭→│ 🌾   │
│Estab.│ │ │Expand│ │ │Optim.│ │ │Harvest│
└──────┘ ╰─┴──────┘ ╰─┴──────┘ ╰─┴──────┘
Green    Teal    Brown   Orange

Benefit:
  ✓ All four are LIVING plants (consistent metaphor)
  ✓ Seed → Growth → Maturity → Harvest (natural cycle)
  ✓ Grain = productivity, nourishment (mission-aligned)
  ✓ Harvest signals "outcomes produced" (not stasis)
  ✓ Universally positive symbol (food, abundance)

Narrative arc: "Plant the seeds, grow them, nurture growth, reap rewards"
Complete, coherent, and mission-aligned.

Color change:
  Old: #C4956A (soft gold — can feel "aloof" or "exclusive")
  New: #D97E3E (warm harvest orange — productive, inviting, abundant)
```

**Visual comparison in phase header:**

```
BEFORE                          AFTER

Wave 1: Establish               Wave 1: Establish
🌱 Green                        🌱 Green
────────────────                ────────────────

Wave 2: Expand                  Wave 2: Expand
🌿 Teal                         🌿 Teal
────────────────                ────────────────

Wave 3: Optimize                Wave 3: Optimize
🌳 Brown                        🌳 Brown
────────────────                ────────────────

Wave 4: Harvest                 Wave 4: Harvest & Propagate
🏛 Gold                         🌾 Orange
(feels institutional)           (feels productive)
```

---

### FIX #3: Seed Dispersal Dots → Single Arrow

#### BEFORE (Decorative, Unclear)
```
Vine connector between phases:

           ↘ ↙ ↗
Wave 1 ───( ○ )─── Wave 2 ───( ○ )─── Wave 3
      vine ↓ ↑      vine
           ↗ ↙ ↘

Three circles with varying opacity
  • Position: (6,6), (20,3), (34,8) — scattered vertically
  • Opacity: 0.6, 0.4, 0.6 — varied fading
  • Fill colors: mix of previous + current phase colors

Problem:
  ❌ What do they represent?
    - Seeds? (realistic seed dispersal would be many)
    - Pollen? (but no pollinator shown)
    - Temporal markers? (position doesn't suggest time)
    - Just visual scatter? (decorative)
  ❌ Users don't understand the metaphor
  ❌ Adds visual complexity without meaning
  ❌ On mobile, might look like activity badges/errors
```

#### AFTER (Clear Progression Signal)
```
Vine connector between phases:

Wave 1 ─────→ Wave 2 ─────→ Wave 3 ─────→ Wave 4
      vine    vine    vine
      (gradient coloring)

Single arrow marker at right side of vine
  • Clear meaning: "progression flows this direction"
  • Universally understood (arrow = direction)
  • Matches reading order (left-to-right)
  • Reduces visual clutter
  • Same gradient coloring (previous phase → current phase)

Benefit:
  ✓ Semantically clear (arrow = flow, progression)
  ✓ Less visual noise
  ✓ Scales better to mobile
  ✓ Easier to explain to users
  ✓ If tooltip added: "Propagation energy: Wave N outcomes seed Wave N+1"
```

**Mobile rendering:**

```
BEFORE (cramped)              AFTER (cleaner)

Wave 1 ┏━━━━━━━━━━┓           Wave 1 ──→ Wave 2
       ┃ (●●●) ↓  ┃                  ↓
       Wave 2 ━━━━━            Wave 2 ──→ Wave 3
       ┃ (●●●) ↓  ┃                  ↓
       Wave 3 ━━━━━            Wave 3 ──→ Wave 4
       ┃ (●●●) ↓  ┃
       Wave 4 ┗━━━━━

Dots create visual                Arrows guide eye
clutter on small screens          clearly through flow
```

---

### FIX #4: Phase State Selector (New)

#### BEFORE (No Pause/Failure Options)
```
All phases flow forward monotonically:

Wave 1 ───→ Wave 2 ───→ Wave 3 ───→ Wave 4
(active)   (active)   (active)   (active)

Problem:
  ❌ What if Wave 2 is blocked waiting for Wave 1 completion?
  ❌ What if Wave 3 fails and is abandoned?
  ❌ What if Wave 2 is paused, waiting for funding?

UI has no way to express realistic scenarios:
  • Dormant (paused, will resume)
  • Failed (abandoned, won't proceed)
  • Waiting (blocked on upstream phase)

Result: Users forced to delete phases or leave misleading "In Progress" status
```

#### AFTER (Realistic State Tracking)
```
Phases can have multiple states:

Wave 1 ───→ Wave 2 ───→ Wave 3 ───→ Wave 4
 ✓          ⏸          ✗          ○
Complete   Paused    Abandoned   Not Started

State options per phase:
┌─────────────────────────────────┐
│ Phase Status: ▼                  │
│  ○ In Progress                   │
│  ✓ Complete                      │
│  ⏸ Paused (waiting on resources) │
│  ✗ Discontinued (no Wave 4)      │
└─────────────────────────────────┘

Visual rendering by state:

  ACTIVE          COMPLETE        PAUSED            DISCONTINUED
  ┌─────┐        ┌─────┐        ┌─────┐ (50%)    ┌─────┐ (70%)
  │ 🌱  │        │ 🌱  │        │ 🌱  │         │ 🌱  │
  │Wave1│ ✓      │Wave1│ ✓      │Wave2│ ⏸       │Wave3│ ✗
  │85%  │        │100% │        │50%  │         │0%   │
  └─────┘        └─────┘ Color  └─────┘ Gray    └─────┘ Red-brown
                 Full   Maintained Light/Muted   Muted

Benefit:
  ✓ Realistic initiative tracking
  ✓ Honors botany (dormancy, senescence are natural)
  ✓ Better Goodwill alignment (not all initiatives succeed)
  ✓ Allows paused initiatives to resume later
  ✓ Doesn't force deletion of "failed" phases
```

---

## MEDIUM-PRIORITY ENHANCEMENTS

---

### ENHANCEMENT #1: Phase Duration/Timeline

#### BEFORE (Hidden)
```
Wave 1: Establish [5 plans] [85% health]
Wave 2: Expand    [3 plans] [72% health]
Wave 3: Optimize  [2 plans] [60% health]

Problem:
  ❌ No indication of WHEN each phase is scheduled
  ❌ User doesn't know if phases are concurrent or sequential
  ❌ Can't plan resources (is Wave 2 overlapping Wave 1?)
  ❌ Nonprofit users expect fiscal/grant year clarity
```

#### AFTER (Timeline Explicit)
```
Wave 1: Establish [Q1: Jan–Mar] [5 plans] [85% health]
Wave 2: Expand    [Q2: Apr–Jun] [3 plans] [72% health]
Wave 3: Optimize  [Q3: Jul–Sep] [2 plans] [60% health]
Wave 4: Harvest   [Q4: Oct–Dec] [1 plan]  [50% health]

Benefit:
  ✓ Temporal context visible
  ✓ Shows calendar quarters (relevant for nonprofits)
  ✓ Helps plan resource allocation
  ✓ Aligns with Goodwill's operational cycles
  ✓ If set, shows expected duration
```

---

### ENHANCEMENT #2: Improved Phase Descriptions

#### BEFORE (Generic)
```
Wave 1: "Initial planting — foundational work"
Wave 2: "New growth from first harvest"
Wave 3: "Mature ecosystem expansion"
Wave 4: "Legacy and sustained impact"

Problem:
  ⚠ Narrative jumps around (foundational → harvest skips growth)
  ⚠ "Mature ecosystem expansion" is vague
  ⚠ "Legacy and sustained impact" doesn't describe the phase
  ⚠ No action-oriented language
```

#### AFTER (Narrative Arc)
```
Wave 1: "Establish core foundations and systems"
        → (What you're doing: building infrastructure)

Wave 2: "Expand impact; deploy beyond initial pilot"
        → (What you're doing: spreading to new areas/teams)

Wave 3: "Optimize; refine based on real-world feedback"
        → (What you're doing: improving from live data)

Wave 4: "Harvest & Propagate; institutionalize gains"
        → (What you're doing: lock in benefits; prepare for next cycle)

Benefit:
  ✓ Clear story: Establish → Expand → Optimize → Harvest → Propagate
  ✓ Action-oriented (helps teams understand what to do)
  ✓ Mission-aligned (harvest = fruits of labor, for community benefit)
  ✓ Botanical coherence (complete cycle from seed to seed)
```

---

### ENHANCEMENT #3: Vine Tooltip

#### BEFORE (No Explanation)
```
Wave 1 ──[three dots]──→ Wave 2

User hovers and... nothing appears. What are the dots?
```

#### AFTER (Tooltip on Hover)
```
Wave 1 ──[arrow]──→ Wave 2
        ^ hover here

Tooltip appears:
┌────────────────────────────────────────┐
│ Propagation energy: Outcomes from Wave 1│
│ seed Wave 2 work. Preceding phase       │
│ completion enables the next phase.      │
└────────────────────────────────────────┘

Benefit:
  ✓ Explains the metaphor without cluttering UI
  ✓ Educational (users learn the botanical model)
  ✓ Optional (doesn't intrude if user doesn't hover)
```

---

## SUMMARY TABLE: BEFORE VS. AFTER

| Aspect | Before | After | Improvement |
|--------|--------|-------|-------------|
| **Terminology** | "Season" (6 mentions) | "Wave" (6 mentions) | Removes calendar confusion; fits nonprofit language |
| **Phase 4 Icon** | 🏛 (monument) | 🌾 (grain) | Completes botanical narrative; aligns with mission |
| **Phase 4 Color** | #C4956A (gold/aloof) | #D97E3E (harvest orange/warm) | More inviting; better signals "productivity" |
| **Vine Dots** | ○○○ (three, unclear) | → (single arrow) | Clearer progression signal; less visual noise |
| **Phase States** | None (only active/inactive) | 4 states: active, complete, paused, discontinued | Realistic tracking; honors natural cycles |
| **Timeline** | Hidden (no dates shown) | Visible (Q1–Q4 if set) | Transparent planning; nonprofit-relevant |
| **Phase Descriptions** | Generic, narrative jumps | Narrative arc (Establish → Harvest) | Clear story; action-oriented; mission-aligned |
| **Overall Clarity** | Good (7.5/10) | Excellent (8.0–8.5/10) | +0.5–1.0 point improvement |

---

## IMPACT ASSESSMENT

### What Changes for Users

**Visual:**
- ✓ Phase labels now say "Wave 1" instead of "First Season"
- ✓ Phase 4 shows grain icon instead of building icon
- ✓ Phase 4 header is warmer orange color
- ✓ Vine connectors between phases show arrow instead of dots
- ✓ Phase header includes start/end date if set

**Functional:**
- ✓ New dropdown in phase header: select phase state (paused/discontinued)
- ✓ Paused phases show faded visually (50% opacity, gray color)
- ✓ Discontinued phases show with strikethrough or X icon (red-brown color)
- ✓ Tooltip on vine explains "propagation energy" concept

**Conceptual:**
- ✓ Users understand phases as abstract "waves," not calendar-tied
- ✓ Users see phase progression as a complete cycle (seed to harvest to propagation)
- ✓ Users can pause initiatives without deletion
- ✓ Users see when they should expect each phase (Q1–Q4)

---

## IMPLEMENTATION SEQUENCE

**Step 1 (30 min):** Rename "Season" → "Wave" globally
  → Update SEASON_META constant
  → Update UI labels
  → Verify all references changed

**Step 2 (15 min):** Update Phase 4 icon and color
  → 🏛 → 🌾
  → #C4956A → #D97E3E
  → Verify color contrast (WCAG AA)

**Step 3 (30 min):** Simplify vine visual
  → Remove three dots
  → Add arrow marker
  → Test on mobile

**Step 4 (1 hour):** Add phase state selector
  → Add dropdown to phase header
  → Update visual rendering per state
  → Test state persistence in data

**Step 5 (1 hour, optional):** Add timeline/duration
  → Display start/end date in phase header
  → Calculate and show Q1–Q4 labels
  → Ensure mobile layout handles dates

**Total time: 2 hours 45 minutes (critical) + 1 hour (enhancement)**

---

## Testing Verification

**Visual:**
- [ ] All "Season" labels changed to "Wave"
- [ ] Phase 4 shows 🌾 icon in all views
- [ ] Phase 4 color is #D97E3E (harvest orange)
- [ ] Vine shows arrow, not dots
- [ ] Phases stack cleanly on mobile

**Functional:**
- [ ] Phase state dropdown works
- [ ] Paused state shows faded visual
- [ ] Discontinued state shows red-brown with X icon
- [ ] State changes persist in data

**Compatibility:**
- [ ] All existing 1-phase objectives display correctly
- [ ] Multi-phase objectives display correctly (2–4 phases)
- [ ] Dependency tracking still works
- [ ] Health bar calculations unchanged
- [ ] Plan counts per phase correct

---

## Botanical Coherence Score

| Aspect | Before | After |
|--------|--------|-------|
| Visual metaphor | 7.5/10 | 8.5/10 |
| Terminology clarity | 5.5/10 | 8.0/10 |
| Realism (dormancy/failure) | 5.5/10 | 8.0/10 |
| Narrative arc | 6.0/10 | 8.5/10 |
| Mission alignment | 7.5/10 | 8.5/10 |
| **OVERALL** | **6.5–7.5/10** | **8.0–8.5/10** |

**Estimated improvement: +1.0–1.5 points**

---
