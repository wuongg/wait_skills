# Landing Page Skills — Cheatsheet (1 trang)

> **Cho người dùng / team.** Đọc 5 phút là nắm được toàn pipeline. Không cần
> đọc SKILL.md gốc.

---

## Câu chuyện 1 dòng

Trước đây: nói "làm landing page" → skill build nhảy thẳng vào chọn màu,
motion → bố cục section thường bị "thừa / thiếu / sai thứ tự".

Giờ: **hai skill làm hai việc khác nhau**, và một **contract** đứng giữa.

```
brief  →  PLANNER (section gì, thứ tự nào)  →  CONTRACT  →  BUILDER (trông ra sao)
```

---

## 2 skill + 1 contract

| Thành phần | Vai trò | File |
|---|---|---|
| **Planner** | Quyết định *cái gì* & *thứ tự nào*. KHÔNG code. | `landing-page-composition-architect/SKILL.md` |
| **Contract** | Dịch Blueprint → Build Spec. Validation gate. | `landing-page-skills-integration/SKILL.md` |
| **Builder** | Quyết định *trông thế nào* & *chuyển động ra sao*. Code. | `cinematic-landing-page/SKILL.md` (v4.1) |

**Golden rule:** planner sở hữu **structure**, builder sở hữu **surface**.

---

## 6 intent — planner hỏi 1 câu là biết

| Intent | Khi nào dùng | Spine mặc định |
|---|---|---|
| **I1** Launch | Ra mắt brand / sản phẩm mới | Hook → Value → Proof → CTA |
| **I2** Conversion | Lấy lead, sign-up, bán | Problem → Solution → Benefits → Trust → CTA |
| **I3** Brand | Trang premium, editorial, luxury | Atmosphere → Philosophy → Signature → World |
| **I4** Portfolio | Studio, agency, freelancer | Identity → Work → Method → Contact |
| **I5** Product Story | Giải thích cách sản phẩm hoạt động | Context → Mechanism → Benefits → Use cases → CTA |
| **I6** Campaign | Teaser, coming-soon, event | Tease → World → Details → Action |

---

## 16 slot — mọi section đều là 1 trong 16 cái này

**Mở đầu:** S1 Hero · S2 Fast Context · S3 Core Promise
**Giải thích:** S4 Problem · S5 Mechanism · S6 Feature Grid · S7 Use Case
**Cảm xúc:** S8 Philosophy · S9 Mood Gallery · S10 Signature
**Niềm tin:** S11 Logo · S12 Metrics · S13 Testimonials · S14 FAQ
**Kết thúc:** S15 CTA · S16 Soft Footer

**Hard rules:**
- Page dùng **5–8 slot**. Không ít hơn 4. Không nhiều hơn 8 (I5 max 9).
- **S1 bắt buộc.** S15 bắt buộc (trừ I3 dùng S16).
- Không lặp slot. S6 và S9 không được đứng cạnh nhau.
- Trust cluster (S11+S12+S13) tối đa **2 trên 3**.

---

## Blueprint — đầu ra của planner

5 block cố định:

1. **Header** — intent, awareness, spine, pace, density.
2. **Section table** — mỗi dòng 1 section: slot, layout family, content, weight, CTA role.
3. **Rhythm rules** — "không 2 section very-high liên tiếp", "CTA chính chỉ 1", v.v.
4. **Kill list** — cấm cái gì trên trang này.
5. **Handoff note** — 1 đoạn cho builder.

Kết thúc luôn bằng: **"Blueprint locked."**

---

## Layout family — planner nói, builder dịch

15 loại. Planner chọn 1 trong 15. Builder dịch sang archetype A–F.

| Layout family | Archetype hay dùng |
|---|---|
| full-bleed hero | A |
| split hero | A |
| centered statement | D |
| benefit rail | D |
| card grid | D |
| staggered stack | D / B |
| editorial block | D / F |
| mood gallery | B / E |
| logo strip | D |
| metric band | D |
| quote panel | D / A |
| accordion list | D |
| CTA band | D / A |
| sticky footer CTA | D |
| soft footer | D |

**Cap:** tối đa **2 signature archetype** per page. Hero giữ dominant.

---

## Validation — 11 câu hỏi trước khi code

Builder tự hỏi (xem `landing-page-skills-integration/SKILL.md` §6):

- [ ] Section order khớp blueprint?
- [ ] Không thêm/bớt/đổi section?
- [ ] Dominant archetype ở S1?
- [ ] ≤ 2 archetype tổng?
- [ ] ≤ 2 motion signature?
- [ ] Primary CTA = 1 (trừ I3)?
- [ ] Không có item nào trong kill list?
- [ ] Cold traffic ⇒ có S2?
- [ ] Không adjacency cấm (S6+S9, S11+S13)?

Fail 1 cái → dừng, gửi `revision_request` về planner. **Không code luồn.**

---

## Anti-patterns — cả planner và builder đều từ chối

- ❌ "Nhét 12 section."
- ❌ "CTA to ở hero cho cold traffic."
- ❌ "Copy y trang Linear."
- ❌ "Bỏ hero luôn."
- ❌ "Feature grid 12 items."
- ❌ "Cho cả logo + metrics + testimonials + FAQ."
- ❌ "Build tạm đi rồi tính."

Mỗi cái đều có pushback 1 lần; nếu user vẫn ép, ghi `user_override: true`.

---

## Khi nào dùng cái gì

| Bạn muốn… | Dùng |
|---|---|
| Landing page mới từ đầu | Planner → Contract → Builder (full pipeline) |
| Chỉnh màu / typo / hình trên trang đã có | Chỉ Builder (micro-edit exception) |
| Đảo thứ tự section | Quay lại Planner (đây là structure change) |
| Thêm section mới | Quay lại Planner |
| Làm 5 landing page cùng intent | Planner 1 lần → clone blueprint → Builder 5 lần |

---

## Quy trình 3 bước thực tế

```
1. "Tôi cần landing page cho [X]."
        → Planner chạy, trả Blueprint.

2. "Blueprint ok."  (hoặc "sửa section 3 lại")
        → Planner lock, handoff.

3. "Build."
        → Builder emit Build Spec, validation pass, code.
```

Không bước nào được nhảy cóc.

---

## Quick FAQ

**Q: Planner hỏi nhiều không?**
A: Tối đa 2 batch × 4 câu. Nếu brief đã đủ thông tin, planner skip và đề
xuất blueprint luôn.

**Q: Tôi có thể nói "mặc định đi" không?**
A: Có. Mỗi intent có 1 default blueprint đã rhythm-check.

**Q: Builder có được đổi section không?**
A: Không. Section order là law. Builder chỉ được chọn archetype, motion,
mood, stack.

**Q: Muốn thêm slot mới (ví dụ "pricing")?**
A: Slot library là closed. Pricing là content của S15 hoặc S6, không phải
slot mới. Nếu thật sự cần slot mới, đó là decision lớn → sửa
`landing-page-composition-architect/SKILL.md`.

**Q: Patch v4.1 bắt buộc không?**
A: Nếu dùng chung với planner thì bắt buộc. Nếu builder vẫn chạy độc lập
(không qua planner) thì v4.0 vẫn ok.

---

**Đọc xong trang này là dùng được.** Đào sâu: `cinematic-landing-page/EXAMPLES.md`. Regression: `TESTS.md`.
