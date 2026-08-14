---
name: landing-page-skills-tests
description: >
  Acceptance tests for the landing-page-skills pipeline. Each test is a
  self-contained brief → expected Blueprint (or expected refusal). Run
  these after ANY change to `landing-page-composition-architect` rules
  (Phases 1–5, slot library, heuristic engine) or to
  `landing-page-skills-integration` mapping/validation logic. A change is
  good only if it breaks zero tests, OR breaks tests in a way you
  consciously update. 30 tests total: 20 happy-path, 6 refusal-path,
  4 edge-case.
license: MIT
version: 1.0
compatible_with:
  - landing-page-composition-architect >=1.0
  - landing-page-skills-integration >=1.0
  - cinematic-landing-page >=4.1
---

# Landing Page Skills — Acceptance Tests v1

## How to use

Each test has four fields:

- **Brief** — the raw user request.
- **Expected** — what the planner MUST emit.
- **Rationale** — which rule(s) drive that expectation.
- **Tags** — `[happy]` / `[refusal]` / `[edge]`, plus intent ID.

When you change a rule:

1. Run all 30 tests mentally (or via a harness).
2. A test may legitimately flip expected output ONLY if you consciously
   accept that behavior change. Update the test in the same commit.
3. Any unaccounted-for flip is a regression.

---

## PART 1 — HAPPY-PATH TESTS (20)

### T01 — SaaS demo, cold, ads
**Brief.** "Làm landing cho tool dev, mục tiêu sign-up, ads traffic, có 4 features + 2 quotes."
**Expected.**
- Intent I2, awareness cold, traffic ads, pace balanced.
- Sections: S1 → S2 → S4 → S5 → S6 → S12 or S13 → S15 (or both S12+S13).
- S2 mandatory. No S8, no S9.
- Card grid ≤ 1.
**Rationale.** R1 (cold gate), R2 (ads gate), R8, slot cap.
**Tags.** [happy][I2]

### T02 — 3D studio, warm, referral
**Brief.** "Studio 3D premium, luxury vibe, có 8 render đẹp, không bán thô."
**Expected.**
- Intent I3, awareness warm, pace slow-burn.
- Sections: S1 → S8 → S10 → S9 → S11 → S16.
- No S15 (I3 exception), no S6/S14/S12/S13.
- Editorial exception R10 allows S8+S10 adjacency.
**Rationale.** I3 rules, R10, slot library I3 exceptions.
**Tags.** [happy][I3]

### T03 — Personal portfolio, warm
**Brief.** "Portfolio cá nhân, 5 case, 3-step process, 2 awards, không SaaS."
**Expected.**
- Intent I4.
- Sections: S1 → S10 → S7 → S8 → S11 → S16.
- Contact merged into S16. No S15.
- No card grid, no FAQ, no testimonials.
**Rationale.** I4 spine, S16 contact merge.
**Tags.** [happy][I4]

### T04 — Coming-soon teaser, cold, social
**Brief.** "Drop streetwear 30 ngày nữa, gom waitlist, 1 key visual + tagline."
**Expected.**
- Intent I6, pace fast.
- Sections: S1 → S9 → S3 → S15 (waitlist as primary).
- S2 legally skipped despite cold traffic (I6 exception).
- No S14, no S13, no S6.
**Rationale.** I6 S2-override, R9 (fast pace), I6 bans.
**Tags.** [happy][I6]

### T05 — Drone product story, cold, organic
**Brief.** "Camera drone mới, cần giải thích cơ chế, 2 phút demo video, 5 features, 3 use cases."
**Expected.**
- Intent I5, pace slow-burn, density rich.
- Sections: S1 → S2 → S4 → S5 → S6 → S7 → S13 → S15.
- S5 and S7 both staggered stack, separated by S6 (legal per R8 spirit).
**Rationale.** I5 default spine, R8 adjacency logic.
**Tags.** [happy][I5]

### T06 — Event conference, warm, social
**Brief.** "Conference 1 ngày, 8 speaker, 4 agenda, 3 sponsor, bán vé."
**Expected.**
- Intent I6 (event variant), pace balanced.
- Sections: S1 → S3 → S7 → S5 → S11 → S15.
- S7 repurposed as lineup card grid (legal).
**Rationale.** I6 flex on S7 role.
**Tags.** [happy][I6]

### T07 — Launch announcement, cold, organic
**Brief.** "Ra mắt brand cà phê mới, muốn tạo buzz."
**Expected.**
- Intent I1.
- Sections: S1 → S3 → S10 → S6 → S11 → S15.
- S10 (signature differentiator) used mid-page.
**Rationale.** I1 default spine.
**Tags.** [happy][I1]

### T08 — B2B SaaS, warm, organic
**Brief.** "Tool CRM cho SMB, khách đã biết category, muốn demo."
**Expected.**
- Intent I2, awareness warm.
- S2 skipped (warm awareness).
- Sections: S1 → S4 → S5 → S6 → S12 → S13 → S15.
**Rationale.** R1 negative branch.
**Tags.** [happy][I2]

### T09 — Fashion lookbook, warm
**Brief.** "Bộ sưu tập SS26, lookbook style, premium."
**Expected.**
- Intent I3.
- Heavy weight on S9. No card grid.
- S16 as contact/exit.
**Rationale.** I3 + S9 dominant.
**Tags.** [happy][I3]

### T10 — Agency site, warm
**Brief.** "Agency creative, 6 người, 4 case, muốn trang giới thiệu."
**Expected.**
- Intent I4.
- Sections: S1 → S10 → S7 → S8 → S11 → S16.
- Team content absorbed into S16 or S10 (not a new slot).
**Rationale.** Slot library is closed; no S17 "team" slot.
**Tags.** [happy][I4]

### T11 — App waitlist, cold, social
**Brief.** "App chưa launch, cần email list, 1 mockup, tagline."
**Expected.**
- Intent I6, pace fast.
- 4 sections. S15 = waitlist form.
**Rationale.** R9 length budget.
**Tags.** [happy][I6]

### T12 — Course landing, cold, ads
**Brief.** "Khóa học online, ads về landing, muốn bán. Có 3 module, 5 testimonial, 2 outcome stat."
**Expected.**
- Intent I2.
- Sections: S1 → S2 → S4 → S5 → S7 → S13 → S12 → S15 (or S13+S12 swapped).
- Trust cluster ≤ 2 — pick 2 of {S11, S12, S13}. Here S12+S13.
- No S14 (page already long).
**Rationale.** Trust cluster cap.
**Tags.** [happy][I2]

### T13 — Editorial magazine brand
**Brief.** "Tạp chí online về kiến trúc, cần trang brand, slow-burn."
**Expected.**
- Intent I3, pace slow-burn.
- Heavy editorial blocks. No card grid.
**Rationale.** R5 + R6.
**Tags.** [happy][I3]

### T14 — Hot-audience retargeting
**Brief.** "Ads retargeting tới người đã xem demo, chốt deal."
**Expected.**
- Intent I2, awareness hot.
- S2 banned. Short page (5 slots max).
- Skip S4 (they know the pain).
- S1 → S3 → S6 → S13 → S15.
**Rationale.** R1 hot branch.
**Tags.** [happy][I2]

### T15 — Studio solo photographer
**Brief.** "Freelance photographer, 30 ảnh, muốn trang giới thiệu."
**Expected.**
- Intent I4.
- S7 as work strip uses `staggered stack` or `mood gallery`.
- No card grid, no FAQ.
**Rationale.** I4 defaults.
**Tags.** [happy][I4]

### T16 — Developer tool open source
**Brief.** "Open-source CLI tool, muốn landing page để giải thích và link GitHub."
**Expected.**
- Intent I5.
- S15 CTA = "View on GitHub".
- Light trust (S11 optional if have logos).
**Rationale.** I5 default; CTA role preserved.
**Tags.** [happy][I5]

### T17 — Charity fundraiser
**Brief.** "Chiến dịch gây quỹ, 1 câu chuyện cảm động, 1 mục tiêu số."
**Expected.**
- Intent I3 or I6 (decide by "bán vé" vs "kêu gọi"). For gây quỹ: I3 with S15 donation CTA allowed.
- S15 = donate. No S14.
**Rationale.** I3 + S15 override for donation.
**Tags.** [happy][I3]

### T18 — Productized service
**Brief.** "Dịch vụ thiết kế logo trọn gói, $299, có 3 gói."
**Expected.**
- Intent I2.
- Pricing can be absorbed into S15 CTA band or as a new sub-section of S6 (not a new slot).
**Rationale.** Slot library closed; pricing is content, not slot.
**Tags.** [happy][I2]

### T19 — Micro-launch for a feature
**Brief.** "Feature mới trong app hiện có, muốn trang giới thiệu riêng."
**Expected.**
- Intent I1 (launch variant) or I5 (explainer) — disambiguate.
- If feature-focused: I5.
**Rationale.** Intent diagnosis with ambiguity resolution.
**Tags.** [happy][I1][I5]

### T20 — Portfolio team-of-two
**Brief.** "Studio 2 người, 6 dự án, không có award."
**Expected.**
- Intent I4.
- S11 dropped (asset reality — no awards, R3).
- Sections: S1 → S10 → S7 → S8 → S16.
**Rationale.** R3 (asset reality).
**Tags.** [happy][I4]

---

## PART 2 — REFUSAL-PATH TESTS (6)

### T21 — User demands 12 sections
**Brief.** "Cứ nhét 12 section cho đủ."
**Expected.** Refuse once, cap at 8 (or 9 for I5).
**Rationale.** Slot rule: sections.length ≤ 8 (≤9 for I5 heavy).
**Tags.** [refusal]

### T22 — User demands CTA in hero for cold traffic
**Brief.** "Đặt nút mua to ở hero luôn."
**Expected.** Push back once for cold traffic; if user insists, mark
`user_override: true` on S1.
**Rationale.** R7 + override protocol.
**Tags.** [refusal]

### T23 — User demands copy of a competitor page
**Brief.** "Copy y hệt trang Linear."
**Expected.** Refuse cloning. Offer reverse-engineered blueprint.
**Rationale.** PHASE 6 anti-pattern.
**Tags.** [refusal]

### T24 — User demands no hero
**Brief.** "Bỏ hero đi, vào thẳng features."
**Expected.** Refuse. S1 is mandatory.
**Rationale.** Slot rule: S1 mandatory.
**Tags.** [refusal]

### T25 — User demands 12-item feature grid
**Brief.** "Tôi có 12 features, cho hết vào grid."
**Expected.** Cap at 6 in S6. Suggest moving remainder to S7 as use cases.
**Rationale.** S6 slot definition caps at 6.
**Tags.** [refusal]

### T26 — User demands all trust signals
**Brief.** "Cho cả logo strip, metrics, testimonials, FAQ vào."
**Expected.** Collapse trust cluster to ≤ 2 of {S11, S12, S13}. S14 separate
decision based on intent.
**Rationale.** Trust cluster rule.
**Tags.** [refusal]

---

## PART 3 — EDGE-CASE TESTS (4)

### T27 — Ambiguous intent
**Brief.** "Làm trang cho sản phẩm mới, kiểu gì cũng được."
**Expected.** List top 2 intent candidates and ask ONE disambiguation
question. Do NOT guess.
**Rationale.** PHASE 1: ambiguous → ask.
**Tags.** [edge]

### T28 — User provides zero assets
**Brief.** "Chưa có gì cả, chỉ có ý tưởng."
**Expected.** Blueprint must only use slots with `content_required` that
planner can draft. Drop S11/S13 (need real quotes/logos).
**Rationale.** R3 (asset reality).
**Tags.** [edge]

### T29 — User asks for Blueprint change mid-build
**Brief.** (During builder phase) "Đổi S4 với S5 chỗ nhau."
**Expected.** Builder refuses. Routes back to planner with
`revision_request` (adjacency_violation or layout_conflict).
**Rationale.** `landing-page-skills-integration/SKILL.md` §2, §7.
**Tags.** [edge]

### T30 — Blueprint is present but malformed
**Brief.** Blueprint JSON has `locked: false` or missing `sections[]`.
**Expected.** Builder stops and asks planner to re-issue. Does NOT
auto-fix or proceed.
**Rationale.** PHASE 0.0 decision tree case 2.
**Tags.** [edge]

---

## PART 4 — REGRESSION HARNESS (optional, pseudocode)

```python
# tests.py — drop-in runner
import json

TESTS = [
    {"id": "T01", "brief": "...", "expect": {"intent": "I2", "awareness": "cold", ...}},
    # ...
]

def run(planner_fn, integration_fn):
    results = []
    for t in TESTS:
        blueprint = planner_fn(t["brief"])
        spec = integration_fn(blueprint)
        results.append(check(t, blueprint, spec))
    return results

def check(t, blueprint, spec):
    # Field-by-field comparison vs t["expect"]
    # Log flips
    ...
```

When in doubt, the human-readable tests in Parts 1–3 are the source of
truth. The harness is a convenience.

---

## PART 5 — MAINTENANCE RULES

1. **One test per behavior.** Don't bundle 3 expectations into one test.
2. **Every rule change = test review.** Update affected tests in the same
   commit.
3. **New slot, new intent, new layout family = new test.** At least one
   happy + one refusal.
4. **Don't delete tests.** If a behavior is intentionally removed, mark
   the test `[deprecated]` and add the replacement.
5. **Quarterly review.** Re-read `cinematic-landing-page/EXAMPLES.md` and
   this file together; prune any test that no longer represents a
   real-world brief pattern.

---

**End of tests.**
