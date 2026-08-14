---
name: page-types-catalog
description: >
  The shared vocabulary for every page type that lives NEXT to a landing
  page: dashboard, list, detail, form, auth, settings, docs, billing,
  onboarding, report, error, empty state. For each type this file locks:
  purpose (how it differs from landing), cinematic budget (0–100%),
  content grammar (required info + order), allowed layout patterns,
  interaction requirements, and a hard kill list. Both the Constitution
  skill and every downstream builder read this file first. Never invent
  a page type outside this catalog without bumping the version.
license: MIT
version: 1.0
compatible_with:
  - landing-page-composition-architect >=1.0
  - landing-page-skills-integration >=1.0
  - product-design-constitution >=1.0
---

# Page Types Catalog v1

## The core idea

A landing page is **a single punch**. Every other page in a product is
**a recurring conversation**. They cannot share style rules — only DNA.

This file defines the 12 page types. Each entry is a contract:

- **Purpose** — why this page exists (and how it differs from landing).
- **Cinematic budget** — 0–100%. The single most important number on
  this page. It caps how much of the landing page's visual drama may
  survive here.
- **Content grammar** — what info MUST appear, in what priority order.
- **Layout patterns** — the closed list of allowed patterns.
- **Interaction requirements** — what MUST be interactive, what MUST NOT.
- **Kill list** — what is banned, no exceptions.

**The Budget Law.** Cinematic budget is not a suggestion. A builder that
exceeds the budget for a page type has failed, regardless of how
beautiful the output is.

---

## T-01 — Dashboard (budget: 10%)

**Purpose.** Repeated operational visits. The user comes to *do* or
*check*, not to feel. Success = time-to-information, not wow.

**Content grammar (priority order).**
1. Page title + primary action (top-right).
2. Key metrics (3–6, scannable in 5s).
3. Primary data view (table / chart / kanban).
4. Secondary panels (activity, alerts, shortcuts).
5. Filters / date range (persistent, visible).

**Allowed layout patterns.**
- `sidebar shell` (fixed nav left, content right)
- `topbar shell` (horizontal nav, content below)
- `metric band` (3–6 KPI cards)
- `data table` (sortable, paginated)
- `chart panel` (one chart per panel)
- `split panel` (list left, detail right)

**Interaction requirements.**
- Every metric: hover = tooltip or drill link.
- Tables: sort, filter, paginate. No infinite scroll for operational data.
- Loading = skeleton, never spinner-only for >1s loads.
- All actions keyboard-reachable.

**Kill list.**
- ❌ Full-bleed hero anything.
- ❌ Scroll-driven animation / parallax.
- ❌ Video backgrounds, kinetic type, cursor effects.
- ❌ Motion > 300ms anywhere.
- ❌ Marketing copy ("Unleash your potential") — dashboard speaks in facts.

---

## T-02 — List / Collection (budget: 10%)

**Purpose.** Browse and pick from many items. Success = findability.

**Content grammar.**
1. Title + count ("42 projects").
2. Primary action ("New project").
3. Filter / sort / search bar.
4. Item list (table OR card list — pick one, never both).
5. Pagination or load-more.
6. Empty state (see T-12).

**Allowed layout patterns.**
- `data table`
- `card list` (horizontal rows, not grid walls)
- `filter rail` (left filters + right results)

**Interaction requirements.**
- Search debounced ≤ 300ms.
- Filter state survives navigation (URL params).
- Bulk actions appear only on selection.

**Kill list.**
- ❌ Masonry / justified galleries (that's mood gallery — landing only).
- ❌ Carousels for operational lists.
- ❌ Hover-only actions on touch-reachable UIs.

---

## T-03 — Detail / Record (budget: 10%)

**Purpose.** Read and act on ONE thing deeply.

**Content grammar.**
1. Breadcrumb / back link.
2. Object title + status badge + primary actions.
3. Core content (the thing itself).
4. Metadata panel (created, owner, tags).
5. Related items (max 1 rail).
6. Activity / history (collapsed by default).

**Allowed layout patterns.**
- `article layout` (centered column, max 720–960px)
- `split panel` (content left, meta right — meta collapses on mobile)
- `tabbed panel` (max 5 tabs; beyond that → split into sub-pages)

**Kill list.**
- ❌ Hero treatment of the record (it's a tool, not a poster).
- ❌ More than 2 primary-styled buttons.
- ❌ Auto-playing media.

---

## T-04 — Form / Multi-step (budget: 5%)

**Purpose.** Get the user from "empty" to "submitted" with minimum
friction. The page is a corridor, not a room.

**Content grammar.**
1. Step indicator (if >1 step) — always visible.
2. One question cluster per screen.
3. Field labels ABOVE inputs (never placeholder-only).
4. Primary action bottom-right ("Continue" / "Submit").
5. Secondary action bottom-left ("Back").
6. Help text inline, not in modals.

**Allowed layout patterns.**
- `centered column` (max 480–560px)
- `field group` (label + input + hint + error slot)
- `stepper` (numbered, non-interactive past steps)

**Interaction requirements.**
- Enter key = next field / submit.
- Errors inline, on blur, human language.
- Never clear entered data on error.
- Autosave for forms > 3 minutes of effort.

**Kill list.**
- ❌ Any animation that delays input (animated field entrances).
- ❌ Dark patterns (pre-checked upsells, hidden decline).
- ❌ Multi-column forms (except first+last name pairs).
- ❌ "Are you sure?" modals for non-destructive submits.

---

## T-05 — Auth (login / register / reset) (budget: 5%)

**Purpose.** Get through the door. The user does not want to be here.

**Content grammar.**
1. Logo (small, top).
2. One headline ("Welcome back" — not a paragraph).
3. Minimal fields (login = 2, register = 3 max, reset = 1).
4. Primary action full-width.
5. One escape link ("Forgot password" / "Create account").
6. Social auth (optional, below divider, max 3 providers).

**Allowed layout patterns.**
- `centered card` (400px, quiet background)
- `split auth` (form left, brand panel right) — brand panel is the ONLY
  place the 5% budget may be spent (1 subtle image/gradient, no motion)

**Kill list.**
- ❌ Marketing carousel inside auth.
- ❌ Video backgrounds behind forms.
- ❌ Password rules revealed only after failure — show them upfront.

---

## T-06 — Settings (budget: 0%)

**Purpose.** Pure utility. The most conservative page in the system.

**Content grammar.**
1. Settings nav (sections list, left or top).
2. Section title + one-line description.
3. Grouped controls (label left, control right).
4. Save behavior is explicit: "Save" button OR auto-save with visible
   "Saved ✓" — pick one per product, never mix.
5. Danger zone at bottom, visually separated, requires confirm.

**Allowed layout patterns.**
- `settings rail` (nav + content)
- `control row` (the only allowed row anatomy)
- `danger zone` (red-tinted, isolated)

**Kill list.**
- ❌ ANY decorative element.
- ❌ Icons without labels.
- ❌ Toggles that trigger irreversible actions without confirm.
- ❌ Motion beyond a 150ms fade.

---

## T-07 — Docs / Help (budget: 20%)

**Purpose.** Answer a question fast, then get out of the way.

**Content grammar.**
1. Search (dominant, top).
2. Doc nav (tree, left, collapsible, current item highlighted).
3. Article (720px column, generous line-height).
4. On-this-page nav (right, for articles > 3 screens).
5. "Was this helpful?" at bottom.
6. Edit/feedback link.

**Allowed layout patterns.**
- `three-column docs shell`
- `article layout`
- `code block` (with copy button, syntax highlight)
- `callout` (note / warning / tip — 3 types max)

**Interaction requirements.**
- Anchor links on every heading.
- Keyboard shortcut for search (`/` or `Cmd+K`).

**Kill list.**
- ❌ Full-bleed images mid-article.
- ❌ Serif display type for body (readability first).
- ❌ Scroll-jacking of any kind.

---

## T-08 — Billing / Pricing (in-product) (budget: 10%)

**Purpose.** Money decisions need calm and clarity, not pressure.

**Content grammar.**
1. Current plan state (what I have NOW).
2. Plan comparison (max 4 plans; differences, not full feature lists).
3. Price with billing period toggle (monthly/annual).
4. One primary CTA per plan row/column.
5. FAQ (max 6) — this is the ONE non-landing page where S14 lives.
6. Trust line (refund policy, cancel anytime) — plain text.

**Allowed layout patterns.**
- `plan table` (side-by-side, recommended plan visually elevated)
- `invoice list` (data table)
- `centered confirm` for plan changes

**Kill list.**
- ❌ Countdown timers / false scarcity.
- ❌ Hiding the downgrade path.
- ❌ Confetti on payment (it reads as mockery on expensive plans).

---

## T-09 — Onboarding / First-run (budget: 30%)

**Purpose.** Bridge between landing's promise and the product's reality.
This is the ONE app page allowed to feel a little cinematic.

**Content grammar.**
1. Welcome (1 line, echoing landing's promise — voice continuity).
2. Progress (3–5 steps max).
3. One action per step (setup, import, invite).
4. Skip always visible.
5. Final step = first moment of value (not a congratulation screen).

**Allowed layout patterns.**
- `centered wizard`
- `checklist panel` (persistent, dismissible)
- `empty-state-as-step` (first dashboard IS the tutorial)

**Interaction requirements.**
- Skippable at every step.
- Resumable (progress persists).
- Motion allowed up to 500ms here — the highest non-marketing budget.

**Kill list.**
- ❌ Product tours with 12 tooltips.
- ❌ Mandatory video watching.
- ❌ Asking for data you don't use immediately.

---

## T-10 — Report / Analytics (budget: 15%)

**Purpose.** Understanding, then decision. Data is the hero.

**Content grammar.**
1. Title + date range + export action.
2. Headline metric + delta ("+12% vs last period").
3. Primary chart (one, large).
4. Breakdown charts (small multiples, same scale).
5. Data table (for those who want the numbers).
6. Methodology footnote (how numbers are computed).

**Allowed layout patterns.**
- `chart panel`
- `metric band`
- `data table`
- `small multiples`

**Interaction requirements.**
- Every chart: hover tooltip with exact values.
- Chart types conservative: line / bar / donut. No 3D, ever.

**Kill list.**
- ❌ Animated chart entrances on every visit (animate once per session).
- ❌ Rainbow palettes (use brand scale, ≤ 6 data colors).
- ❌ Truncated axes that exaggerate deltas.

---

## T-11 — Error / System status (budget: 15%)

**Purpose.** The product failed. The page's job is to absorb frustration.

**Content grammar.**
1. What happened (plain language, no codes in the headline).
2. What the user can do (1 action: retry / go home / contact).
3. Technical detail (collapsed, for support).
4. Status page link (for 5xx).

**Allowed layout patterns.**
- `centered statement` + 1 illustration (this is where the budget goes)
- `inline error` for section-level failures (never lose page data)

**Kill list.**
- ❌ Blaming the user ("You did something wrong").
- ❌ Quirky humor on payment/data-loss errors (match severity).
- ❌ Dead ends — every error page has a way out.

---

## T-12 — Empty state (budget: 15%)

**Purpose.** Turn "nothing here" into "here's your first step".

**Content grammar.**
1. What this space will hold (1 line).
2. Why it's worth filling (1 line, max).
3. ONE action to create the first item.
4. Optional: sample data / template shortcut.

**Allowed layout patterns.**
- `centered statement` + illustration
- `inline empty` (small, inside panels)

**Kill list.**
- ❌ Multiple competing CTAs.
- ❌ Generic clip-art that ignores the constitution's illustration style.
- ❌ Guilt-tripping copy ("You haven't done anything yet!").

---

## Cross-type rules (apply to ALL 12)

- **Voice continuity.** Every headline in every page type could sit next
  to the landing hero and sound like the same person. Test: read the
  landing H1, then the dashboard title, out loud. Same human? Pass.
- **Chrome consistency.** Nav position, logo placement, avatar location,
  and footer presence are IDENTICAL across T-01..T-12 (landing excepted —
  it may break chrome deliberately).
- **Budget is per-page, not per-element.** Spending 30% of a 10% budget
  on three different elements = over budget. Sum matters.
- **Density inheritance.** `density` from the landing Blueprint maps to:
  minimal → app pages airy; rich → app pages compact. Never invert.

---

**End of catalog.**
