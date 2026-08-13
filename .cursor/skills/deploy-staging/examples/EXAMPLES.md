---
name: landing-page-skills-examples
description: >
  End-to-end worked examples for the landing-page-skills pipeline. Six case
  studies — SaaS demo, 3D studio brand, personal portfolio, coming-soon
  teaser, product-story explainer, and event campaign — each showing:
  (1) the user brief, (2) the planner's Composition Blueprint (table + JSON),
  (3) the builder's Build Spec (JSON), (4) the validation gate result, and
  (5) rationale notes. Use these to calibrate the planner's judgement and
  to sanity-check new blueprints against known-good structures.
license: MIT
version: 1.0
compatible_with:
  - landing-page-composition-architect >=1.0
  - landing-page-skills-integration >=1.0
  - cinematic-landing-page >=4.1
---

# Landing Page Skills — Worked Examples v1

Six full pipelines from brief → shipped-ready spec. Each example follows the
same 5-block structure so you can diff them.

Structure per example:

1. **Brief** — the raw user request.
2. **Blueprint (table)** — planner output, user-facing.
3. **Blueprint (JSON)** — planner output, machine-facing.
4. **Build Spec (JSON)** — builder output, pre-code.
5. **Validation & notes** — why this passes; what almost went wrong.

---

## EXAMPLE 1 — SaaS Demo Landing (I2 Conversion)

### 1.1 Brief

> "Làm landing page cho tool phân tích log dev. Muốn cho developer đăng ký
> dùng thử. Traffic chủ yếu từ Google Ads. Có 4 feature chính, 3 logo khách,
> 2 quote từ user cũ, 1 metric '50% giảm thời gian debug'. Không có video."

### 1.2 Blueprint — table

- **Page intent:** I2 Conversion
- **Awareness level:** cold
- **Traffic:** ads
- **Narrative spine:** Problem → Solution → Benefits → Trust → CTA
- **Pace:** balanced
- **Density:** balanced
- **Total sections:** 8

| # | Slot | Section name | JTBD | Why here | Layout family | Content required | Visual weight | CTA role |
|---|------|--------------|------|----------|---------------|------------------|---------------|----------|
| 1 | S1 | Hero | Grab attention + one clear promise | first impression | split hero | headline, subcopy, product screenshot | very high | soft |
| 2 | S2 | Fast Context | Clarify what the tool is in 1 line | cold + ads gate | centered statement | 1-sentence clarifier | low | none |
| 3 | S4 | The Debug Tax | Name the pain | before selling solution | editorial block | pain paragraph, small illustration | medium | none |
| 4 | S5 | How It Works | Show the mechanism | after pain lands | staggered stack | 3 steps, each with copy + micro-diagram | high | none |
| 5 | S6 | Features | Prove capability | after mechanism | card grid | 4 features (title + 1-line desc + icon) | medium | none |
| 6 | S12 | Outcomes | Quantify value | before ask | metric band | "50% less debug time" + 2 supporting stats | high | none |
| 7 | S13 | Voices | Human validation | reduce doubt | quote panel | 2 quotes, name + role | medium | none |
| 8 | S15 | Start Free | The ask | close | CTA band | CTA copy, email form | high | primary |

### 1.3 Blueprint — JSON

```json
{
  "blueprint_version": "1.0",
  "page": {
    "intent": "I2",
    "intent_name": "Conversion",
    "awareness": "cold",
    "traffic": "ads",
    "narrative_spine": "Problem -> Solution -> Benefits -> Trust -> CTA",
    "pace": "balanced",
    "density": "balanced",
    "primary_emotion": "clarity",
    "total_sections": 8
  },
  "sections": [
    {"index": 1, "slot": "S1",  "name": "Hero",         "jtbd": "grab attention + one clear promise", "why_here": "first impression",         "layout_family": "split hero",         "content_required": ["headline","subcopy","product_screenshot"], "visual_weight": "very high", "cta_role": "soft"},
    {"index": 2, "slot": "S2",  "name": "Fast Context", "jtbd": "clarify what the tool is",           "why_here": "cold + ads gate",           "layout_family": "centered statement", "content_required": ["one_sentence_clarifier"],                    "visual_weight": "low",       "cta_role": "none"},
    {"index": 3, "slot": "S4",  "name": "The Debug Tax","jtbd": "name the pain",                       "why_here": "before selling solution",   "layout_family": "editorial block",    "content_required": ["pain_paragraph","illustration"],             "visual_weight": "medium",    "cta_role": "none"},
    {"index": 4, "slot": "S5",  "name": "How It Works", "jtbd": "show mechanism",                      "why_here": "after pain lands",          "layout_family": "staggered stack",    "content_required": ["step1","step2","step3","diagrams"],          "visual_weight": "high",      "cta_role": "none"},
    {"index": 5, "slot": "S6",  "name": "Features",     "jtbd": "prove capability",                    "why_here": "after mechanism",           "layout_family": "card grid",          "content_required": ["4_features"],                                "visual_weight": "medium",    "cta_role": "none"},
    {"index": 6, "slot": "S12", "name": "Outcomes",     "jtbd": "quantify value",                      "why_here": "before ask",                "layout_family": "metric band",        "content_required": ["primary_metric","two_supporting_metrics"],   "visual_weight": "high",      "cta_role": "none"},
    {"index": 7, "slot": "S13", "name": "Voices",       "jtbd": "human validation",                    "why_here": "reduce doubt",              "layout_family": "quote panel",        "content_required": ["quote1","quote2"],                           "visual_weight": "medium",    "cta_role": "none"},
    {"index": 8, "slot": "S15", "name": "Start Free",   "jtbd": "convert",                             "why_here": "close",                     "layout_family": "CTA band",           "content_required": ["cta_copy","email_form"],                     "visual_weight": "high",      "cta_role": "primary"}
  ],
  "rhythm_rules": [
    "No two 'very high' weight sections adjacent.",
    "Primary CTA in S15 only.",
    "Card grid appears exactly once (S6).",
    "Trust cluster limited to S12 + S13 (no S11 — only 3 logos not enough)."
  ],
  "kill_list": [
    "No S8 (brand philosophy — ads traffic, wastes attention).",
    "No S9 (mood gallery — off-intent for tool demo).",
    "No S14 (FAQ — page already dense).",
    "No S11 (logo strip — only 3 logos, weak signal)."
  ],
  "handoff_note": "Preserve clarity above all. S1 wants cinematic weight; S4 and S13 must stay quiet and readable. Order and layout families are LOCKED.",
  "locked": true
}
```

### 1.4 Build Spec — JSON

```json
{
  "build_spec_version": "1.0",
  "blueprint_ref": "locked",
  "stack": "V2 react-vite-tailwind",
  "dominant_archetype": "A",
  "second_archetype": null,
  "mood": "Light Minimal",
  "sections": [
    {"index": 1, "slot": "S1",  "layout_family": "split hero",         "archetype": "A", "pattern": "split",         "motion": ["hero_fade_in_800ms","subcopy_delay_200ms"], "media": {"type": "image", "asset_ref": "hero_screenshot.png"}, "notes": "Dominant archetype anchor."},
    {"index": 2, "slot": "S2",  "layout_family": "centered statement", "archetype": "D", "pattern": "centered",      "motion": [],                                          "media": {"type": "none"},                                        "notes": "Kept intentionally quiet — reads in 2s."},
    {"index": 3, "slot": "S4",  "layout_family": "editorial block",    "archetype": "D", "pattern": "editorial",     "motion": ["fade_on_enter"],                           "media": {"type": "image","asset_ref": "debug_pain.svg"},         "notes": "Long-form pain narrative."},
    {"index": 4, "slot": "S5",  "layout_family": "staggered stack",    "archetype": "D", "pattern": "alternating",   "motion": ["stagger_reveal_100ms"],                    "media": {"type": "image","asset_ref": "step_diagrams/*"},        "notes": "Only place motion is felt in body."},
    {"index": 5, "slot": "S6",  "layout_family": "card grid",          "archetype": "D", "pattern": "2x2",           "motion": ["hover_lift_soft"],                         "media": {"type": "image","asset_ref": "feature_icons/*"},        "notes": "Max 4 tiles — hard cap."},
    {"index": 6, "slot": "S12", "layout_family": "metric band",        "archetype": "D", "pattern": "big-number",    "motion": ["count_up_on_view_1200ms"],                 "media": {"type": "none"},                                        "notes": "Second signature interaction; consumes motion budget."},
    {"index": 7, "slot": "S13", "layout_family": "quote panel",        "archetype": "D", "pattern": "single-quote",  "motion": [],                                          "media": {"type": "none"},                                        "notes": "Single quote per view, no carousel."},
    {"index": 8, "slot": "S15", "layout_family": "CTA band",           "archetype": "D", "pattern": "centered-form", "motion": [],                                          "media": {"type": "none"},                                        "notes": "Only primary CTA on page."}
  ],
  "acceptance_criteria": [
    "First viewport = S1 composition only.",
    "Primary CTA in S15 exactly once.",
    "No adjacent 'very high' weight sections (checked: S1→S2 ok, S5→S6 ok, S6→S12 ok).",
    "Motion signatures = 2 (hero reveal + metric count-up).",
    "Card grid appears exactly once."
  ]
}
```

### 1.5 Validation & notes

- ✅ 8 sections, all INTEGRATION.md §6 checks pass.
- ✅ S2 present right after S1 (awareness = cold gate).
- ✅ No S6/S9 adjacency (S9 not on page).
- ✅ Trust cluster ≤ 2 (S12 + S13).
- ⚠️ Almost included S11 logo strip — dropped because only 3 logos = weak.
  Rule R3 (asset reality).
- ⚠️ Motion budget consumed by hero + metric count-up. No more allowed.

---

## EXAMPLE 2 — 3D Studio Brand Page (I3 Brand Editorial)

### 2.1 Brief

> "Studio 3D visualization cao cấp, khách là brand luxury. Muốn trang cảm
> giác reverence, không bán hàng thô. Có 8 dự án ảnh render đẹp, 1 manifesto
> ngắn, 4 giải thưởng."

### 2.2 Blueprint — table

- **Page intent:** I3 Brand Editorial
- **Awareness level:** warm
- **Traffic:** referral
- **Narrative spine:** Atmosphere → Philosophy → Signature → World
- **Pace:** slow-burn
- **Density:** minimal
- **Total sections:** 6

| # | Slot | Section name | JTBD | Why here | Layout family | Content required | Visual weight | CTA role |
|---|------|--------------|------|----------|---------------|------------------|---------------|----------|
| 1 | S1 | Atmosphere | Set the mood | first impression | full-bleed hero | hero image/video, studio name | very high | none |
| 2 | S8 | Manifesto | State the belief | ground the brand | editorial block | manifesto paragraph | medium | none |
| 3 | S10 | The Craft | Signature differentiator | why-us | editorial block | 1 short essay + inline image | high | none |
| 4 | S9 | World | Immersive gallery | show, don't tell | mood gallery | 6–8 selected renders | very high | none |
| 5 | S11 | Recognition | Trust anchor | quiet proof | logo strip | 4 award marks | low | none |
| 6 | S16 | Contact | Soft exit | quiet close | soft footer | email, IG handle | very low | soft |

### 2.3 Blueprint — JSON

```json
{
  "blueprint_version": "1.0",
  "page": {
    "intent": "I3",
    "intent_name": "Brand Editorial",
    "awareness": "warm",
    "traffic": "referral",
    "narrative_spine": "Atmosphere -> Philosophy -> Signature -> World",
    "pace": "slow-burn",
    "density": "minimal",
    "primary_emotion": "reverence",
    "total_sections": 6
  },
  "sections": [
    {"index": 1, "slot": "S1",  "name": "Atmosphere",  "jtbd": "set the mood",           "why_here": "first impression", "layout_family": "full-bleed hero", "content_required": ["hero_media","studio_name"], "visual_weight": "very high", "cta_role": "none"},
    {"index": 2, "slot": "S8",  "name": "Manifesto",   "jtbd": "state the belief",       "why_here": "ground the brand", "layout_family": "editorial block", "content_required": ["manifesto_paragraph"],       "visual_weight": "medium",    "cta_role": "none"},
    {"index": 3, "slot": "S10", "name": "The Craft",   "jtbd": "signature differentiator","why_here": "why-us",           "layout_family": "editorial block", "content_required": ["short_essay","inline_image"],"visual_weight": "high",      "cta_role": "none"},
    {"index": 4, "slot": "S9",  "name": "World",       "jtbd": "immersive proof",        "why_here": "show don't tell",  "layout_family": "mood gallery",    "content_required": ["6_to_8_renders"],            "visual_weight": "very high", "cta_role": "none"},
    {"index": 5, "slot": "S11", "name": "Recognition", "jtbd": "trust anchor",           "why_here": "quiet proof",      "layout_family": "logo strip",      "content_required": ["4_award_marks"],             "visual_weight": "low",       "cta_role": "none"},
    {"index": 6, "slot": "S16", "name": "Contact",     "jtbd": "soft exit",              "why_here": "quiet close",      "layout_family": "soft footer",     "content_required": ["email","ig_handle"],         "visual_weight": "very low",  "cta_role": "soft"}
  ],
  "rhythm_rules": [
    "Editorial exception (R10) invoked: S8 + S10 back-to-back allowed because visual weight steps medium -> high.",
    "S9 must follow an editorial block, not another gallery.",
    "No primary CTA. S16 uses soft link only."
  ],
  "kill_list": [
    "No S6 (card grid — feels SaaS).",
    "No S12 (metric band — breaks editorial voice).",
    "No S13 (SaaS-style testimonials).",
    "No S14 (FAQ — kills mood, banned for I3).",
    "No S15 (hard CTA — brand page ends with S16)."
  ],
  "handoff_note": "Reverence is the emotion. S1 and S9 want cinematic treatment (dominant archetype should carry both). Body sections stay hushed and readable. Order and layout families are LOCKED.",
  "locked": true
}
```

### 2.4 Build Spec — JSON

```json
{
  "build_spec_version": "1.0",
  "blueprint_ref": "locked",
  "stack": "V1 vanilla",
  "dominant_archetype": "B",
  "second_archetype": "F",
  "mood": "Dark Cinematic",
  "sections": [
    {"index": 1, "slot": "S1",  "layout_family": "full-bleed hero", "archetype": "F", "pattern": "kinetic-type-poster",   "motion": ["marquee_studio_name_25s","char_fade_0.07s"], "media": {"type": "video","asset_ref": "hero_loop.mp4"}, "notes": "Kinetic type sets the tone; second signature."},
    {"index": 2, "slot": "S8",  "layout_family": "editorial block", "archetype": "D", "pattern": "editorial",             "motion": ["fade_on_enter"],                             "media": {"type": "none"},                               "notes": "Quiet body."},
    {"index": 3, "slot": "S10", "layout_family": "editorial block", "archetype": "D", "pattern": "editorial-w-image",     "motion": ["fade_on_enter"],                             "media": {"type": "image","asset_ref": "craft_still.jpg"}, "notes": "Weight bump per R10."},
    {"index": 4, "slot": "S9",  "layout_family": "mood gallery",    "archetype": "B", "pattern": "sticky-cinema-scroll",  "motion": ["scroll_scrub_layers"],                       "media": {"type": "image","asset_ref": "renders/*"},     "notes": "Dominant archetype anchor; consumes motion budget."},
    {"index": 5, "slot": "S11", "layout_family": "logo strip",      "archetype": "D", "pattern": "quiet-row",             "motion": [],                                            "media": {"type": "image","asset_ref": "awards/*"},      "notes": "No motion; visual weight low."},
    {"index": 6, "slot": "S16", "layout_family": "soft footer",     "archetype": "D", "pattern": "minimal-footer",        "motion": [],                                            "media": {"type": "none"},                               "notes": "Soft close, no hard CTA."}
  ],
  "acceptance_criteria": [
    "First viewport = S1 composition only.",
    "No primary CTA on page (I3 exception).",
    "Signature archetypes = 2 (F for hero, B for gallery).",
    "No S6/S9 adjacency.",
    "Editorial exception R10 honored (S8 medium -> S10 high)."
  ]
}
```

### 2.5 Validation & notes

- ✅ 6 sections. All INTEGRATION.md §6 checks pass.
- ✅ Primary CTA count = 0 (allowed for I3 with soft-footer close).
- ✅ 2 signature archetypes (F + B) — at cap.
- ⚠️ Two editorial blocks back-to-back (S8, S10) — legal via R10 because
  weight steps up.
- ⚠️ Adjacency S10 (editorial) → S9 (mood gallery) is OK; the forbidden
  pair is S6+S9, not editorial+S9.

---

## EXAMPLE 3 — Personal Portfolio (I4 Portfolio)

### 3.1 Brief

> "Portfolio cá nhân — mình là product designer freelance. 5 case study
> chính, 3 bước process, 2 giải thưởng nhỏ. Không muốn kiểu SaaS."

### 3.2 Blueprint — table

- **Page intent:** I4 Portfolio
- **Awareness level:** warm
- **Traffic:** direct
- **Narrative spine:** Identity → Work → Method → Contact
- **Pace:** balanced
- **Density:** balanced
- **Total sections:** 6

| # | Slot | Section name | JTBD | Why here | Layout family | Content required | Visual weight | CTA role |
|---|------|--------------|------|----------|---------------|------------------|---------------|----------|
| 1 | S1 | Identity | Say who you are | first impression | full-bleed hero | name, role, tagline, portrait | very high | soft |
| 2 | S10 | What I Do Best | Signature differentiator | why hire me | editorial block | 1 paragraph + 1 image | medium | none |
| 3 | S7 | Selected Work | Show the goods | anchor of page | staggered stack | 5 case study rows | high | soft |
| 4 | S8 | How I Work | Process | after seeing work | editorial block | 3 steps as prose | medium | none |
| 5 | S11 | Recognition | Trust anchor | quiet proof | logo strip | 2 award marks + 3 client logos | low | none |
| 6 | S16 | Say Hi | Soft exit + contact | close | soft footer | email, LinkedIn, socials | low | soft |

### 3.3 Blueprint — JSON

```json
{
  "blueprint_version": "1.0",
  "page": {
    "intent": "I4",
    "intent_name": "Portfolio",
    "awareness": "warm",
    "traffic": "direct",
    "narrative_spine": "Identity -> Work -> Method -> Contact",
    "pace": "balanced",
    "density": "balanced",
    "primary_emotion": "confidence",
    "total_sections": 6
  },
  "sections": [
    {"index": 1, "slot": "S1",  "name": "Identity",       "jtbd": "say who you are",       "why_here": "first impression", "layout_family": "full-bleed hero", "content_required": ["name","role","tagline","portrait"], "visual_weight": "very high", "cta_role": "soft"},
    {"index": 2, "slot": "S10", "name": "What I Do Best", "jtbd": "signature differentiator","why_here": "why hire me",     "layout_family": "editorial block", "content_required": ["paragraph","inline_image"],         "visual_weight": "medium",    "cta_role": "none"},
    {"index": 3, "slot": "S7",  "name": "Selected Work",  "jtbd": "show the goods",         "why_here": "anchor of page",   "layout_family": "staggered stack", "content_required": ["5_case_rows"],                       "visual_weight": "high",      "cta_role": "soft"},
    {"index": 4, "slot": "S8",  "name": "How I Work",     "jtbd": "process",                "why_here": "after work shown", "layout_family": "editorial block", "content_required": ["3_steps_prose"],                     "visual_weight": "medium",    "cta_role": "none"},
    {"index": 5, "slot": "S11", "name": "Recognition",    "jtbd": "trust anchor",           "why_here": "quiet proof",      "layout_family": "logo strip",      "content_required": ["awards","client_logos"],             "visual_weight": "low",       "cta_role": "none"},
    {"index": 6, "slot": "S16", "name": "Say Hi",         "jtbd": "soft exit + contact",    "why_here": "close",            "layout_family": "soft footer",     "content_required": ["email","linkedin","socials"],        "visual_weight": "low",       "cta_role": "soft"}
  ],
  "rhythm_rules": [
    "Work strip (S7) is the anchor, not the hero.",
    "Contact merged into S16 (no S15 needed for I4).",
    "Case rows staggered — no card-grid feel."
  ],
  "kill_list": [
    "No S6 (feels SaaS).",
    "No S14 (FAQ — discouraged for I4).",
    "No S13 (testimonial carousel — cheapens portfolio).",
    "No metric band."
  ],
  "handoff_note": "Confidence, restraint. S1 wants cinematic treatment; S7 wants image quality high but layout quiet. Everything else hushed. Order and layout families are LOCKED.",
  "locked": true
}
```

### 3.4 Build Spec — JSON

```json
{
  "build_spec_version": "1.0",
  "blueprint_ref": "locked",
  "stack": "V1 vanilla",
  "dominant_archetype": "C",
  "second_archetype": null,
  "mood": "Warm Editorial",
  "sections": [
    {"index": 1, "slot": "S1",  "layout_family": "full-bleed hero", "archetype": "C", "pattern": "cursor-spotlight", "motion": ["cursor_spotlight_mask"], "media": {"type": "image","asset_ref": "portrait.jpg"},    "notes": "Dominant archetype — one signature interaction."},
    {"index": 2, "slot": "S10", "layout_family": "editorial block", "archetype": "D", "pattern": "editorial",        "motion": ["fade_on_enter"],         "media": {"type": "image","asset_ref": "craft.jpg"},         "notes": "Body reads first."},
    {"index": 3, "slot": "S7",  "layout_family": "staggered stack", "archetype": "D", "pattern": "alternating-rows", "motion": ["stagger_reveal_100ms"],  "media": {"type": "image","asset_ref": "cases/*"},           "notes": "Second signature; anchor of page."},
    {"index": 4, "slot": "S8",  "layout_family": "editorial block", "archetype": "D", "pattern": "editorial",        "motion": ["fade_on_enter"],         "media": {"type": "none"},                                   "notes": "Prose, no diagrams."},
    {"index": 5, "slot": "S11", "layout_family": "logo strip",      "archetype": "D", "pattern": "quiet-row",        "motion": [],                        "media": {"type": "image","asset_ref": "marks/*"},           "notes": "Quiet."},
    {"index": 6, "slot": "S16", "layout_family": "soft footer",     "archetype": "D", "pattern": "minimal-footer",   "motion": [],                        "media": {"type": "none"},                                   "notes": "Contact merged; soft CTA text link only."}
  ],
  "acceptance_criteria": [
    "First viewport = S1 composition only.",
    "No primary CTA (I4 exception with S16 contact).",
    "Signature archetypes = 1 (C).",
    "No card grid on page.",
    "Motion signatures = 2 (spotlight + case reveal)."
  ]
}
```

### 3.5 Validation & notes

- ✅ 6 sections. All INTEGRATION.md §6 checks pass.
- ✅ No S6, no S14, no S13 — I4 discipline maintained.
- ⚠️ S1 cta_role = soft (scroll cue), not primary. Contact lives in S16.
- ⚠️ Awareness = warm → S2 skipped intentionally (R1 allows).

---

## EXAMPLE 4 — Coming-Soon Teaser (I6 Campaign)

### 4.1 Brief

> "Ra mắt bộ sưu tập streetwear mới trong 30 ngày nữa. Muốn hype + gom
> waitlist. Có 1 key visual, 1 câu tagline. Trang phải nhanh."

### 4.2 Blueprint — table

- **Page intent:** I6 Campaign / Teaser
- **Awareness level:** cold
- **Traffic:** social
- **Narrative spine:** Tease → World → Details → Action
- **Pace:** fast
- **Density:** minimal
- **Total sections:** 4

| # | Slot | Section name | JTBD | Why here | Layout family | Content required | Visual weight | CTA role |
|---|------|--------------|------|----------|---------------|------------------|---------------|----------|
| 1 | S1 | Tease | Grab, don't explain | first impression | full-bleed hero | key visual, tagline | very high | none |
| 2 | S9 | The World | Atmosphere | build desire | mood gallery | 3–4 supporting shots | high | none |
| 3 | S3 | Drop Date | Concrete promise | anchor the hype | centered statement | date, one-line pitch | medium | none |
| 4 | S15 | Join Waitlist | The ask | close | CTA band | email form, privacy note | high | primary |

### 4.3 Blueprint — JSON

```json
{
  "blueprint_version": "1.0",
  "page": {
    "intent": "I6",
    "intent_name": "Campaign / Teaser",
    "awareness": "cold",
    "traffic": "social",
    "narrative_spine": "Tease -> World -> Details -> Action",
    "pace": "fast",
    "density": "minimal",
    "primary_emotion": "hype",
    "total_sections": 4
  },
  "sections": [
    {"index": 1, "slot": "S1",  "name": "Tease",         "jtbd": "grab, don't explain", "why_here": "first impression", "layout_family": "full-bleed hero",    "content_required": ["key_visual","tagline"], "visual_weight": "very high", "cta_role": "none"},
    {"index": 2, "slot": "S9",  "name": "The World",     "jtbd": "atmosphere",          "why_here": "build desire",     "layout_family": "mood gallery",       "content_required": ["3_to_4_shots"],         "visual_weight": "high",      "cta_role": "none"},
    {"index": 3, "slot": "S3",  "name": "Drop Date",     "jtbd": "concrete promise",    "why_here": "anchor the hype",  "layout_family": "centered statement", "content_required": ["date","one_line_pitch"],"visual_weight": "medium",    "cta_role": "none"},
    {"index": 4, "slot": "S15", "name": "Join Waitlist", "jtbd": "convert",             "why_here": "close",            "layout_family": "CTA band",           "content_required": ["email_form","privacy_note"],"visual_weight": "high",  "cta_role": "primary"}
  ],
  "rhythm_rules": [
    "R9 fast pace: 4 slots hard cap.",
    "S2 skipped despite cold traffic — teaser intent overrides clarifier (I6 exception).",
    "After S9 mood gallery, S3 centered statement provides the visual-weight step-down."
  ],
  "kill_list": [
    "No S6 (features — no product to feature yet).",
    "No S8 (philosophy — kills teaser energy).",
    "No S14 (FAQ — banned for I6).",
    "No S13 (no testimonials for unreleased product)."
  ],
  "handoff_note": "Hype is the emotion. S1 and S9 both want cinematic weight. Total scroll <= 2.5 viewports. Order and layout families are LOCKED.",
  "locked": true
}
```

### 4.4 Build Spec — JSON

```json
{
  "build_spec_version": "1.0",
  "blueprint_ref": "locked",
  "stack": "V1 vanilla",
  "dominant_archetype": "F",
  "second_archetype": "E",
  "mood": "Dark Cinematic",
  "sections": [
    {"index": 1, "slot": "S1",  "layout_family": "full-bleed hero",    "archetype": "F", "pattern": "kinetic-type-over-cutout", "motion": ["marquee_tagline_22s","char_fade_0.07s"], "media": {"type": "image","asset_ref": "hero_cutout.png"}, "notes": "Dominant archetype."},
    {"index": 2, "slot": "S9",  "layout_family": "mood gallery",       "archetype": "E", "pattern": "switcher-crossfade",       "motion": ["opacity_swap_700ms"],                    "media": {"type": "image","asset_ref": "world/*"},        "notes": "Second archetype; balanced pace picks E."},
    {"index": 3, "slot": "S3",  "layout_family": "centered statement", "archetype": "D", "pattern": "centered",                 "motion": [],                                        "media": {"type": "none"},                                "notes": "Step-down after S9."},
    {"index": 4, "slot": "S15", "layout_family": "CTA band",           "archetype": "D", "pattern": "centered-form",            "motion": [],                                        "media": {"type": "none"},                                "notes": "Waitlist form, single primary CTA."}
  ],
  "acceptance_criteria": [
    "First viewport = S1 only.",
    "Primary CTA = 1 (S15).",
    "Signature archetypes = 2 (F + E) — at cap.",
    "Scroll length <= 2.5 viewports.",
    "No adjacency violation (S1 -> S9 -> S3 -> S15)."
  ]
}
```

### 4.5 Validation & notes

- ✅ 4 sections (minimum allowed; fast pace).
- ⚠️ S2 skipped despite cold traffic — I6 teaser intent legally overrides
  R1 (clarifier would kill the mystery).
- ⚠️ Motion budget saturated at signature level (F + E). No extra body motion.

---

## EXAMPLE 5 — Product Story Explainer (I5)

### 5.1 Brief

> "Camera drone mới, giá tầm trung. Cần giải thích cơ chế chống rung mới.
> Có 2 phút video demo, 5 feature, 3 use case (du lịch, gia đình, sáng tạo),
> 2 quote."

### 5.2 Blueprint — table

- **Page intent:** I5 Product Story
- **Awareness level:** cold
- **Traffic:** organic
- **Narrative spine:** Context → Mechanism → Benefits → Use cases → CTA
- **Pace:** slow-burn
- **Density:** rich
- **Total sections:** 8

| # | Slot | Section name | JTBD | Why here | Layout family | Content required | Visual weight | CTA role |
|---|------|--------------|------|----------|---------------|------------------|---------------|----------|
| 1 | S1 | Meet the drone | Hook + product reveal | first impression | full-bleed hero | product shot/video | very high | soft |
| 2 | S2 | What it is | 1-line clarifier | cold gate | centered statement | one-liner | low | none |
| 3 | S4 | The Shake Problem | Name the pain | before mechanism | editorial block | pain paragraph + comparison clip | medium | none |
| 4 | S5 | How Stabilization Works | Show mechanism | anchor of page | staggered stack | 3 layers of stabilization, each with copy + diagram | high | none |
| 5 | S6 | Features | Prove capability | after mechanism | card grid | 5 features (icon + title + line) | medium | none |
| 6 | S7 | Fits Your Trip | Use cases | help user project themselves | staggered stack | 3 scenarios, image + copy | high | none |
| 7 | S13 | Owner Voices | Human validation | reduce doubt | quote panel | 2 quotes | medium | none |
| 8 | S15 | Get Yours | Convert | close | CTA band | CTA copy, price anchor | high | primary |

### 5.3 Blueprint — JSON

```json
{
  "blueprint_version": "1.0",
  "page": {
    "intent": "I5",
    "intent_name": "Product Story",
    "awareness": "cold",
    "traffic": "organic",
    "narrative_spine": "Context -> Mechanism -> Benefits -> Use cases -> CTA",
    "pace": "slow-burn",
    "density": "rich",
    "primary_emotion": "wonder",
    "total_sections": 8
  },
  "sections": [
    {"index": 1, "slot": "S1",  "name": "Meet the drone",       "jtbd": "hook + product reveal", "why_here": "first impression",   "layout_family": "full-bleed hero",    "content_required": ["product_video"],                    "visual_weight": "very high", "cta_role": "soft"},
    {"index": 2, "slot": "S2",  "name": "What it is",           "jtbd": "1-line clarifier",      "why_here": "cold gate",           "layout_family": "centered statement", "content_required": ["one_liner"],                        "visual_weight": "low",       "cta_role": "none"},
    {"index": 3, "slot": "S4",  "name": "The Shake Problem",    "jtbd": "name the pain",         "why_here": "before mechanism",    "layout_family": "editorial block",    "content_required": ["pain_paragraph","comparison_clip"], "visual_weight": "medium",    "cta_role": "none"},
    {"index": 4, "slot": "S5",  "name": "How Stabilization Works","jtbd": "show mechanism",      "why_here": "anchor of page",      "layout_family": "staggered stack",    "content_required": ["3_layers_diagrams"],                "visual_weight": "high",      "cta_role": "none"},
    {"index": 5, "slot": "S6",  "name": "Features",             "jtbd": "prove capability",      "why_here": "after mechanism",     "layout_family": "card grid",          "content_required": ["5_features"],                       "visual_weight": "medium",    "cta_role": "none"},
    {"index": 6, "slot": "S7",  "name": "Fits Your Trip",       "jtbd": "use cases",             "why_here": "self-projection",     "layout_family": "staggered stack",    "content_required": ["3_scenarios"],                      "visual_weight": "high",      "cta_role": "none"},
    {"index": 7, "slot": "S13", "name": "Owner Voices",         "jtbd": "human validation",      "why_here": "reduce doubt",        "layout_family": "quote panel",        "content_required": ["2_quotes"],                         "visual_weight": "medium",    "cta_role": "none"},
    {"index": 8, "slot": "S15", "name": "Get Yours",            "jtbd": "convert",               "why_here": "close",               "layout_family": "CTA band",           "content_required": ["cta_copy","price_anchor"],          "visual_weight": "high",      "cta_role": "primary"}
  ],
  "rhythm_rules": [
    "Slow-burn pace: 8 slots allowed.",
    "Card grid appears exactly once (S6).",
    "Staggered stack allowed twice (S5 and S7) — legal because separated by S6.",
    "Trust cluster = S13 only (single-source trust; no S11/S12 needed)."
  ],
  "kill_list": [
    "No S8 (philosophy — off-intent for explainer).",
    "No S9 (mood gallery — competes with mechanism section).",
    "No S11 (logo strip — not enough B2B logos to matter).",
    "No S14 (FAQ — page already 8 sections; would tip to bloat)."
  ],
  "handoff_note": "Wonder is the emotion. S1 and S5 want cinematic scroll story treatment (this is where B archetype earns its keep). S4 through S7 form the education spine — stay clear over clever. Order and layout families are LOCKED.",
  "locked": true
}
```

### 5.4 Build Spec — JSON

```json
{
  "build_spec_version": "1.0",
  "blueprint_ref": "locked",
  "stack": "V2 react-vite-tailwind",
  "dominant_archetype": "A",
  "second_archetype": "B",
  "mood": "Neo-Tech",
  "sections": [
    {"index": 1, "slot": "S1",  "layout_family": "full-bleed hero",    "archetype": "A", "pattern": "framed-canvas",   "motion": ["hero_reveal_1000ms"],   "media": {"type": "video","asset_ref": "hero_loop.mp4"},          "notes": "Dominant archetype anchor."},
    {"index": 2, "slot": "S2",  "layout_family": "centered statement", "archetype": "D", "pattern": "centered",        "motion": [],                       "media": {"type": "none"},                                        "notes": "Quiet."},
    {"index": 3, "slot": "S4",  "layout_family": "editorial block",    "archetype": "D", "pattern": "editorial-w-clip","motion": ["fade_on_enter"],        "media": {"type": "video","asset_ref": "shake_compare.mp4"},      "notes": "Pain narrative + before/after clip."},
    {"index": 4, "slot": "S5",  "layout_family": "staggered stack",    "archetype": "B", "pattern": "sticky-scroll-scene","motion": ["scroll_scrub_layers"], "media": {"type": "image","asset_ref": "stab_layers/*"},          "notes": "Second signature — sticky cinema."},
    {"index": 5, "slot": "S6",  "layout_family": "card grid",          "archetype": "D", "pattern": "2x3-lite",        "motion": ["hover_lift_soft"],      "media": {"type": "image","asset_ref": "feature_icons/*"},        "notes": "5 tiles + 1 filler card or asymmetric layout."},
    {"index": 6, "slot": "S7",  "layout_family": "staggered stack",    "archetype": "D", "pattern": "alternating-rows","motion": ["stagger_reveal_100ms"], "media": {"type": "image","asset_ref": "scenarios/*"},            "notes": "Second staggered stack, legal (separated from S5 by S6)."},
    {"index": 7, "slot": "S13", "layout_family": "quote panel",        "archetype": "D", "pattern": "single-quote",    "motion": [],                       "media": {"type": "none"},                                        "notes": "One quote per view."},
    {"index": 8, "slot": "S15", "layout_family": "CTA band",           "archetype": "D", "pattern": "centered-cta",    "motion": [],                       "media": {"type": "none"},                                        "notes": "Single primary CTA."}
  ],
  "acceptance_criteria": [
    "First viewport = S1 only.",
    "Primary CTA = 1 (S15).",
    "Signature archetypes = 2 (A + B) — at cap.",
    "Card grid appears once (S6).",
    "No adjacent 'very high' weight sections.",
    "Scroll length 5–8 viewports (slow-burn)."
  ]
}
```

### 5.5 Validation & notes

- ✅ 8 sections; slow-burn allows this length.
- ✅ Two staggered stacks legal because S6 sits between them.
- ✅ Cold traffic → S2 present right after S1 (R1).
- ⚠️ Rich density → editorial-block and staggered-stack preferred; card
  grid limited to one instance.

---

## EXAMPLE 6 — Event Campaign (I6 with details)

### 6.1 Brief

> "Sự kiện conference 1 ngày về AI cho product designers. Muốn bán vé. Có
> lineup 8 speaker, agenda 4 phần, 3 sponsor logo, thời gian + địa điểm."

### 6.2 Blueprint — table

- **Page intent:** I6 Campaign / Event
- **Awareness level:** warm
- **Traffic:** social
- **Narrative spine:** Tease → World → Details → Action
- **Pace:** balanced
- **Density:** balanced
- **Total sections:** 6

| # | Slot | Section name | JTBD | Why here | Layout family | Content required | Visual weight | CTA role |
|---|------|--------------|------|----------|---------------|------------------|---------------|----------|
| 1 | S1 | The Event | Grab + establish identity | first impression | full-bleed hero | event name, date, key visual | very high | soft |
| 2 | S3 | Why This Year | Concrete promise | anchor | centered statement | one-line pitch | medium | none |
| 3 | S7 | Lineup | Show the goods | speakers matter most | card grid | 8 speaker cards | high | none |
| 4 | S5 | Agenda | How the day flows | after speakers | staggered stack | 4 agenda blocks with times | medium | none |
| 5 | S11 | Backed by | Trust anchor | quiet proof | logo strip | 3 sponsor logos | low | none |
| 6 | S15 | Get Tickets | Convert | close | CTA band | ticket CTA + price + venue line | high | primary |

### 6.3 Blueprint — JSON

```json
{
  "blueprint_version": "1.0",
  "page": {
    "intent": "I6",
    "intent_name": "Campaign / Event",
    "awareness": "warm",
    "traffic": "social",
    "narrative_spine": "Tease -> World -> Details -> Action",
    "pace": "balanced",
    "density": "balanced",
    "primary_emotion": "anticipation",
    "total_sections": 6
  },
  "sections": [
    {"index": 1, "slot": "S1",  "name": "The Event",   "jtbd": "grab + identity",    "why_here": "first impression", "layout_family": "full-bleed hero",    "content_required": ["event_name","date","key_visual"], "visual_weight": "very high", "cta_role": "soft"},
    {"index": 2, "slot": "S3",  "name": "Why This Year","jtbd": "concrete promise",   "why_here": "anchor",           "layout_family": "centered statement", "content_required": ["one_line_pitch"],                  "visual_weight": "medium",    "cta_role": "none"},
    {"index": 3, "slot": "S7",  "name": "Lineup",      "jtbd": "show the goods",     "why_here": "speakers matter most","layout_family": "card grid",       "content_required": ["8_speaker_cards"],                 "visual_weight": "high",      "cta_role": "none"},
    {"index": 4, "slot": "S5",  "name": "Agenda",      "jtbd": "how the day flows",  "why_here": "after speakers",   "layout_family": "staggered stack",    "content_required": ["4_agenda_blocks"],                 "visual_weight": "medium",    "cta_role": "none"},
    {"index": 5, "slot": "S11", "name": "Backed by",   "jtbd": "trust anchor",       "why_here": "quiet proof",      "layout_family": "logo strip",         "content_required": ["3_sponsor_logos"],                 "visual_weight": "low",       "cta_role": "none"},
    {"index": 6, "slot": "S15", "name": "Get Tickets", "jtbd": "convert",            "why_here": "close",            "layout_family": "CTA band",           "content_required": ["cta_copy","price","venue_line"],   "visual_weight": "high",      "cta_role": "primary"}
  ],
  "rhythm_rules": [
    "Note: S7 used AS lineup card grid (repurposed) — not use-case scenarios. Legal because slot definition allows 'scenario' framing.",
    "No S6 needed; S7 as card grid absorbs the capability display role.",
    "S11 kept low weight; do not enlarge sponsor logos."
  ],
  "kill_list": [
    "No S8 (philosophy — event page not a manifesto).",
    "No S9 (mood gallery — competes with lineup imagery).",
    "No S13 (past-attendee testimonials would work only if this is repeat event; user didn't provide).",
    "No S14 (FAQ — banned for I6)."
  ],
  "handoff_note": "Anticipation. S1 wants cinematic; S7 speaker cards must feel human, not corporate. Sponsor row stays hushed. Order and layout families are LOCKED.",
  "locked": true
}
```

### 6.4 Build Spec — JSON

```json
{
  "build_spec_version": "1.0",
  "blueprint_ref": "locked",
  "stack": "V2 react-vite-tailwind",
  "dominant_archetype": "A",
  "second_archetype": "F",
  "mood": "Dark Cinematic",
  "sections": [
    {"index": 1, "slot": "S1",  "layout_family": "full-bleed hero",    "archetype": "F", "pattern": "kinetic-type-event-name", "motion": ["marquee_event_name_25s"], "media": {"type": "image","asset_ref": "hero.jpg"},        "notes": "Second archetype (F) used at hero for identity."},
    {"index": 2, "slot": "S3",  "layout_family": "centered statement", "archetype": "D", "pattern": "centered",               "motion": [],                          "media": {"type": "none"},                                 "notes": "Quiet step-down after hero."},
    {"index": 3, "slot": "S7",  "layout_family": "card grid",          "archetype": "D", "pattern": "4x2-portraits",          "motion": ["hover_reveal_role"],       "media": {"type": "image","asset_ref": "speakers/*"},      "notes": "Human portraits, one signature interaction (hover)."},
    {"index": 4, "slot": "S5",  "layout_family": "staggered stack",    "archetype": "D", "pattern": "timeline",               "motion": ["stagger_reveal_100ms"],    "media": {"type": "none"},                                 "notes": "Agenda blocks with times aligned."},
    {"index": 5, "slot": "S11", "layout_family": "logo strip",         "archetype": "D", "pattern": "quiet-row",              "motion": [],                          "media": {"type": "image","asset_ref": "sponsors/*"},      "notes": "Small, quiet."},
    {"index": 6, "slot": "S15", "layout_family": "CTA band",           "archetype": "A", "pattern": "centered-cta-band",      "motion": [],                          "media": {"type": "none"},                                 "notes": "Dominant archetype echoes here for closing weight."}
  ],
  "acceptance_criteria": [
    "First viewport = S1 only.",
    "Primary CTA = 1 (S15).",
    "Signature archetypes = 2 (A + F).",
    "Card grid appears once (S7 lineup).",
    "Awareness gate: warm → S2 not required."
  ]
}
```

### 6.5 Validation & notes

- ✅ 6 sections; balanced pace fits.
- ⚠️ S7 repurposed as lineup card grid rather than use-case scenarios —
  legal because S7's JTBD ("scenario / who this is for") covers "who is
  speaking" for event pages.
- ⚠️ S6 not used; S7-as-grid absorbs the capability display role. This
  keeps only one card grid on the page.
- ⚠️ Warm awareness → S2 legally skipped.

---

## PATTERN LIBRARY — quick lookup

Cross-example patterns worth memorizing:

| Pattern | Rule | Seen in |
|---|---|---|
| Cold + ads → S2 mandatory after S1 | R1 | Ex1 |
| I3 ends with S16, not S15 | Slot rule | Ex2 |
| I4 merges contact into S16 | Slot rule | Ex3 |
| I6 may legally skip S2 despite cold traffic | I6 exception | Ex4 |
| Two editorial blocks back-to-back OK if weight steps | R10 | Ex2 |
| Card grid ≤ 1 per page (except I5) | R6 | Ex1, Ex3, Ex5, Ex6 |
| Trust cluster ≤ 2 of {S11, S12, S13} | Slot rule | Ex1 (S12+S13), Ex6 (S11 only) |
| Motion signatures ≤ 2 per page | Builder cap | all |
| Signature archetypes ≤ 2 per page | Builder cap | all |
| Staggered stack twice legal iff separated by another family | R8 spirit | Ex5 (S5, S7 with S6 between) |
| S7 can absorb lineup/roster role in I6 | I6 flex | Ex6 |

---

## APPENDIX — how to add a new example

1. Start from the brief.
2. Diagnose intent (PHASE 1 of `landing-page-composition-architect`).
3. Fill blueprint table using the 16-slot library.
4. Emit blueprint JSON verbatim from the table.
5. Run PHASE 5 heuristics silently — annotate any rule invoked in
   `rhythm_rules`.
6. Emit build spec JSON referencing the blueprint
   (`cinematic-landing-page` PHASE 1.6).
7. Run `cinematic-landing-page-integration/INTEGRATION.md` §6 validation
   gate; log any near-miss in `Validation & notes`.
8. Add a row to the Pattern Library if a new cross-example pattern emerged.

Never fake an example. Every row of every table must correspond to real
content the user could actually supply.

---

**End of examples.**
