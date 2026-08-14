# Landing Page Skills

Bộ skill làm landing page theo pipeline hai bước: **architect** quyết định cấu trúc, **builder** quyết định look & motion rồi mới viết code. Skill `landing-page-skills-integration` là hợp đồng handoff giữa hai bên.

```
Brief
  → Composition Architect   (WHAT / ORDER / DENSITY)
  → Integration Contract    (Blueprint → Build Spec)
  → Cinematic Builder       (HOW IT LOOKS / MOVES / CODE)
  → Shipped page
```

## Cấu trúc repo

```
.cursor/skills/
├── CHEATSHEET.md                          ← 1 trang, đọc 5 phút
├── TESTS.md                               ← 30 acceptance tests (pipeline)
├── landing-page-composition-architect/
│   └── SKILL.md                           ← planner
├── landing-page-skills-integration/
│   └── SKILL.md                           ← contract / validation
└── cinematic-landing-page/
    ├── SKILL.md                           ← builder v4.1
    ├── EXAMPLES.md                        ← 6 case studies
    └── PATCH.md                           ← changelog v4.0 → v4.1
```

`CHEATSHEET.md` và `TESTS.md` nằm ở gốc `.cursor/skills/` vì chúng thuộc **cả pipeline**, không gắn một skill.

| Skill | Việc làm | Không làm |
|---|---|---|
| **Composition Architect** | Intent, narrative spine, 5–8 section, layout family, rhythm, kill list → Composition Blueprint | Không viết code, không chọn mood/motion/archetype |
| **Cinematic Landing Page** | Archetype A–F, mood, motion, stack, viết HTML hoặc React | Không đổi số section / thứ tự / JTBD của blueprint |
| **Integration** | Schema Blueprint, map layout family → archetype, invariant, failure modes | — |

## Cài đặt

**Cách 1 — clone repo**

```bash
git clone https://github.com/wuongg/wait_skills.git
```

Mở folder đó trong agent IDE. Khi hỏi landing page / bố cục / trang giới thiệu, skill sẽ được dùng.

**Cách 2 — copy skill sang máy**

```
~/.cursor/skills/
```

(Windows: `%USERPROFILE%\.cursor\skills\`)

Copy cả ba thư mục skill ở trên vào đó (giữ nguyên cấu trúc `SKILL.md`). `CHEATSHEET.md` và `TESTS.md` copy kèm nếu muốn dùng trên máy.

## Tài liệu

| File | Dành cho | Đọc khi |
|---|---|---|
| [`.cursor/skills/CHEATSHEET.md`](.cursor/skills/CHEATSHEET.md) | Người dùng / team | 5 phút nắm pipeline, 6 intent, 16 slot, anti-pattern |
| [`.cursor/skills/cinematic-landing-page/EXAMPLES.md`](.cursor/skills/cinematic-landing-page/EXAMPLES.md) | Planner + builder | Calibrate blueprint / Build Spec (6 case) |
| [`.cursor/skills/TESTS.md`](.cursor/skills/TESTS.md) | Maintainer | Sau mỗi lần sửa rule planner hoặc validation (30 test) |
| [`.cursor/skills/cinematic-landing-page/PATCH.md`](.cursor/skills/cinematic-landing-page/PATCH.md) | Maintainer | Changelog builder v4.0 → v4.1 |

## Pipeline làm việc

Agent **không viết code ngay**. Flow chuẩn:

```
Diagnose intent  →  Blueprint  →  CHỐT  →  Build Spec  →  Code  →  Chỉnh từng phần
```

### 1. Architect — chốt cấu trúc

Suy ra page intent trước khi hỏi:

| | Intent | Spine gợi ý |
|---|---|---|
| I1 | Launch / Announce | Hook → Value → Proof → CTA |
| I2 | Conversion / Lead-gen | Problem → Solution → Benefits → Trust → CTA |
| I3 | Brand / Editorial | Atmosphere → Philosophy → Signature → World |
| I4 | Portfolio / Studio | Identity → Work → Method → Contact |
| I5 | Product Story | Context → Mechanism → Benefits → Use cases → CTA |
| I6 | Campaign / Teaser | Tease → World → Details → Action |

Rồi đề xuất Composition Blueprint (section, layout family, visual weight, kill list). Reply **ok** / **mặc định đi** / **chốt** để khóa.

Architect **không** bàn archetype cinematic, cursor effect, hay palette — đó là việc của builder.

### 2. Builder — chốt look rồi build

Sau blueprint (hoặc brief đủ nếu chỉ gọi builder), agent hỏi ngắn (tối đa 4 câu / đợt), rồi khóa Build Spec.

**Sáu archetype**

| | Tên | Phù hợp |
|---|---|---|
| A | Fixed-Viewport Hero | Launch, coming soon, một composition |
| B | Sticky Cinema Scroll | Story nhiều cảnh, fashion / destination |
| C | Cursor-Effect Hero | Portfolio, poster tương tác |
| D | Multi-Section Studio | Studio / agency nhiều khối |
| E | Switcher Hero | Team, lookbook, crossfade |
| F | Kinetic-Type Poster | Portfolio cá nhân, chữ lớn chạy |

**Mood:** Dark Cinematic · Warm Editorial · Neo-Tech · Light Minimal · Light Editorial · Soft Glass

**Stack**

- **V1** — một file `index.html` (CSS/JS inline) — mặc định cho A/B/C/E/F
- **V2** — React + Vite + Tailwind (+ motion/GSAP) — mặc định cho D hoặc trang sẽ mở rộng

Chưa **CHỐT** spec thì chưa có file.

### 3. Nhận file & chỉnh tiếp

- V1: mở `index.html` bằng trình duyệt
- V2: `npm install && npm run dev`

Nói tự nhiên để sửa đúng chỗ (*đổi headline*, *video khác*, *bớt section*, *CTA thành …*). Mỗi lần nhận lại bản đầy đủ, không patch rời.

## Câu hay dùng

```
Làm landing portfolio studio, mặc định đi.
```

```
Trang launch sản phẩm X, intent I1, mood Dark Cinematic.
Headline ý là "ship faster without the chaos". Chốt rồi build.
```

```
Chỉ cần blueprint trước — đừng code. Intent conversion, 5–6 section.
```

```
Đổi video sang [URL], headline ngắn hơn, CTA thành "Book a demo".
```

## Mẹo

1. Gửi reference (link hoặc tên trang) — nhanh hơn mô tả vibe dài.
2. Reply **mặc định đi** khi lười: agent khóa default hợp lý và đi tiếp.
3. Architect trước, builder sau — đừng xin Features / FAQ / metric band trừ khi intent thật sự cần.
4. Hero media: tối, loop kín, không watermark; hoặc để agent tìm asset có license.
5. Một mood, tối đa 2 signature interaction. Đừng trộn Dark Cinematic với pastel.

## Giới hạn

- Architect không viết UI; builder không tự thêm/bớt/đổi thứ tự section đã lock
- Không form backend, analytics, i18n phức tạp
- Hero cần URL hoặc để agent tìm; skill không host video
- Cover desktop / tablet / mobile — không tối ưu email hay in ấn

## License

MIT
