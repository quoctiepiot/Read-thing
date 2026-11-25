---
name: content-value-check
description: >
  Chấm giá trị thực của một bài viết, bài báo, thread, newsletter, video transcript hay nội dung văn bản: đáng đọc không, chắt ra được gì, có câu view không, gợi ra hành động gì. Dùng khi người dùng muốn ĐÁNH GIÁ nội dung chứ không chỉ tóm tắt: "bài này có gì hay không?", "đáng đọc không?", "check bài này", "bài này có hữu ích không?", "có phải clickbait không?", "tin được không?", "value check", "phân tích bài viết", hoặc gửi nhiều bài và hỏi nên đọc bài nào. Nếu người dùng chỉ xin tóm tắt / ý chính / TL;DR mà không hỏi giá trị hay độ tin cậy → dùng summarize-content, không dùng skill này.
---

# Content Value Check

Mục đích: đưa **phán quyết**, không phải tóm tắt — bài này có đáng thời gian của người dùng không, nó cho gì, tin được tới đâu, và đọc xong nên làm gì.

---

## Bước 0 — Lấy nội dung

- Text được paste vào / file → dùng trực tiếp (PDF, DOCX: đọc bằng skill tương ứng).
- URL → fetch trang. **Không fetch được thì nói rõ, không đoán nội dung từ tiêu đề.** Có thể đánh giá riêng tiêu đề nếu người dùng muốn, nhưng phải ghi là "chỉ dựa trên tiêu đề".
- Screenshot → đọc ảnh.
- Chỉ có một đoạn trích → ghi rõ verdict chỉ áp dụng cho đoạn đó.

## Bước 1 — Chọn độ dài output

| Nội dung | Format |
|---|---|
| Ngắn (dưới ~400 chữ, một post/thread ngắn) | **Bản gọn**: Verdict + Tinh chất + Câu view + Hành động, mỗi phần 1–3 dòng |
| Dài (bài báo, newsletter, blog, transcript) | **Bản đầy đủ** bên dưới |
| Nhiều bài cùng lúc | **Bảng so sánh** (xem cuối file) |

Phần "Phân tích bổ sung" chỉ viết những mục thực sự có điều để nói.

---

## Format bản đầy đủ

### 🎯 VERDICT: <một câu duy nhất, có góc độ>
Ví dụ: *"Đọc kỹ nếu bạn đang định X — phần 3 là thứ khó tìm ở chỗ khác"*, *"Lướt 2 đoạn cuối là đủ"*, *"Bỏ qua — tiêu đề hứa nhiều hơn nội dung có"*.

Kèm một dòng chỉ số:
```
Đọc mất: ~N phút · Ý đáng giữ: K · Mật độ: Cao / Trung bình / Thấp · Độ tin cậy: Cao / Trung bình / Thấp
```
- **Ý đáng giữ** = số bullet ở phần Tinh chất (đếm được, không bịa).
- **Mật độ** = ý đáng giữ so với thời gian đọc. Mốc tham khảo: ≥1 ý / 2 phút = Cao; ~1 ý / 5 phút = Trung bình; ít hơn = Thấp.
- **Không dùng phần trăm** (kiểu "62% thực chất") — đó là độ chính xác giả.

### 📦 TINH CHẤT
Chỉ các điểm có giá trị thật, mỗi bullet = một insight / fact / framework **áp dụng được hoặc đáng nhớ lâu**. Đánh dấu:
- **[Mới]** — ít người biết, khó tìm ở chỗ khác
- **[Quen]** — đúng nhưng phổ biến (chỉ giữ nếu được trình bày đặc biệt hữu ích)

Không có gì đáng giữ → viết thẳng *"Không có ý nào đáng giữ."*

### 🎣 CÂU VIEW? CÓ / KHÔNG / MỘT PHẦN
Kiểm tra:
- Tiêu đề phóng đại, số mơ hồ ("7 bí quyết"), kích cảm xúc, "ai cũng mắc lỗi này"?
- Nội dung có deliver đúng điều tiêu đề hứa không?
- Cliffhanger, FOMO, vague authority ("chuyên gia nói", "nghiên cứu chỉ ra")?
- Câu chuyện cảm xúc lấn át thông tin?
- Có bán gì ở cuối (khóa học, sản phẩm, affiliate, kêu gọi follow)?

CÓ hoặc MỘT PHẦN → nêu **thủ thuật cụ thể**, trích câu làm ví dụ. Câu view không tự động có nghĩa là vô giá trị — nội dung vẫn chắc thì ghi nhận cả hai.

### ⚡ HÀNH ĐỘNG GỢI RA
- **[Làm ngay]** → ...
- **[Tìm hiểu thêm]** → ...
- **[Áp dụng khi]** → ...
- **[Tránh / Dừng]** → ...

Chỉ liệt kê hành động cụ thể, kiểm chứng được. "Hãy suy nghĩ tích cực hơn" không tính. Không có → *"Không có hành động rõ ràng — bài mang tính giải trí / tổng quan / truyền cảm hứng."*

### 🔍 PHÂN TÍCH BỔ SUNG (chỉ mục nào có điều để nói)

**Độ tin cậy & claim cần kiểm**
- Tác giả có chuyên môn thật hay chỉ là "người đã trải qua"? Có xung đột lợi ích không?
- Số liệu có nguồn không? Liệt kê **tối đa 3 claim quan trọng nhất** mà bài dựa vào, mỗi cái gắn: *Có nguồn / Không nguồn / Đáng ngờ*.
- Nếu có công cụ tìm web và claim ảnh hưởng tới quyết định (sức khỏe, tiền bạc, pháp lý) → kiểm nhanh 1–2 claim then chốt và ghi kết quả. Không kiểm được thì ghi "chưa kiểm".

**Bias & lỗ hổng**
- Bài đang quảng bá gì (sản phẩm, quan điểm, lối sống)?
- Survivorship bias, nhầm tương quan với nhân quả, chỉ trưng ví dụ thuận lợi, bỏ qua phản biện lớn?

**Độ sâu & đối tượng**
- Rộng-nông hay hẹp-sâu? Hợp với người mới / trung cấp / nâng cao?

**Tuổi thọ thông tin**
- Còn đúng sau 5 năm không, hay phụ thuộc thị trường, công nghệ, chính sách tại một thời điểm? Ghi ngày đăng nếu thấy, và flag nếu thông tin có thể đã cũ.

---

## Bảng so sánh (khi có nhiều bài)

```
| # | Bài | Verdict ngắn | Ý đáng giữ | Mật độ | Tin cậy | Câu view |
|---|-----|--------------|-----------|--------|---------|----------|
```
Sau bảng: **Đọc bài nào trước** (một câu), và những ý mà chỉ một bài có (nếu các bài trùng nhau nhiều).

---

## Nguyên tắc chấm

1. **Không hào phóng với phần độn.** Mở bài 3 đoạn để nói một ý = độn.
2. **Insight ≠ thông tin.** Điều ai cũng biết không tính là giá trị.
3. **Hành động mơ hồ không được tính.**
4. **Verdict phải có góc độ.** "Bài có điểm mạnh và điểm yếu" = không có verdict.
5. **Không bịa chỉ số.** Chỉ đưa con số đếm hoặc ước được (thời gian đọc, số ý); còn lại dùng mức Cao / Trung bình / Thấp.
6. **Biết người đọc thì cá nhân hóa.** Nếu biết bối cảnh của người dùng (nghề, mục tiêu, dự án đang làm), verdict nói bài này có giá trị với *họ* tới đâu, không chỉ giá trị chung.

## Tone
- Thẳng, không khách sáo. Bài dở → nói thẳng vì sao. Bài hay → chỉ đúng chỗ hay.
- Không hedging kiểu "tùy người đọc", "mỗi người một góc nhìn".
- Trả lời bằng ngôn ngữ người dùng đang dùng, kể cả khi bài viết bằng tiếng khác.
