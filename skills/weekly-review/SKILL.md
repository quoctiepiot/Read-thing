---
name: weekly-review
description: >
  Duyệt lại hằng tuần kho Notion "Read-thing · Insights": hỏi kết quả các hành động, phép thử và quyết định đã tới hạn xem lại, cập nhật trạng thái, báo số liệu tuần, chỉ ra pattern (lưu nhiều mà không làm, dời mãi, chủ đề đủ để tổng hợp) và chốt 1–3 việc ưu tiên cho tuần tới. Dùng khi người dùng gõ "review tuần", "weekly review", "duyệt tuần", "tuần này có gì cần xem lại", "kho insight thế nào rồi", khi một lịch hằng tuần kích hoạt, hoặc khi người dùng muốn đặt lịch review. KHÔNG dùng để review task công việc, lịch họp hay AAR của experience-loop.
---

# Weekly Review

Mắt xích cuối của chuỗi Read-thing: **desire-check / content-value-check / decision-check → insight-capture → weekly-review → synthesize**. Không có bước này, kho chỉ đầy lên chứ không có gì được làm.

Mục tiêu một lần review: **mỗi dòng tới hạn đều có kết quả hoặc quyết định rõ (xong / đang / bỏ / dời có lý do)**, và tuần tới có 1–3 việc ưu tiên. Toàn bộ nên xong trong 10 phút.

---

## Bước 1 — Đọc kho

1. Tìm database "Read-thing · Insights" trong Notion. Không có → nói thẳng *"Chưa có kho — lưu vài bài bằng insight-capture trước đã"* và dừng.
2. Lấy 3 nhóm:
   - **Tới hạn:** Xem lại ≤ hôm nay, Trạng thái là Mới lưu hoặc Đang thử (gồm Hành động, Phép thử, Quyết định)
   - **Mới tuần này:** Ngày lưu trong 7 ngày qua
   - **Số liệu chung:** đếm theo Trạng thái và Loại, đếm theo Chủ đề

## Bước 2 — Hỏi gộp một lượt

Gửi **một tin nhắn**, liệt kê các dòng tới hạn, đánh số, mỗi dòng một câu hỏi ngắn theo loại. Tối đa 10 dòng; nhiều hơn thì ưu tiên Quyết định → Phép thử → Hành động [Làm ngay] → còn lại, và nói rõ còn bao nhiêu dòng để tuần sau.

| Loại | Câu hỏi |
|---|---|
| Hành động | "Xong / đang làm / bỏ / dời?" |
| Phép thử | "Kết quả so với tiêu chí <tiêu chí trong Ghi chú> thế nào?" |
| Quyết định | "Kết quả thực tế so với kỳ vọng <kỳ vọng trong Ghi chú>? Nếu quyết lại hôm nay có chọn như cũ không?" |

Mẫu:
> Tuần này có 5 dòng tới hạn. Trả lời ngắn theo số, ví dụ "1 xong, 2 bỏ, 3 dời 1 tuần":
> 1. [Hành động] Đặt giới hạn 30 phút đọc tin mỗi ngày — xong / đang / bỏ / dời?
> 2. [Phép thử] Part-time 2 tuần ở quán cà phê — kết quả so với tiêu chí "vẫn muốn làm tiếp, không phải cố"?
> 3. [Quyết định] Chọn khóa học A thay vì B — kết quả so với kỳ vọng "dùng được ngay trong việc"? Quyết lại có chọn A không?

Không có dòng nào tới hạn → bỏ qua bước này, sang bước 4.

## Bước 3 — Cập nhật theo câu trả lời

- **Xong** → Đã áp dụng; câu người dùng kể thêm thì ghi vào Ghi chú kèm ngày.
- **Đang** → giữ Đang thử, đặt Xem lại +7 ngày.
- **Bỏ** → Bỏ; ghi lý do một dòng nếu người dùng nói.
- **Dời** → đặt ngày mới, **Số lần dời +1**.
- **Phép thử:**
  - Đạt tiêu chí → Đã áp dụng, ghi "Kết quả: thật". Gợi ý decision-check nếu bước tiếp là chọn cách làm.
  - Không đạt → Bỏ, ghi "Kết quả: ảo — <lý do>". Đây là kết quả tốt: tiết kiệm được một cam kết lớn sai hướng.
  - Không rõ → hỏi đúng một câu: "Nếu phải dừng hẳn từ hôm nay, bạn nhẹ nhõm hay tiếc?"
- **Quyết định:** tách **chất lượng quyết định** khỏi **may rủi** — kết quả xấu chưa chắc là quyết định sai. Ghi vào Ghi chú: kết quả thực tế, "quyết lại: giữ / đổi", và một bài học nếu có. Xong thì Đã áp dụng, hoặc đặt mốc xem lại tiếp nếu chưa đủ dữ liệu.

Dòng nào người dùng không trả lời → **giữ nguyên, không tự đoán kết quả**.

Lỗi khi ghi → nói rõ dòng nào chưa cập nhật được; không báo "đã cập nhật" khi chưa ghi được.

## Bước 4 — Báo cáo tuần

```
Review tuần <dd/mm> · Read-thing · Insights (<link>)
Tuần này: lưu N · áp dụng M · bỏ K · dời L · còn quá hạn Q
Tổng kho: <tổng> ý · tỷ lệ áp dụng hành động: <đã áp dụng>/<tổng hành động đã tới hạn>
Pattern: <chỉ những dòng dưới đây nếu đúng>
Tuần tới ưu tiên: 1. … 2. … 3. …
```

Chỉ dùng số đếm được từ kho; không ước lượng.

**Pattern cần báo (chỉ khi đúng):**
- **Lưu nhiều, làm ít:** tuần lưu ≥10 dòng mà áp dụng 0 → gợi ý lưu ít hơn, chỉ giữ ý gắn với việc đang làm.
- **Dời mãi:** dòng có Số lần dời ≥2 → hỏi thẳng "bỏ hẳn hay làm trong tuần này?". Không có lựa chọn dời lần ba nếu không có lý do mới.
- **Đủ để tổng hợp:** một Chủ đề có ≥8 dòng, hoặc có ý Số lần gặp ≥3 → gợi ý *"Gõ **tổng hợp <chủ đề>** để gom thành nguyên tắc"* (skill synthesize).
- **Quyết định lệch kỳ vọng ≥2 lần cùng kiểu** → nêu kiểu lệch (ví dụ: luôn đánh giá thấp thời gian cần).

## Bước 5 — Chốt ưu tiên tuần tới

Đề xuất 1–3 việc từ các dòng Đang thử / Mới lưu, ưu tiên: sắp tới hạn → gắn với việc đang làm → rẻ và nhanh. Người dùng chọn hoặc sửa; đặt Xem lại +7 ngày cho những việc được chọn.

---

## Đặt lịch hằng tuần

Khi người dùng muốn review tự chạy:
- Hỏi giờ một lần nếu chưa biết; mặc định đề xuất tối Chủ nhật, giờ Việt Nam (Asia/Ho_Chi_Minh).
- Tạo một lịch hằng tuần với lời nhắc chạy weekly-review.
- Khi lịch chạy mà không có người trả lời ngay: **chỉ đọc và gửi danh sách câu hỏi + số liệu, không đổi trạng thái dòng nào**. Cập nhật khi người dùng trả lời.

## Tone

- Gọn. Đây là việc 10 phút, không phải buổi coaching.
- Không trách móc vì làm ít; nói số liệu và đề xuất một điều chỉnh cụ thể.
- Bỏ một việc là kết quả hợp lệ, không phải thất bại.
