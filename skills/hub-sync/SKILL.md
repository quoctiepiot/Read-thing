---
name: hub-sync
description: "General skill: đồng bộ state / tiến độ với Notion Agent Hub (Tasks, Events, Agents) và đọc / ghi memory của repo trên Google Drive, để nhiều agent ở các repo NPD-Engineering, Assistant, Read-thing làm việc song song và cập nhật tiến độ cho nhau. Dùng ở ĐẦU và CUỐI mọi task nhiều bước, task kéo qua nhiều session, chuỗi skill, hoặc khi người dùng hỏi: \"agent khác đang làm gì\", \"tiến độ các agent\", \"task X tới đâu\", \"nhận việc\", \"giao cho agent khác\", \"cập nhật hub\", \"ghi memory\", \"nhớ lại bài học về X\", \"what are the other agents doing\", \"claim / hand off this task\", \"update the hub\", \"save this lesson\". Không dùng cho câu hỏi một lượt không cần theo dõi, không dùng để lưu insight đọc sách (đó là insight-capture), không dùng để lưu file gốc / kết quả (để trên Drive, hub chỉ giữ link)."
---

# Hub sync

Hai kho, hai việc khác nhau:

| Kho | Chứa | Ở đâu |
|---|---|---|
| **State** (dùng chung mọi repo) | Việc gì, ai đang giữ, tới đâu, kẹt gì | Notion page **Agent Hub**: Tasks, Events, Agents |
| **Memory** (riêng từng repo) | Bài học, quyết định, sự thật, quy ước rút ra sau task | Google Drive, thư mục `memory/` của repo đó |

ID, cột, định dạng giá trị: `references/hub-schema.md`. Thư mục memory và mẫu mục: `references/memory-drive.md`.
Đọc cả hai trước lần gọi đầu tiên.

## Quy tắc cứng

1. **Events là nguồn sự thật, chỉ ghi thêm.** Không sửa / xoá event cũ; ghi sai thì thêm event `correction`.
2. **Chỉ Owner đổi `Status`, `Owner`, `Lease until` của Task.** Agent khác (kể cả ở repo khác) cập nhật
   tiến độ bằng cách **ghi Event** gắn vào Task đó. Ngoại lệ: lease đã hết hạn → được nhận lại (Bước 2).
3. **Dữ liệu chỉ dùng mã:** part number, `SUP-xxx`, `CUS-xxx`, tên dự án. Không tên thật supplier / khách hàng,
   không số đo / dung sai chi tiết, không giá, không thông tin cá nhân. Kết quả và file gốc để trên Drive,
   hub chỉ giữ link (`Output link`, `Link`).
4. **Memory chỉ ghi vào thư mục của repo mình.** Đọc memory repo khác được khi liên quan.
5. **Hub không chặn việc chính.** Notion / Drive lỗi → vẫn làm task, cuối kết quả ghi mục
   "Hub chưa cập nhật" liệt kê các thao tác định ghi để chạy lại sau.
6. Ghi hub và ghi memory **không cần hỏi trước**. Tải file gốc lên Drive vẫn phải hỏi.

Tên agent: `<repo>/<skill>` (vd. `NPD-Engineering/fai-review`). Chuỗi skill: dùng skill tiêu thụ cuối.
Định danh phiên: `<agent> @ <session id>`; không có session id thì `@ <surface> <YYYY-MM-DD HH:MM>`.
Giờ: ISO 8601, múi `+07:00` (Asia/Ho_Chi_Minh).

## Bước 1: Đầu task — đọc

1. Tìm Task trùng: query Tasks theo `Tags` (part, mã) và từ khoá tên việc, `Status` khác `done` / `cancelled`.
2. Tìm memory: repo mình trước, theo part number / mã / tag mảng (cách search: `references/memory-drive.md`).
   Mục memory có trạng thái `thay thế` → đọc mục mới hơn.
3. Báo ngắn cho người dùng nếu thấy: việc đã có người giữ, việc phụ thuộc chưa xong, bài học liên quan.

## Bước 2: Nhận việc (claim)

| Tình huống | Làm gì |
|---|---|
| Chưa có Task | Tạo Task: `Status = claimed`, `Owner`, `Lease until = now + 2h`, `Repo`, `Domain`, `Skill`, `Tags`, `Requested by`. Ghi Event `create` rồi `claim`. |
| Task `todo`, không Owner | Ghi `Owner`, `Lease until`, `Status = claimed`. Event `claim`. |
| Có Owner, lease **còn hạn** | **Không nhận.** Báo người dùng ai đang giữ. Muốn góp tiến độ → chỉ ghi Event. |
| Có Owner, lease **hết hạn** | Được nhận lại: Event `claim` ghi rõ "nhận lại từ <owner cũ>, lease hết <giờ>", rồi đổi Owner / Lease. |
| `Depends on` có Task chưa `done` | `Status = blocked`, `Blocker = chờ HUB-x`. Event `blocker`. Không bắt đầu phần phụ thuộc. |

Sau khi ghi claim: **đọc lại Task**. Owner không phải mình (agent khác ghi cùng lúc) → rút lui, ghi Event `note`.

## Bước 3: Trong lúc làm

- Mỗi mốc (xong một skill trong chuỗi, gặp RISK, đổi hướng): Event `progress`, cập nhật `Progress`,
  `Next step`, gia hạn `Lease until`, cập nhật `Last heartbeat` của mình trong Agents.
- Kẹt: `Status = blocked`, `Blocker`, Event `blocker`. Gỡ được: Event `unblock`, `Status = in_progress`.
- Giao lại cho agent khác: Event `handoff` (ghi agent nhận, việc còn lại), `Status = todo`, xoá `Owner`, `Lease until`.
- Việc mới phát sinh cho repo khác: tạo Task mới `Status = todo`, `Requested by = agent`, `Repo` = repo đích.
- RISK chưa giải quyết của bước trước mang sang Event của bước sau, không coi là đã chắc chắn.

## Bước 4: Cuối task — ghi

1. Kết quả cần người dùng quyết (accept / reject, ký, gửi) → `Status = review`. Xong hẳn → `done`.
   Dừng giữa chừng → Event `release`, `Status = todo`, xoá Owner / Lease, ghi `Next step`.
2. `Output link` = link Drive tới kết quả (nếu đã lưu). Event `done` / `review` tóm tắt 1–2 dòng.
3. Có bài học / quyết định / sự thật đáng nhớ → tạo mục memory (mẫu: `references/memory-drive.md`).
   Không có gì đáng nhớ thì không ghi.
4. Cuối kết quả gửi người dùng, thêm một dòng: `Hub: HUB-<id> → <status>` và `Memory: <số mục đã ghi>`.

## Khi người dùng hỏi tiến độ chung

Query Tasks `Status` khác `done` / `cancelled`, nhóm theo Repo. Mỗi Task một dòng:
`HUB-id · Task · Status · Owner · Progress · Next step`. Gắn cờ: lease hết hạn, `blocked` > 2 ngày,
`review` chờ người dùng, Task không đổi > 7 ngày (`Last edited`).
