# ImpactQ v4.3 Phase/Season System
## Quick Implementation Guide

**Panel Review Date:** March 27, 2026
**Overall Score:** 7.5/10 (Botanically Coherent)
**Time to Fix (High-Priority Items):** 2–3 hours

---

## THE FOUR CRITICAL FIXES

### FIX #1: Rename "Season" → "Wave" (30 minutes)

**Problem:** "Season" implies calendar-driven phenology; phases are abstract cycles.

**Files:** `/sessions/brave-stoic-shannon/mnt/AI/impactq/index.html` (lines 267–272)

**Current Code:**
```javascript
const SEASON_META = {
  1: { label: 'First Season', icon: '🌱', desc: 'Initial planting — foundational work', color: '#5A8F5A' },
  2: { label: 'Second Season', icon: '🌿', desc: 'New growth from first harvest', color: '#2A6B6B' },
  3: { label: 'Third Season', icon: '🌳', desc: 'Mature ecosystem expansion', color: '#8B7355' },
  4: { label: 'Fourth Season', icon: '🏛', desc: 'Legacy and sustained impact', color: '#C4956A' }
};
```

**Change To:**
```javascript
const SEASON_META = {
  1: { label: 'Wave 1', icon: '🌱', desc: 'Establish core foundations and systems', color: '#5A8F5A' },
  2: { label: 'Wave 2', icon: '🌿', desc: 'Expand impact; deploy beyond initial pilot', color: '#2A6B6B' },
  3: { label: 'Wave 3', icon: '🌳', desc: 'Optimize; refine based on real-world feedback', color: '#8B7355' },
  4: { label: 'Wave 4', icon: '🌾', desc: 'Harvest & Propagate; institutionalize gains', color: '#D97E3E' }
};
```

**Additional locations to update:**
- Line 867: `<label style={{...}}>Wave (Phase)</label>`
- Line 890: `{getSeasonMeta(phase - 1).label} outcomes` → `{getSeasonMeta(phase - 1).label} completion`

---

### FIX #2: Replace Phase 4 Icon (15 minutes)

**Problem:** 🏛 (monument) breaks botanical metaphor; suggests stasis not growth.

**Solution:** Use 🌾 (grain/harvest) — signals maturity, productivity, and mission alignment.

**Files:** `/sessions/brave-stoic-shannon/mnt/AI/impactq/index.html` (line 272, color line 268)

**Change:**
```javascript
// Old:
4: { label: 'Fourth Season', icon: '🏛', desc: '...', color: '#C4956A' }

// New:
4: { label: 'Wave 4', icon: '🌾', desc: 'Harvest & Propagate; institutionalize gains', color: '#D97E3E' }
```

**Why #D97E3E (harvest orange) instead of #C4956A (gold):**
- Better "harvest" signal (warm, productive, not "trophy")
- Avoids "exclusive/elite" connotations (fits nonprofit culture)
- Maintains contrast with text for accessibility

---

### FIX #3: Add Phase State Selector (1 hour)

**Problem:** No way to express paused or failed phases; forces linear progression.

**Files:** `/sessions/brave-stoic-shannon/mnt/AI/impactq/index.html` (lines 2830–2860, phase header rendering)

**Current Phase Header:**
```jsx
<div style={{display: 'flex', alignItems: 'center', gap: '12px', ...}}>
  <StageIcon status={...} />
  <div>{sm.label} | {phasePlans.length} plans | {health}% health</div>
</div>
```

**Enhanced Phase Header (add state selector):**
```jsx
<div style={{display: 'flex', alignItems: 'center', gap: '12px', ...}}>
  <StageIcon status={...} />
  <div style={{flex: 1}}>
    <div style={{fontSize: '14px', fontWeight: 600}}>{sm.label}</div>
    <div style={{fontSize: '11px', color: 'var(--text-muted)'}}>
      {sm.desc} | {phasePlans.length} plans | {health}% health
    </div>
  </div>

  {/* NEW: State selector */}
  <select value={phaseState || 'active'} onChange={(e) => setPhaseState(e.target.value)}
    style={{fontSize: '11px', padding: '4px', borderRadius: '4px', border: '1px solid var(--border)'}}>
    <option value="active">In Progress</option>
    <option value="complete">Complete</option>
    <option value="dormant">Paused</option>
    <option value="failed">Discontinued</option>
  </select>
</div>
```

**Data Model Update:**
```javascript
// Add to plan/objective data structure:
phase: { number: 2, state: 'active' | 'complete' | 'dormant' | 'failed' }
```

**Visual States:**
| State | Opacity | Color | Icon |
|-------|---------|-------|------|
| active | 100% | Full | ✓ (normal) |
| complete | 100% | Full | ✓ (full color) |
| dormant | 50% | #D3D0CA (gray) | ⏸ (pause icon) |
| failed | 70% | #8B5A5A (red-brown) | ✗ (X icon) |

---

### FIX #4: Simplify Seed Dots → Single Arrow (30 minutes)

**Problem:** Three dots between phases are decorative, unclear meaning.

**Files:** `/sessions/brave-stoic-shannon/mnt/AI/impactq/index.html` (lines 2776–2791, vine SVG)

**Current SVG (three dots):**
```jsx
<svg width="40" height="24" viewBox="0 0 40 24">
  <linearGradient id={`vine-grad-${ph}`} x1="0" y1="0" x2="1" y2="0">
    <stop offset="0%" stopColor={getSeasonMeta(ph - 1).color} />
    <stop offset="100%" stopColor={sm.color} />
  </linearGradient>
  <path d="M0,12 C10,4 30,20 40,12" stroke={`url(#vine-grad-${ph})`} strokeWidth="2" fill="none" />
  {/* THREE DOTS — REMOVE THESE */}
  <circle cx="6" cy="6" r="2.5" fill={getSeasonMeta(ph - 1).color} opacity="0.6" />
  <circle cx="20" cy="3" r="2" fill={sm.color} opacity="0.4" />
  <circle cx="34" cy="8" r="2.5" fill={sm.color} opacity="0.6" />
</svg>
```

**Simplified SVG (arrow only):**
```jsx
<svg width="40" height="24" viewBox="0 0 40 24">
  <linearGradient id={`vine-grad-${ph}`} x1="0" y1="0" x2="1" y2="0">
    <stop offset="0%" stopColor={getSeasonMeta(ph - 1).color} />
    <stop offset="100%" stopColor={sm.color} />
  </linearGradient>
  {/* Vine line only */}
  <path d="M0,12 C10,4 30,20 40,12" stroke={`url(#vine-grad-${ph})`} strokeWidth="2" fill="none" />

  {/* Single arrow marker (right-pointing) */}
  <polygon points="35,10 40,12 35,14" fill={sm.color} />
</svg>
```

**Optional Tooltip (on hover):**
```jsx
title="Propagation energy: Outcomes from Wave {ph-1} seed Wave {ph}"
```

---

## MEDIUM-PRIORITY ADDITIONS (v4.3.1 or v4.4)

### Add Time/Duration to Phase Headers

**What to show:**
```
Wave 1: Establish [Q1: Jan–Mar] [5 plans] [85% health]
```

**Implementation:**
- Add `phaseStartDate` and `phaseEndDate` to data model
- Calculate Q1–Q4 labels from dates
- Display in phase header (right side, after health %)

**Effort:** 1 hour

---

### Add Vine Tooltip

**Popup on hover:**
```
"Propagation energy: Outcomes from Wave N seed Wave N+1"
```

**Implementation:**
- Add `title` attribute to vine SVG container
- Or use custom tooltip component on hover

**Effort:** 30 minutes

---

### Update Phase Descriptions (Already in Fix #1)

The new descriptions create a narrative arc:
```
Wave 1: Establish core foundations and systems
Wave 2: Expand impact; deploy beyond initial pilot
Wave 3: Optimize; refine based on real-world feedback
Wave 4: Harvest & Propagate; institutionalize gains
```

---

## TESTING CHECKLIST

Before deploying to v4.3.1:

- [ ] Rename all "Season" labels to "Wave" throughout UI
- [ ] Verify SEASON_META constant updated in all references
- [ ] Test Phase 4 icon (🌾) renders in all views (Present, Bloom, Garden)
- [ ] Verify new Phase 4 color (#D97E3E) has sufficient contrast
- [ ] Test phase state dropdown on desktop
- [ ] Test phase state dropdown on mobile (doesn't break layout)
- [ ] Verify vine SVG arrow renders correctly
- [ ] Test horizontal scroll behavior on mobile with 3–4 waves
- [ ] Confirm all phase descriptions match new narrative arc
- [ ] Check that "depends on Wave X" language is updated
- [ ] Smoke test: Create objective with 2+ phases, verify visual rendering

---

## PRIORITY TIMELINE

| Rank | Item | Time | Priority |
|------|------|------|----------|
| 1 | Rename "Season" → "Wave" | 30 min | HIGH |
| 2 | Replace Phase 4 icon + color | 15 min | HIGH |
| 3 | Add phase state selector | 1 hour | HIGH |
| 4 | Simplify seed dots → arrow | 30 min | MEDIUM |
| 5 | Add time/duration to headers | 1 hour | MEDIUM |
| 6 | Add vine tooltip | 30 min | LOW |

**Total for high-priority fixes: 2 hours 15 minutes**
**Total with medium-priority: 3 hours 45 minutes**

---

## SCORE SUMMARY

| Aspect | Before | After | Improvement |
|--------|--------|-------|-------------|
| Terminology clarity | Medium | High | ✓ "Wave" removes calendar confusion |
| Metaphor integrity | Good | Excellent | ✓ Grain icon completes botanical narrative |
| Visual clarity | Good | Better | ✓ Arrow simplifies progression signal |
| Realism | Limited | High | ✓ Phase states allow paused/failed initiatives |
| Overall botanical coherence | 6.5/10 (v4.0) | 7.5/10 (v4.3+) | **+1.0** |

---

**For Questions:** Refer to full expert panel review in `/PHASE-SEASON-EXPERT-REVIEW-3ROUND.md`
