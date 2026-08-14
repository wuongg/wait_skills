---
name: multi-page-integration
description: >
  Contract that connects the Design Constitution to every page builder
  that is NOT the cinematic landing builder. Defines the Page Spec JSON
  schema (the app-side sibling of the landing Build Spec), downgrade
  rules from cinematic to quiet mode, cross-page consistency checks
  (chrome, nav, auth state, breadcrumbs), and the handoff protocol when
  a user asks for "thêm trang quản lý / trang settings / trang docs"
  after a landing exists. Read before building ANY non-landing page.
license: MIT
version: 1.0
compatible_with:
  - product-design-constitution >=1.0
  - page-types-catalog >=1.0
  - landing-page-skills-integration >=1.0
---

# Multi-Page Integration Contract v1

## The pipeline, extended

```
                         ┌────────────────────────────────────┐
                         │  LANDING SIDE (already exists)     │
                         │  planner → contract → cinematic     │
                         │  builder → landing page             │
                         └──────────────┬─────────────────────┘
                                        │ extract DNA
                                        ▼
                         [ product-design-constitution ]
                                        │ emits
                                        ▼
                     Constitution (tokens.json, locked)
                                        │
        ┌───────────────┬───────────────┼───────────────┬──────────────┐
        ▼               ▼               ▼               ▼              ▼
   [T-01/02/03]    [T-04/05]       [T-06/08]       [T-07]        [T-09..T-12]
   data pages      form/auth       settings/       docs          states
                                   billing
```

**Golden rule (extended).**
- Planner owns landing structure.
- Cinematic builder owns landing surface.
- **Constitution owns product DNA.**
- Page builders own page function — never DNA.

---

## 1. PAGE SPEC — the app-side sibling of Build Spec

Before building any T-01..T-12 page, the builder emits a Page Spec:

```json
{
  "page_spec_version": "1.0",
  "constitution_ref": {"version": "1.0", "locked": true},
  "page_type": "T-01",
  "page_type_name": "Dashboard",
  "cinematic_budget": 10,
  "shell": "sidebar shell",
  "content": [
    {"region": "header",  "pattern": "page title + primary action", "tokens": ["type.scale.lg", "color.brand.primary"]},
    {"region": "metrics", "pattern": "metric band", "items": 4},
    {"region": "main",    "pattern": "data table", "features": ["sort","filter","paginate"]},
    {"region": "side",    "pattern": "chart panel", "chart": "line"}
  ],
  "tokens_used": ["color.surface.canvas", "color.text.primary", "type.families.body", "shape.radius.md"],
  "budget_spend": [
    {"element": "metric delta color shift", "cost": 4},
    {"element": "hover lift on cards", "cost": 3}
  ],
  "budget_total": 7,
  "acceptance_criteria": [
    "Every token resolves to constitution tokens.json",
    "budget_total <= cinematic_budget",
    "No kill-list item from page-types-catalog T-01 present",
    "Chrome matches §3 of this contract"
  ]
}
```

**Invariants.**
- `budget_total` ≤ `cinematic_budget` (from `page-types-catalog`). Over = fail.
- Every value in `tokens_used` MUST resolve in `tokens.json`. A token
  that doesn't exist = the builder is inventing DNA = hard fail.
- `content[].pattern` ∈ the page type's allowed layout patterns.
  Anything else = hard fail.

---

## 2. DOWNGRADE RULES (cinematic → quiet)

Applied automatically when translating any landing-flavored request into
an app page. (Mirrors the Constitution's Downgrade Matrix; this is the
builder-side enforcement.)

| If the user/builder proposes… | Rule | Enforced as |
|---|---|---|
| Display type > `app_max` | D1 | Cap at constitution `type.rules.app_max` |
| Motion duration > page budget allows | D2 | Cap at `motion.rules.app_cap` (300ms) |
| Full-bleed media | D3 | Contain within `surface.raised` panel |
| Custom easing curves | D4 | Replace with `motion.easings.enter/exit` |
| Colors outside tokens | D5 | Map to nearest token, log the distance |
| New radius personality | D6 | Snap to constitution `shape.radius` scale |
| Effects (grain, glow, blur wash) | D7 | Remove; log as amendment candidate |
| Marketing voice in app copy | D8 | Rewrite to plain, factual voice |

**D-Log.** Every D1–D8 enforcement is logged in the Page Spec as
`downgrades_applied[]`. If the same downgrade fires on 3+ pages, the
Constitution SHOULD receive an amendment proposal — the product is
telling you its DNA is wrong, not its pages.

---

## 3. CROSS-PAGE CONSISTENCY (the Chrome Contract)

Every non-landing page in the product MUST share:

### Chrome anatomy
- **Nav position:** one choice per product (sidebar OR topbar), applied
  to T-01..T-12 uniformly.
- **Logo:** same slot, same size, links to the same home route.
- **User menu / avatar:** always top-right.
- **Breadcrumbs:** required on T-03; optional T-01/T-02; absent T-04..T-05.
- **Page title:** always `type.scale.lg`, always top-left of content region.
- **Primary action:** top-right of content region, `color.brand.primary`,
  max ONE per page.

### Auth-state continuity
- Logged-out → landing chrome.
- Logged-in → app chrome.
- The TRANSITION (login screen → first dashboard) is the highest-risk
  brand-continuity moment. Rule: auth page (T-05) uses landing's
  surface tokens on its brand panel, so the handoff feels continuous.

### Voice continuity test
Read aloud, in order: landing H1 → dashboard title → settings section
title → error headline. If any one sounds like a different writer, fail.

### Dark/light continuity
- If landing is dark and app is light (common and legitimate), the
  Constitution MUST define both `surface.canvas` values explicitly, and
  ALL other tokens must be chosen to work on both. No silent flips.

---

## 4. VALIDATION GATE (app side)

Run before code on every non-landing page. All must pass:

- [ ] `constitution_ref.locked === true` and version is current.
- [ ] `page_type` ∈ `page-types-catalog`.
- [ ] Every `content[].pattern` ∈ that type's allowed patterns.
- [ ] `budget_total <= cinematic_budget`.
- [ ] Every `tokens_used` entry resolves in `tokens.json`.
- [ ] No kill-list item present (from that type's `page-types-catalog` entry).
- [ ] Chrome Contract §3 satisfied (nav, logo, avatar, title, action).
- [ ] Motion durations ≤ `motion.rules.app_cap` (or page budget if lower).
- [ ] Voice continuity test passed.
- [ ] `prefers-reduced-motion` honored.

Fail → fix the Page Spec. If the fix requires a token that doesn't
exist → emit an **amendment proposal** to the Constitution (never invent
the token locally).

---

## 5. AMENDMENT PROTOCOL (builder → constitution)

```json
{
  "amendment_proposal": {
    "token": "color.brand.tertiary",
    "proposed_value": "#…",
    "rationale": "3 report pages need a second data-diverging hue",
    "page_types_benefiting": ["T-10", "T-01"],
    "sameness_test": "re-run with new token — PASS/FAIL + note"
  }
}
```

The Constitution skill re-issues a new version (1.0 → 1.1). Builders
pin to a version; migrations are explicit, never ambient.

---

## 6. HANDOFF SCRIPTS

**User asks for a dashboard after landing exists:**
> "Landing đã có DNA rồi. Mình extract Constitution trước (1 lượt), rồi
> build dashboard theo T-01 với budget 10%. Đồng ý không?"

**User asks for a page with no Constitution yet:**
> "Chưa có Constitution — nếu build trang quản lý bây giờ sẽ lệch DNA
> với landing. Cho mình 1 lượt để extract trước."

**User demands cinematic dashboard:**
> "Dashboard budget là 10% — vượt mức này user sẽ ghét sau tuần đầu dùng.
> Mình có thể đưa drama vào đúng 1 chỗ: màn onboarding (T-09, budget 30%)
> hoặc empty state đầu tiên. Chọn chỗ để 'đẹp' nhé."

---

## 7. ANTI-PATTERNS (both sides refuse)

- ❌ Building an app page from the landing's Build Spec instead of a
  Page Spec (wrong artifact, wrong contract).
- ❌ "Clone landing hero vào dashboard cho đồng bộ." → Sameness comes
  from tokens, never from transplanted sections.
- ❌ Per-page color overrides ("trang này hồng nhẹ cho nữ tính").
- ❌ Two nav paradigms in one product (sidebar on dashboard, topbar on
  settings).
- ❌ Skipping the Constitution because "trang này nhỏ thôi".
  Small pages are where inconsistency starts.

---

**End of contract.**
