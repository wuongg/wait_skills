# Landing Page Skills

Bộ skill làm landing page, rồi giữ DNA brand cho cả product (dashboard, settings, docs…). Hai pipeline nối nhau bằng Constitution.

```
LANDING
  Brief → Architect → Integration → Cinematic Builder → Landing page
                                                         │ extract DNA
PRODUCT                                                  ▼
  Constitution (tokens + rules)
       → Multi-Page Integration (Page Spec)
       → Page builders theo page-types-catalog (T-01..T-12)
```

## Cấu trúc repo

```
.cursor/skills/
├── CHEATSHEET.md                            ← 1 trang, đọc 5 phút (landing)
├── TESTS.md                                 ← 30 acceptance tests (landing)
│
│ ── Landing pipeline ──
├── landing-page-composition-architect/
│   └── SKILL.md                             ← planner
├── landing-page-skills-integration/
│   └── SKILL.md                             ← Blueprint → Build Spec
├── cinematic-landing-page/
│   ├── SKILL.md                             ← builder v4.1
│   ├── EXAMPLES.md
│   └── PATCH.md
│
│ ── Product / multi-page ──
├── product-design-constitution/
│   └── SKILL.md                             ← extract DNA từ landing
├── page-types-catalog/
│   └── SKILL.md                             ← T-01..T-12 + cinematic budget
└── multi-page-integration/
    └── SKILL.md                             ← Page Spec + chrome contract
```

Docs pipeline (`CHEATSHEET.md`, `TESTS.md`) nằm ở gốc `.cursor/skills/` vì thuộc cả landing pipeline, không gắn một skill.

### Landing

| Skill | Việc làm | Không làm |
|---|---|---|
| **Composition Architect** | Intent, spine, 5–8 section, layout family → Blueprint | Không viết code, không chọn mood/motion |
| **Landing Integration** | Schema Blueprint, map → archetype, validation | — |
| **Cinematic Landing Page** | Archetype A–F, mood, motion, code | Không đổi section đã lock |

### Product (sau landing)

| Skill | Việc làm | Không làm |
|---|---|---|
| **Design Constitution** | Extract tokens + downgrade rules từ landing | Không design từng trang app |
| **Page Types Catalog** | 12 loại trang, budget cinematic, kill list | Không invent type ngoài catalog |
| **Multi-Page Integration** | Page Spec, chrome contract, validation app | Không thay Constitution |

## Cài đặt

**Cách 1 — clone repo**

```bash
git clone https://github.com/wuongg/wait_skills.git
```

Mở folder đó trong agent IDE. Khi hỏi landing page / bố cục / trang giới thiệu / đồng nhất app với landing, skill sẽ được dùng.

**Cách 2 — copy skill sang máy**

```
~/.cursor/skills/
```

(Windows: `%USERPROFILE%\.cursor\skills\`)

Copy các thư mục skill cần dùng (giữ `SKILL.md`). Docs (`CHEATSHEET.md`, `TESTS.md`) copy kèm nếu muốn.

## Tài liệu

| File | Dành cho | Đọc khi |
|---|---|---|
| [`.cursor/skills/CHEATSHEET.md`](.cursor/skills/CHEATSHEET.md) | Người dùng / team | 5 phút nắm landing pipeline |
| [`.cursor/skills/cinematic-landing-page/EXAMPLES.md`](.cursor/skills/cinematic-landing-page/EXAMPLES.md) | Planner + builder | Calibrate Blueprint / Build Spec |
| [`.cursor/skills/TESTS.md`](.cursor/skills/TESTS.md) | Maintainer | Sau mỗi lần sửa rule landing |
| [`.cursor/skills/page-types-catalog/SKILL.md`](.cursor/skills/page-types-catalog/SKILL.md) | App builders | Chọn T-01..T-12 + budget |
| [`.cursor/skills/multi-page-integration/SKILL.md`](.cursor/skills/multi-page-integration/SKILL.md) | App builders | Page Spec trước khi code trang app |
| [`.cursor/skills/cinematic-landing-page/PATCH.md`](.cursor/skills/cinematic-landing-page/PATCH.md) | Maintainer | Changelog builder v4.0 → v4.1 |

## Pipeline làm việc

### A. Landing

Agent **không viết code ngay**. Flow chuẩn:

```
Diagnose intent  →  Blueprint  →  CHỐT  →  Build Spec  →  Code  →  Chỉnh từng phần
```

#### 1. Architect — chốt cấu trúc

Suy ra page intent trước khi hỏi:

| | Intent | Spine gợi ý |
|---|---|---|
| I1 | Launch / Announce | Hook → Value → Proof → CTA |
| I2 | Conversion / Lead-gen | Problem → Solution → Benefits → Trust → CTA |
| I3 | Brand / Editorial | Atmosphere → Philosophy → Signature → World |
| I4 | Portfolio / Studio | Identity → Work → Method → Contact |
| I5 | Product Story | Context → Mechanism → Benefits → Use cases → CTA |
| I6 | Campaign / Teaser | Tease → World → Details → Action |

Rồi đề xuất Composition Blueprint. Reply **ok** / **mặc định đi** / **chốt** để khóa.

Architect **không** bàn archetype cinematic, cursor effect, hay palette.

#### 2. Builder — chốt look rồi build

Sau blueprint, agent hỏi ngắn, khóa Build Spec.

**Sáu archetype:** A Fixed-Viewport · B Sticky Cinema · C Cursor-Effect · D Multi-Section · E Switcher · F Kinetic-Type

**Mood:** Dark Cinematic · Warm Editorial · Neo-Tech · Light Minimal · Light Editorial · Soft Glass

**Stack:** V1 `index.html` (mặc định A/B/C/E/F) · V2 React+Vite+Tailwind (mặc định D)

Chưa **CHỐT** spec thì chưa có file.

#### 3. Nhận file & chỉnh tiếp

- V1: mở `index.html` bằng trình duyệt
- V2: `npm install && npm run dev`

Nói tự nhiên để sửa đúng chỗ. Mỗi lần nhận lại bản đầy đủ.

### B. Product pages (sau landing)

```
Landing xong  →  Constitution lock  →  Page Spec (T-xx)  →  Code trang app
```

1. Extract Constitution từ landing (tokens + downgrade matrix).
2. Chọn page type trong catalog (vd dashboard = T-01, budget 10%).
3. Emit Page Spec theo `multi-page-integration`, validation pass, rồi mới code.
4. Không clone hero landing vào dashboard — sameness từ tokens, không từ section.

## Câu hay dùng

```
Làm landing portfolio studio, mặc định đi.
```

```
Trang launch sản phẩm X, intent I1, mood Dark Cinematic.
Headline ý là "ship faster without the chaos". Chốt rồi build.
```

```
Landing xong rồi. Extract Constitution rồi làm dashboard admin.
```

```
Thêm trang settings + billing, giữ DNA giống landing.
```

## Mẹo

1. Gửi reference (link hoặc tên trang) — nhanh hơn mô tả vibe dài.
2. Reply **mặc định đi** khi lười: agent khóa default hợp lý và đi tiếp.
3. Architect trước, builder sau — đừng xin Features / FAQ trừ khi intent cần.
4. Hero media: tối, loop kín, không watermark; hoặc để agent tìm asset có license.
5. Một mood, tối đa 2 signature interaction trên landing.
6. App pages: tôn trọng cinematic budget; vượt budget = fail dù đẹp.

## Giới hạn

- Architect không viết UI; builder không tự thêm/bớt/đổi thứ tự section đã lock
- Constitution không design trang; page builder không invent token
- Không form backend, analytics, i18n phức tạp
- Hero cần URL hoặc để agent tìm; skill không host video
- Cover desktop / tablet / mobile — không tối ưu email hay in ấn

## License

MIT
