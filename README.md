# Cinematic Landing Page

Skill [Cursor](https://cursor.com) làm **trang landing cinematic** — một file `index.html`, không build, không framework.

Agent đóng vai art director: hỏi brief ngắn, chốt spec, rồi mới viết code.

## Cài vào Cursor

**Cách 1 — clone repo này rồi mở bằng Cursor**

```bash
git clone https://github.com/wuongg/wait_skills.git
```

Skill nằm tại:

```
.cursor/skills/deploy-staging/SKILL.md
```

Mở folder đó trong Cursor. Khi bạn hỏi landing page / trang giới thiệu, agent sẽ dùng skill.

**Cách 2 — dùng mọi project**

Copy thư mục skill sang máy bạn:

```
~/.cursor/skills/cinematic-landing-page/
```

(Windows: `%USERPROFILE%\.cursor\skills\cinematic-landing-page\`)

Bên trong chỉ cần `SKILL.md`.

## Khi nào gọi

Nói với agent kiểu:

- “Làm landing page cho sản phẩm X”
- “Trang giới thiệu đẹp, cinematic”
- “Coming soon page premium”
- “Hero page kiểu Linear / Awwwards”

Hoặc gọi thẳng: *dùng skill cinematic landing page*.

## Cách làm việc

Agent **không viết code ngay**. Bốn bước:

```
Hỏi brief  →  Chốt spec  →  Build index.html  →  Chỉnh từng phần
```

### 1. Phỏng vấn

Hỏi từng đợt, tối đa 4 câu. Lười thì trả lời **mặc định** / **tự chọn đi** / **đẹp như Linear** — agent khóa default và đi tiếp.

**Đợt 1 — Sản phẩm & mood**

- Sản phẩm là gì, dành cho ai?
- Chọn mood:

  | | Mood | Cảm giác |
  |---|---|---|
  | A | **Dark Cinematic** | nền đen, chữ bạc, video hero loop — Linear / Vercel / Raycast |
  | B | **Warm Editorial** | giấy kem, serif, ảnh editorial — fashion / architecture |
  | C | **Neo-Tech** | navy/ink, mono sắc, chữ kinetic — dev-tool / crypto |
  | D | **Light Minimal** | trắng, 1 accent, ảnh sản phẩm — Notion / Things |

- Có trang tham chiếu không? (tên hoặc link)
- Headline muốn nói gì? (ý cũng được — agent viết lại)

**Đợt 2 — Copy**

Agent đề xuất headline (2 dòng), subcopy, cặp CTA, mục nav. Duyệt bằng một chữ: *ok*, *chốt*, *đổi …*.

**Đợt 3 — Hero**

| | Nguồn | Ghi chú |
|---|---|---|
| A | Video MP4 của bạn | URL; nên 1080p+, loop mượt, tối, dưới 15MB |
| B | Ảnh tĩnh | URL bạn gửi |
| C | Agent tìm giúp | asset có license, đúng mood |
| D | CSS / SVG | gradient, grain, pan chậm — không cần media |

Kèm 1 câu art direction (*cảnh nên thấy gì*) và vị trí: full-bleed / lệch phải 60% / dưới 40%.

**Đợt 4 — Logo, đối tác, màu**

Logo hình học SVG, dải partner 0–6 mark, palette token. Xác nhận hoặc sửa 1 giá trị.

Nếu tin nhắn đầu đã đủ (brand, mood, copy, asset), agent **bỏ phỏng vấn**, đưa thẳng bảng spec.

### 2. Chốt spec

Bạn thấy một bảng (title, mood, font, màu, hero, headline, CTA, nav). Agent hỏi đúng một câu:

> Chốt spec này chưa? Reply **CHỐT** để tôi build, hoặc nói phần muốn đổi.

Sửa một chỗ: *đổi headline thành …* → bảng cập nhật → hỏi CHỐT lại.

**Chưa CHỐT thì chưa có file.** Đó là cố ý.

### 3. Nhận file

Một `index.html`:

- CSS + JS inline — mở bằng trình duyệt là chạy
- Chỉ tải ngoài: font Google + asset hero (nếu có)
- Desktop: 5 khối — brand mark, nav, pill, copy + CTA, partner strip
- Mobile: menu burger kính mờ, headline xuống dòng, partner 2×2
- Tôn trọng `prefers-reduced-motion`

Agent tóm tắt 3 dòng: đã build gì, hero lấy từ đâu, nên chỉnh gì trước.

Mở file:

```bash
start index.html
```

Hoặc kéo thả vào Chrome / Edge. Xem desktop ở viewport rộng; thu hẹp để kiểm tra menu mobile.

### 4. Chỉnh tiếp

Nói tự nhiên — agent sửa đúng chỗ:

| Bạn nói | Agent làm |
|---|---|
| đổi video | thay hero, giữ fade |
| headline ngắn hơn | viết lại 2 dòng |
| thêm logo | bổ sung mark / partner |
| sáng hơn | nudges palette |
| đổi CTA | đổi nhãn / thứ tự nút |

Mỗi lần nhận lại **cả file**, không phải patch rời.

## Câu hay dùng

```
Làm landing page cinematic cho [sản phẩm], mood Dark Cinematic, mặc định đi.
```

```
Trang coming soon, vibe Linear, headline ý là "ship faster without the chaos".
Video: [URL]. Chốt spec rồi build.
```

```
Đổi video sang [URL mới], headline ngắn hơn, CTA thành "Book a demo".
```

## Mẹo

1. Gửi **reference** (link hoặc tên) — nhanh hơn mô tả vibe dài.
2. Headline: ý ngắn; agent siết còn tối đa 4 từ / dòng.
3. Video hero: tối, loop kín, không watermark, không chữ cháy trên clip.
4. Một mood, một accent. Đừng trộn Dark Cinematic với pastel.
5. Đây là **một composition full-screen**, không phải website nhiều khối. Đừng xin Features / testimonials trừ khi bạn cố ý lệch brief.

## Giới hạn

- Một file HTML — không Next.js, React, CMS
- Không form backend, analytics, i18n phức tạp
- Hero cần URL hoặc để agent tìm; skill không host video
- Cover desktop / tablet / portrait — không tối ưu email hay in ấn

## License

MIT
