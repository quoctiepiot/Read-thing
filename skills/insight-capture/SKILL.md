---
name: insight-capture
description: >
  Lưu những ý đáng giữ và hành động rút ra từ bài viết, video, sách, thread — cùng các phép thử (từ desire-check) và quyết định (từ decision-check) — vào database Notion "Read-thing · Insights", tìm lại những gì đã lưu, và cập nhật trạng thái áp dụng. Dùng khi người dùng nói "lưu bài này", "lưu lại", "lưu ý này", "lưu phép thử", "lưu quyết định", "ghi vào Notion", "save insight", "lưu vào kho", nhất là ngay sau một lần content-value-check, desire-check hoặc decision-check; khi hỏi "mình đã lưu/đọc gì về X?", "tìm lại ý về X"; hoặc khi báo "đã áp dụng …", "bỏ ý …", "đang thử …". KHÔNG dùng để lưu ghi chú họp, tài liệu công việc hay task list thông thường.
---

# Insight Capture

Vòng đầy đủ: **đọc → chấm (content-value-check) → lưu (skill này) → áp dụng → duyệt lại**. Skill này lo bước lưu: biến những gì đã chắt lọc thành các dòng Notion nhỏ, tìm được, không trùng, và có trạng thái để theo dõi.

Ba chế độ:
- **Lưu** — "lưu bài này", "lưu lại"
- **Tìm lại** — "mình đã lưu gì về X?"
- **Cập nhật** — "đã áp dụng ý X", "bỏ ý Y", "đang thử Z"

---

## Database: "Read-thing · Insights"

**Mỗi dòng = một ý** (không phải một bài) — để tìm theo ý, gộp trùng giữa nhiều nguồn, và theo dõi từng hành động.

| Thuộc tính | Kiểu | Ghi chú |
|---|---|---|
| **Ý** | Title | Một câu, tự đứng được khi đọc lại sau 6 tháng không cần bài gốc |
| **Loại** | Select | Insight · Fact · Framework · Hành động · Phép thử · Quyết định |
| **Độ mới** | Select | Mới · Quen |
| **Chủ đề** | Multi-select | 1–3 tag; dùng lại tag đã có trước khi tạo tag mới |
| **Nguồn** | Text | Tên bài — tác giả/kênh |
| **URL** | URL | Nếu có |
| **Ngày lưu** | Date | Hôm nay |
| **Trạng thái** | Select | Mới lưu · Đang thử · Đã áp dụng · Bỏ |
| **Xem lại** | Date | Chỉ cho Hành động (xem bảng dưới) |
| **Số lần gặp** | Number | Mặc định 1; tăng khi nguồn khác nói cùng ý |
| **Nguồn khác** | Text | Các nguồn sau nói cùng ý |
| **Số lần dời** | Number | Mặc định 0; tăng mỗi lần dời ngày Xem lại |
| **Ghi chú** | Text | Bối cảnh áp dụng, phản biện, verdict bài; với Phép thử/Quyết định: xem mục dưới |

Hạn **Xem lại** cho Hành động:
- [Làm ngay] → +7 ngày
- [Tìm hiểu thêm] → +14 ngày
- [Áp dụng khi] → để trống (áp dụng theo tình huống)
- [Tránh / Dừng] → +30 ngày (kiểm xem đã bỏ được chưa)
- Phép thử → ngày kết thúc phép thử
- Quyết định → ngày xem lại mà decision-check đã đặt (mặc định +90 ngày)

### Phép thử và Quyết định

Hai loại này đến từ skill khác, không phải từ bài đọc. Nguồn ghi "desire-check" / "decision-check" kèm ngày.

| Loại | Ý (title) | Ghi chú phải có |
|---|---|---|
| **Phép thử** | "Thử: <cách thử> — để kiểm <mong muốn>" | Giả thuyết · Tiêu chí thành công (kết quả nào nghĩa là desire thật) · Thời hạn |
| **Quyết định** | "Quyết: chọn <X> thay vì <Y>" | Kỳ vọng (sẽ thấy gì nếu đúng) · Điều kiện đổi ý · Mức tự tin lúc quyết |

Trạng thái ban đầu: Phép thử → **Đang thử**; Quyết định → **Mới lưu**. Không kiểm trùng với ý đọc; chỉ kiểm trùng với Phép thử/Quyết định đang mở cùng chủ đề.

### Tìm hoặc tạo database

1. Tìm trong Notion theo tên "Read-thing · Insights".
2. Thấy → dùng. Thấy nhiều cái cùng tên → hỏi một lần dùng cái nào.
3. Không thấy → nói một dòng *"Chưa có database Read-thing · Insights — mình tạo một database riêng tư với các cột trên nhé?"*, rồi tạo khi người dùng đồng ý. Chỉ hỏi lần đầu; sau đó cứ dùng.
4. Database thiếu cột (người dùng đã sửa tay) → ghi vào những cột còn có, đừng tự thêm cột lại.

---

## Chế độ Lưu

### Bước 1 — Lấy danh sách ý

- **Vừa chạy content-value-check trong chat** → lấy trực tiếp: bullet Tinh chất (kèm nhãn [Mới]/[Quen]) và các dòng Hành động.
- **Chưa check** → không chạy lại cả bản đầy đủ. Chỉ chắt nhanh: các ý [Mới] và hành động cụ thể. Không có nội dung bài trong chat → xin nội dung hoặc link.
- **Người dùng chỉ định** ("lưu ý số 2 và 4", "chỉ lưu hành động") → làm đúng như vậy.
- **Vừa chạy desire-check / decision-check** → lưu một dòng Phép thử hoặc Quyết định theo mục trên. Thiếu tiêu chí thành công / kỳ vọng → hỏi đúng một câu trước khi ghi, vì thiếu nó thì weekly-review không chấm được.

### Bước 2 — Lọc

- Mặc định lưu: mọi ý **[Mới]** và mọi **Hành động** cụ thể.
- Ý **[Quen]**: bỏ, trừ khi người dùng bảo lưu hoặc nó gắn trực tiếp với việc họ đang làm.
- Tối đa khoảng **7 dòng mỗi bài**. Hơn thế thì gộp những ý gần nhau.
- Viết lại mỗi ý thành **một câu tự đứng được**: có chủ ngữ, có điều kiện nếu cần ("Khi X thì Y"), không dùng "như trên", "điều này".
- **Không lưu dữ liệu mật** (giá nhà cung cấp, số liệu khách hàng, bản vẽ, tên người, tài liệu nội bộ). Nếu nguồn là tài liệu công việc → viết ý ở dạng trừu tượng, hoặc hỏi trước khi lưu.

### Bước 3 — Kiểm trùng

Với mỗi ý, tìm trong database theo 2–3 từ khóa chính.
- **Trùng ý** (cùng nội dung, khác chữ) → không tạo dòng mới: tăng **Số lần gặp**, thêm nguồn mới vào **Nguồn khác**. Một ý gặp lại từ nhiều nguồn là tín hiệu nó đáng tin hơn — nói ra điều đó khi báo cáo.
- **Gần giống nhưng có thêm điều mới** → tạo dòng mới, ghi "Mở rộng từ: <ý cũ>" vào Ghi chú.
- **Mâu thuẫn với ý đã lưu** → vẫn lưu, ghi "Ngược với: <ý cũ>" vào Ghi chú, và nêu ra khi báo cáo.

### Bước 4 — Ghi và báo cáo

Ghi luôn, không cần hỏi xác nhận (ghi vào Notion rẻ và sửa được). Sau khi ghi, báo gọn:

```
Đã lưu vào Read-thing · Insights (<link>): thêm N · gộp M · bỏ K
1. [Insight · Mới] <ý>
2. [Hành động · xem lại 02/12] <ý>
3. [Gộp ×3] <ý> — giờ đã gặp ở 3 nguồn
⚠ Ngược với ý đã lưu: <…>   (chỉ khi có)
Sai dòng nào thì nói "bỏ dòng 2" hoặc "sửa dòng 1 thành …".
```

Không bao giờ báo "đã lưu" nếu lệnh ghi lỗi — nói rõ dòng nào chưa ghi được và vì sao.

---

## Chế độ Tìm lại

"Mình đã lưu gì về X?", "có ý nào về Y không?"

1. Tìm trong database theo X (cả theo Chủ đề và theo nội dung Ý).
2. Trả về tối đa 10 dòng, ưu tiên: Số lần gặp cao → Độ mới = Mới → mới lưu gần đây.
3. Format: `• <ý> — <nguồn>, <ngày> · <trạng thái>`; gom theo Loại nếu nhiều.
4. Kết thúc bằng **một câu tổng hợp**: những ý này cộng lại nói gì, và có mâu thuẫn nào không.
5. Không thấy gì → nói thẳng; đừng lấp bằng kiến thức chung mà không ghi rõ là "không có trong kho".

## Chế độ Cập nhật

"Đã áp dụng ý X", "bỏ ý Y", "đang thử Z", "dời lịch xem lại".

1. Tìm dòng khớp. Nhiều dòng khớp → liệt kê ngắn, hỏi dòng nào.
2. Cập nhật **Trạng thái** (và **Xem lại** nếu có; dời ngày thì tăng **Số lần dời**). Người dùng kể kết quả ("áp dụng rồi, hiệu quả", "thử rồi, không hợp") → ghi một dòng vào Ghi chú kèm ngày.
3. Xác nhận một dòng: `✓ <ý> → Đã áp dụng`.

---

## Nguyên tắc

- Một câu một ý, đọc lại sau 6 tháng vẫn hiểu.
- Ít mà dùng được hơn nhiều mà không bao giờ mở lại.
- Kho là của người dùng: không tự xóa dòng; "bỏ" = đổi Trạng thái thành Bỏ, trừ khi được bảo xóa hẳn.
- Trả lời bằng tiếng Việt, kể cả khi nguồn bằng tiếng khác; giữ thuật ngữ gốc trong ngoặc nếu cần.
