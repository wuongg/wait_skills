---
name: landing-page-skills-integration
description: >
  Handoff contract between `landing-page-composition-architect` (planner) and
  `cinematic-landing-page` (builder). Defines the Blueprint JSON schema, the
  layout-family → visual-archetype mapping, the invariants the builder must
  preserve, and the failure modes both sides must refuse. Read this whenever
  a Composition Blueprint is being handed off, or whenever the builder is
  about to code a page without a locked blueprint.
license: MIT
version: 1.0
---

# Landing Page Skills — Integration Contract v1

Two skills, one pipeline:

```
User brief
   │
   ▼
[ landing-page-composition-architect ]   ← decides WHAT & ORDER
   │  emits: Composition Blueprint (locked)
   ▼
[ INTEGRATION.md  ← this file ]          ← translates blueprint → build spec
   │  emits: Build Spec (archetype + motion + stack)
   ▼
[ cinematic-landing-page ]               ← decides HOW IT LOOKS & MOVES, writes code
   │
   ▼
Shipped page
```

**Golden rule.** The planner owns *structure*. The builder owns *surface*.
Neither may cross the line. This file is how they stay honest.

---

## 1. THE HANDOFF ARTIFACT — Composition Blueprint (JSON)

The planner's final artifact MUST be renderable as this JSON, even if it
was presented to the user as a table. The builder reads this JSON verbatim.

```json
{
  "blueprint_version": "1.0",
  "page": {
    "intent": "I1 | I2 | I3 | I4 | I5 | I6",
    "intent_name": "Launch | Conversion | Brand | Portfolio | Product Story | Campaign",
    "awareness": "cold | warm | hot",
    "traffic": "ads | organic | social | referral | direct",
    "narrative_spine": "Hook -> Value -> Proof -> CTA",
    "pace": "fast | balanced | slow-burn",
    "density": "minimal | balanced | rich",
    "primary_emotion": "string (one word)",
    "total_sections": 5
  },
  "sections": [
    {
      "index": 1,
      "slot": "S1",
      "name": "Hero",
      "jtbd": "grab attention + set tone",
      "why_here": "first impression",
      "layout_family": "full-bleed hero",
      "content_required": ["headline", "subcopy", "hero_media"],
      "visual_weight": "very high",
      "cta_role": "soft"
    }
  ],
  "rhythm_rules": [
    "No two 'very high' weight sections adjacent.",
    "After any full-bleed hero or mood gallery, next must be centered statement or editorial block.",
    "Primary CTA appears exactly once."
  ],
  "kill_list": [
    "No FAQ",
    "No 6-card feature grid",
    "No metric band"
  ],
  "handoff_note": "One paragraph: emotion to preserve, which slots want cinematic treatment, which stay quiet.",
  "locked": true
}
```

**Invariants.**

- `sections.length` ∈ [4, 9]; 5–8 for standard intents.
- Every `slot` ∈ `{S1..S16}`, unique per page.
- `layout_family` ∈ closed list (see §3).
- `locked: true` is a promise: builder MUST NOT reorder, add, drop, or
  rename sections.

---

## 2. WHAT THE BUILDER MAY DECIDE (and what it may NOT)

### Builder may decide
- Cinematic archetype (A/B/C/D/E/F from `cinematic-landing-page`).
- Motion signatures, easing curves, scroll behavior.
- Color mood, typography, spacing scale.
- Media treatment (grain, blur, framing, cutouts).
- Tech stack (V1 vanilla vs V2 React+Vite+Tailwind).
- Micro-copy polish (as long as intent-preserving).

### Builder may NOT decide
- Section count.
- Section order.
- Which slot maps to which position.
- Whether a section exists at all.
- Renaming a slot's *purpose* (user-facing name can change; JTBD cannot).
- Adding sections not in the blueprint (no surprise CTA banner, no
  surprise newsletter block).
- Removing the primary CTA or duplicating it.

If the builder feels the blueprint is wrong, it must **stop and request a
re-plan**, not silently mutate.

---

## 3. LAYOUT FAMILY → VISUAL ARCHETYPE MAPPING

The planner speaks in layout families. The builder speaks in cinematic
archetypes (A–F). This is the translation table.

| Layout family (planner) | Primary archetype (builder) | Fallback | Notes |
|---|---|---|---|
| `full-bleed hero` | A (Fixed-Viewport Hero) | B | Framed-canvas variant if mood = premium |
| `split hero` | A (pattern: split) | D | Left copy / right media |
| `centered statement` | D section OR A (centered) | — | Low motion, high readability |
| `benefit rail` | D card row | — | 3–4 items, no cards heavier than icon+title+line |
| `card grid` | D grid | — | Max 6 tiles; disable hover motion in I3 |
| `staggered stack` | D asymmetric section | B | Alternating image/text rows |
| `editorial block` | D editorial | F (if display type) | Long-form; avoid card UI |
| `mood gallery` | B (sticky scroll) or E (switcher) | — | Pick by pace: slow-burn→B, balanced→E |
| `logo strip` | D quiet row | — | No motion beyond marquee if requested |
| `metric band` | D big-number row | — | Count-up animation only if pace ≠ slow-burn |
| `quote panel` | D or A single-scene | — | One pull-quote > carousel |
| `accordion list` | D accordion | — | Banned for I3 (see kill list) |
| `CTA band` | D centered CTA | A | Primary CTA lives here |
| `sticky footer CTA` | D sticky footer | — | Only if pace = fast |
| `soft footer` | D minimal footer | — | End-of-page quiet exit |

**Archetype-per-page cap.**
- Max **2 signature archetypes** per page (inherited from
  `cinematic-landing-page` rule).
- The hero section chooses the *dominant* archetype. Other sections
  default to D-style execution unless the planner's `handoff_note`
  explicitly requests cinematic treatment for them.

**Intent-based archetype defaults** (when planner didn't hint):

| Intent | Dominant archetype | Second archetype (optional) |
|---|---|---|
| I1 Launch | A | E |
| I2 Conversion | A (split) | — (stay quiet) |
| I3 Brand Editorial | F or B | E |
| I4 Portfolio | F or C | B |
| I5 Product Story | A + B (scroll story) | — |
| I6 Campaign / Teaser | A or F | — |

---

## 4. BUILD SPEC — the artifact the builder emits before coding

Before writing a single line of code, the builder MUST produce a Build Spec
derived from the Blueprint. This is the second contract in the pipeline.

```json
{
  "build_spec_version": "1.0",
  "blueprint_ref": "locked",
  "stack": "V1 vanilla | V2 react-vite-tailwind",
  "dominant_archetype": "A | B | C | D | E | F",
  "second_archetype": "A | B | C | D | E | F | null",
  "mood": "Dark Cinematic | Warm Editorial | Neo-Tech | Light Minimal | Light Editorial | Soft Glass",
  "sections": [
    {
      "index": 1,
      "slot": "S1",
      "layout_family": "full-bleed hero",
      "archetype": "A",
      "pattern": "framed-canvas",
      "motion": ["hero_fade_in_800ms", "subcopy_delay_200ms"],
      "media": {"type": "image | video | none", "asset_ref": "…"},
      "notes": "why this archetype was chosen for this slot"
    }
  ],
  "acceptance_criteria": [
    "First viewport = S1 composition only.",
    "Primary CTA in S15 exactly once.",
    "No adjacent 'very high' weight sections.",
    "Motion count on page <= 2 signatures."
  ]
}
```

The builder validates the Build Spec against the Blueprint (see §6) BEFORE
coding. Fail closed.

---

## 5. TRANSLATION RULES (planner → builder)

Applied in order.

**T1. Section order is law.** `sections[i].index` in blueprint = position on
page. Builder never reorders.

**T2. Slot → archetype eligibility.** Use §3 table. If a layout family
appears whose primary archetype conflicts with the dominant archetype
already chosen for the hero, use the fallback.

**T3. Weight → motion budget.**

| Visual weight | Motion budget |
|---|---|
| very high | up to 2 signature interactions |
| high | 1 signature interaction |
| medium | micro-interactions only (hover, small fades) |
| low | fades only |
| very low | static |

**T4. CTA role → surface treatment.**

| CTA role | Treatment |
|---|---|
| primary | full button + form/anchor, high contrast |
| hard | button, high contrast, no form |
| soft | text link with arrow |
| none | no CTA element rendered |

**T5. Emotion → mood mapping** (advisory).

| primary_emotion (planner) | Suggested mood (builder) |
|---|---|
| reverence, calm, luxury | Dark Cinematic / Soft Glass |
| clarity, trust, precision | Light Minimal / Neo-Tech |
| warmth, human, story | Warm Editorial / Light Editorial |
| energy, urgency, hype | Neo-Tech / Dark Cinematic |

**T6. Pace → scroll length.**

| Pace | Total scroll (desktop) |
|---|---|
| fast | ≤ 2.5 viewports |
| balanced | 3–5 viewports |
| slow-burn | 5–8 viewports |

**T7. Density → component choice.**

- minimal → prefer type-only sections, wide whitespace.
- balanced → mixed type + media.
- rich → editorial-block heavy; still respect kill list.

**T8. Kill list is absolute.** Anything in `kill_list` is banned in the
Build Spec and the code, even if it would "look cool".

---

## 6. VALIDATION GATE (run before any code is written)

The builder runs this checklist against the Build Spec. All must pass.

- [ ] Every blueprint section has exactly one row in `build_spec.sections`.
- [ ] `index` values are consecutive, starting at 1.
- [ ] No section added, removed, reordered, or merged.
- [ ] `layout_family` per row matches blueprint.
- [ ] Dominant archetype is used by the hero (`index: 1`).
- [ ] Total signature archetypes on page ≤ 2.
- [ ] Sum of "signature interactions" across sections ≤ 2.
- [ ] Primary CTA count = 1 (or 0 iff intent = I3 with soft-footer close).
- [ ] No item from `kill_list` is present in the spec.
- [ ] Awareness gate honored: cold ⇒ S2 exists right after S1.
- [ ] No forbidden adjacency (S6+S9, S11+S13, etc.).

Fail → return to planner with a `revision_request` (see §7). Do NOT code
around a failed gate.

---

## 7. REVISION PROTOCOL

If the builder must push back, it emits a structured request, not free text:

```json
{
  "revision_request": {
    "reason": "layout_conflict | asset_missing | motion_budget_exceeded | kill_list_impossible | adjacency_violation",
    "affected_sections": [3, 4],
    "explanation": "one short paragraph",
    "suggested_fix": "swap S6 and S9 order | drop S13 | downgrade S1 weight to high"
  }
}
```

Planner responds with a **new locked blueprint**, not a patch note.
Blueprints are re-issued whole, versioned by `blueprint_version` bump.

---

## 8. FAILURE MODES BOTH SIDES MUST REFUSE

**Planner must refuse to:**
- Emit an unlocked blueprint.
- Emit fewer than 4 or more than 9 sections.
- Include a slot with `content_required` the user cannot supply.
- Reuse a slot ID.
- Skip S1 or (usually) S15.
- Choose a layout family outside the closed list in §3.

**Builder must refuse to:**
- Code without a locked blueprint.
- Code without a Build Spec that passed §6.
- Add a section "because the page felt empty".
- Drop a section "because it felt redundant".
- Use more than 2 signature archetypes.
- Ignore the kill list.
- Silently downgrade `primary` CTA to `soft`.

If a user directly requests a violation, respond once with the trade-off,
then only comply if they explicitly confirm — and record it in the Build
Spec as `"user_override": true` on the affected row.

---

## 9. MINIMAL END-TO-END EXAMPLE

### Blueprint (planner output, condensed)

- Intent: I2 Conversion, cold, ads, balanced pace, balanced density.
- Sections: `S1 → S2 → S4 → S5 → S6 → S12 → S13 → S15`
- Kill list: no S8, no S9, no S14, no S11.
- Primary emotion: clarity.

### Build Spec (builder output, condensed)

- Stack: V2 (React + Vite + Tailwind + framer-motion).
- Dominant archetype: **A (split hero)**. Second archetype: none.
- Mood: Light Minimal.
- Motion budget used: 2 / 2 (hero split reveal + metric count-up).
- S1 = A split hero. S2 = D centered statement. S4 = D editorial block.
  S5 = D staggered stack. S6 = D card grid (4 tiles). S12 = D metric band.
  S13 = D quote panel (single pull-quote). S15 = D CTA band with form.
- Acceptance: primary CTA once (S15); no S6/S9 adjacency; total scroll
  ≈ 4 viewports.

### Validation

All §6 checks pass. Builder proceeds to code.

---

## 10. WHAT TO TELL THE USER (script snippets)

**When handing off from planner:**
> "Blueprint đã khóa. Chuyển sang skill build (`cinematic-landing-page`)?
> Skill đó sẽ chọn archetype visual + motion + code, không đổi thứ tự
> section."

**When builder rejects a blueprint:**
> "Blueprint này có xung đột ở section {n} — {lý do}. Mình gửi lại planner
> để phát hành bản mới, thay vì tự sửa."

**When user pushes for override:**
> "Nếu ép làm vậy, mình sẽ đánh dấu `user_override: true` ở section đó.
> Trang vẫn build được, nhưng rhythm rule bị phá — bạn xác nhận?"

---

**End of integration contract.**
