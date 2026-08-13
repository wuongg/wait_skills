---
name: patch-cinematic-landing-page
description: >
  Minimal, drop-in patch that upgrades `cinematic-landing-page` from v4.0 to
  v4.1 so it plays well with `landing-page-composition-architect` v1.0 and
  the INTEGRATION contract. Adds a Blueprint gate at PHASE 0, trims
  interview questions that the planner already answered, wires the
  validation gate + revision protocol, and locks a small set of new
  refusals. Does NOT change any archetype, motion, or code-generation
  logic. Reversible: revert by removing the four marked blocks.
license: MIT
version: 1.0
patches: cinematic-landing-page 4.0
result_version: cinematic-landing-page 4.1
compatible_with:
  - landing-page-composition-architect >=1.0
  - landing-page-skills-integration >=1.0
---

# PATCH — cinematic-landing-page v4.0 → v4.1

This patch is small on purpose. It touches only four spots in the original
skill and adds no new archetypes. The point is to make the builder **refuse
to author a page without a locked Blueprint** and to stop **re-asking
questions the planner already answered**.

**Target file (repo layout):**
`../cinematic-landing-page/SKILL.md`

Apply the four blocks below in order. Each block shows:
- **WHERE** (which section of that file)
- **ACTION** (insert / replace / append)
- **BLOCK** (verbatim text to paste)

Integration contract path: `../landing-page-skills-integration/SKILL.md`

At the end there is a Changelog + Rollback section.

---

## BLOCK 1 — Blueprint Gate at PHASE 0

**WHERE:** at the very top of `PHASE 0 — TRIGGER & TONE`, before the tone
paragraph.

**ACTION:** insert.

**BLOCK:**

```markdown
### PHASE 0.0 — BLUEPRINT GATE (v4.1)

Before doing ANYTHING else, check for a **locked Composition Blueprint**
(see `landing-page-skills-integration` /
`../landing-page-skills-integration/SKILL.md` §1).

**Rule.** You MUST NOT choose archetype, motion, mood, or write a single
line of code without a locked Blueprint in the conversation.

**Decision tree:**

1. **Blueprint present and `locked: true`** → accept it verbatim. Skip the
   parts of PHASE 1 that duplicate its fields (see BLOCK 2). Continue with
   art direction only.
2. **Blueprint present but `locked: false` or malformed** → refuse:
   > "Blueprint chưa lock — mình cần bản đã đóng dấu `locked: true` trước
   > khi build. Quay lại planner (`landing-page-composition-architect`)
   > để phát hành bản mới nhé."
3. **No Blueprint at all** → do NOT ask the user visual questions yet.
   Respond:
   > "Trước khi mình chọn archetype / motion, cần cấu trúc section đã
   > khóa. Bạn muốn mình gọi planner
   > (`landing-page-composition-architect`) chạy trước không? Nó xuất
   > Blueprint trong 1–2 lượt hỏi rồi handoff sang đây."
   Stop and wait.

**Exception — micro edits.** If the user only asks for a mechanical tweak
to an already-built page (change a color, swap a hero image, fix a typo),
you may proceed without a Blueprint. Anything that adds, reorders,
removes, or re-purposes a section requires re-planning.

**Anti-pattern (refuse):**
- "Cứ build tạm đi rồi tính" → No. Author without Blueprint = surface
  without structure = throwaway work.
- "Đơn giản thôi mà, cần gì planner" → Offer the default blueprint path:
  planner has a "mặc định đi" shortcut that finishes in one turn.
```

---

## BLOCK 2 — Skip planner-answered questions in the interview

**WHERE:** inside `PHASE 1 — THE INTERVIEW`, immediately before `Batch 0`.

**ACTION:** insert.

**BLOCK:**

```markdown
### v4.1 — Interview delta when a Blueprint is present

If PHASE 0.0 accepted a locked Blueprint, DO NOT re-ask any field the
Blueprint already supplies. Specifically:

| Original interview question | Skip if Blueprint provides |
|---|---|
| Archetype choice | dominant archetype is your call, but page **intent** and layout families are locked. Pick an archetype **compatible** with them (see INTEGRATION §3). |
| Product & audience | `page.intent`, `page.awareness`, `page.traffic` |
| Section list (for D) | `sections[]` (locked — do not renegotiate) |
| Scene beats (for B) | derive from any `layout_family: "mood gallery"` sections |
| Item list (for E) | derive from any `layout_family: "mood gallery"` or `card grid` items |
| Copy for hero | `sections[0].content_required` |
| Pace / scroll length | `page.pace` (map via INTEGRATION §5 T6) |
| Density | `page.density` (map via INTEGRATION §5 T7) |

**You may still ask about:**
- Mood (Dark Cinematic / Warm Editorial / Neo-Tech / Light Minimal / Light
  Editorial / Soft Glass) — unless `primary_emotion` unambiguously implies
  one via INTEGRATION §5 T5, in which case propose and ask for confirmation
  in a single line.
- Tech stack (V1 vanilla vs V2 React+Vite+Tailwind) — unless obvious from
  the intent (INTEGRATION defaults).
- Reference envy / competitor pages — only if you need a specific visual
  direction the Blueprint's `handoff_note` did not pin.
- Asset URLs / brand palette / typography.

**Batch budget.** With a Blueprint present, cap the interview at **one
batch of ≤3 questions**. If the Blueprint's `handoff_note` already covers
mood and stack, skip the interview entirely and present the Build Spec.
```

---

## BLOCK 3 — Wire the Build Spec + Validation Gate

**WHERE:** insert as a new phase after the Signature Interaction Library
(or after `PHASE 1 — THE INTERVIEW`) and before
`PHASE 2 — SPEC SHEET LOCK`.

**ACTION:** insert new phase.

**BLOCK:**

```markdown
## PHASE 1.6 — BUILD SPEC + VALIDATION (v4.1)

Before writing any code, emit a **Build Spec** derived from the Blueprint,
following INTEGRATION.md §4. Then run the Validation Gate (INTEGRATION.md
§6). All boxes must tick. If any fail:

- Do NOT patch around it in code.
- Emit a `revision_request` (INTEGRATION.md §7) back to the planner.
- Stop and wait for a new locked Blueprint (version bump).

**Build Spec must include, at minimum:**

- `stack` (V1 or V2)
- `dominant_archetype` (one of A–F)
- `second_archetype` (one of A–F or `null`; max 2 total on page)
- `mood`
- `sections[]` — one row per Blueprint section, in the same order, with
  `archetype`, `pattern`, `motion[]`, `media`, and a short `notes` field.
- `acceptance_criteria[]` — copy the Blueprint's rhythm rules and add
  motion/archetype caps.

**Present the Build Spec to the user in this format** (short, scannable):

```
BUILD SPEC v1.0 — READY
Stack: V2 (React + Vite + Tailwind + framer-motion)
Dominant archetype: A (split hero)   Second: none
Mood: Light Minimal
Motion budget: 2 / 2
Sections: S1(A) → S2(D) → S4(D) → S5(D) → S6(D) → S12(D) → S13(D) → S15(D)
Validation: PASS
```

Then ask ONE question:
> "Chốt Build Spec này để mình bắt đầu code?"

If user says yes → proceed to the original build phase.
If user changes any item → re-run validation before proceeding.
If user asks to change section order / add-remove sections → refuse and
route back to planner (this is a structure change, not a surface change).
```

---

## BLOCK 4 — Refusal list additions

**WHERE:** at the end of `## ANTI-PATTERNS (never do these)`.

**ACTION:** append.

**BLOCK:**

```markdown
### v4.1 additional refusals

- **"Đổi thứ tự section này cho hợp lý hơn."** → refuse. Section order is
  locked by the Blueprint. Emit a `revision_request` to the planner.
- **"Bỏ section này đi, không cần đâu."** → refuse. Same as above.
- **"Thêm banner CTA giữa trang cho chắc."** → refuse if the Blueprint's
  primary CTA is already placed. Extra CTAs violate INTEGRATION §6
  ("Primary CTA count = 1").
- **"Cho thêm hiệu ứng nữa cho đẹp."** → refuse if motion budget already
  at 2 signatures. Downgrade an existing one first or push back.
- **"Copy y hệt trang X."** → refuse. Offer to have planner
  reverse-engineer trang X's Blueprint instead.
- **"Skill planner rườm rà, bỏ đi được không?"** → refuse. Explain the
  golden rule: planner owns structure, builder owns surface. Without
  planner, builder degrades to templated output.

**Escape valve.** If the user explicitly insists on a violation after one
push-back, comply but mark the affected row in the Build Spec with
`"user_override": true` and reflect it in `acceptance_criteria` so the
downstream validator does not silently accept it.
```

---

## APPLYING THE PATCH — quick recipe

1. Open `../cinematic-landing-page/SKILL.md` v4.0
   (skill name `cinematic-landing-page` — not a separate `SKILL.md`).
2. Bump the version header from `version: 4.0` to `version: 4.1`.
3. Paste BLOCK 1 at the top of `PHASE 0 — TRIGGER & TONE`.
4. Paste BLOCK 2 immediately before `### Batch 0` inside
   `PHASE 1 — THE INTERVIEW`.
5. Paste BLOCK 3 as a new `PHASE 1.6` after the interview section and
   before `PHASE 2 — SPEC SHEET LOCK` (and before the Signature Interaction
   Library if you keep that between interview and Phase 2).
6. Paste BLOCK 4 at the end of `## ANTI-PATTERNS (never do these)`.
7. Save. No other lines of the v4.0 file need to change.

## CHANGELOG (v4.0 → v4.1)

- **Added.** PHASE 0.0 Blueprint Gate — refuses to author without a
  locked Blueprint. Micro-edit exception preserved.
- **Added.** PHASE 1.6 Build Spec + Validation — formalizes the artifact
  handed to the code phase; wires INTEGRATION §4 and §6.
- **Changed.** PHASE 1 interview — skips fields the planner already
  supplies (intent, awareness, section list, pace, density, hero copy).
  Batch budget drops to 1 × ≤3 questions when Blueprint is present.
- **Added.** Four new refusals aligned to INTEGRATION §8.
- **Unchanged.** All six archetypes (A–F), the 5 hero patterns, motion
  library, mood palette, stack choices, and the final code output format.

## ROLLBACK

To revert to v4.0: delete BLOCK 1, BLOCK 2, BLOCK 3, and BLOCK 4 (they are
clearly bounded). Change the version header back to `version: 4.0`.
Nothing else in the original file depends on these blocks.

---

**End of patch.**

> **Status:** blocks above are already applied in
> `../cinematic-landing-page/SKILL.md` (v4.1).
> Keep this file as the reversible changelog / re-apply recipe.
