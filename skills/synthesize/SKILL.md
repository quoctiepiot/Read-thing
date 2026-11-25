---
name: synthesize
description: >
  Gom các ý đã lưu trong kho Notion "Read-thing · Insights" về một chủ đề thành bộ nguyên tắc của riêng người dùng: nhóm ý gần nhau, xếp theo độ chắc (đã tự kiểm chứng, nhiều nguồn, một nguồn), đặt các ý mâu thuẫn cạnh nhau kèm điều kiện áp dụng, chỉ ra khoảng trống, rồi ghi thành trang Notion "Nguyên tắc · [chủ đề]". Dùng khi người dùng gõ "tổng hợp [chủ đề]", "nguyên tắc của mình về X", "mình đã học được gì về X", "gom các ý về X", "synthesize", hoặc khi weekly-review gợi ý một chủ đề đã đủ dữ liệu. Nếu chỉ muốn xem lại danh sách ý đã lưu → dùng chế độ Tìm lại của insight-capture.
---

# Synthesize

Biến nhiều ý rời rạc đọc từ nhiều nguồn thành **một bộ nguyên tắc ngắn của chính người dùng**, có ghi rõ nguyên tắc nào đã tự kiểm chứng, nguyên tắc nào mới chỉ là đọc được.

---

## Bước 1 — Lấy dữ liệu

1. Tìm database "Read-thing · Insights". Không có → nói thẳng và dừng.
2. Lấy các dòng thuộc chủ đề: theo tag Chủ đề **và** theo từ khóa trong Ý (một ý có thể thuộc chủ đề mà bị gắn tag khác). Bỏ các dòng Trạng thái = Bỏ, **trừ** Phép thử/Quyết định có kết quả "ảo" hay "đổi" — đó là bằng chứng ngược, cần giữ.
3. Ít hơn 5 dòng → không tổng hợp. Nói: *"Mới có N ý về <chủ đề> — chưa đủ để gom thành nguyên tắc."*, liệt kê chúng, và gợi ý lưu thêm.
4. Chủ đề quá rộng (≥40 dòng, nhiều nhánh khác nhau) → đề xuất 2–4 chủ đề con và hỏi một lần làm cái nào, hoặc làm hết.

## Bước 2 — Nhóm ý

Gom thành **3–7 nhóm** theo ý nghĩa, không theo nguồn. Mỗi ý chỉ thuộc một nhóm. Ý lẻ không vào nhóm nào → để ở mục "Ý lẻ".

## Bước 3 — Viết nguyên tắc

Mỗi nhóm → **một nguyên tắc**, viết dạng **KHI … THÌ …** hoặc một quy tắc ngắn hành động được. Không viết khẩu hiệu ("hãy kiên nhẫn").

Gắn độ chắc cho từng nguyên tắc, theo bằng chứng trong kho:

| Nhãn | Điều kiện |
|---|---|
| **[Đã kiểm chứng]** | Có dòng Đã áp dụng kèm kết quả tốt trong Ghi chú, hoặc Phép thử/Quyết định cho kết quả khớp |
| **[Nhiều nguồn]** | Tổng Số lần gặp của các ý trong nhóm ≥3, từ các nguồn khác nhau |
| **[Một nguồn]** | Còn lại |
| **[Bị phản bác]** | Có kết quả tự áp dụng ngược lại |

Kinh nghiệm của chính người dùng thắng ý đọc được: nguyên tắc [Bị phản bác] vẫn ghi, nhưng ghi rõ "áp dụng không hiệu quả với bạn vì …".

Không bịa bằng chứng: nhãn chỉ dựa trên những gì có trong kho.

## Bước 4 — Mâu thuẫn và khoảng trống

- **Mâu thuẫn:** đặt hai ý cạnh nhau. Không chọn bừa một bên — tìm **điều kiện** mỗi bên đúng ("A khi mới bắt đầu, B khi đã có nền"). Không tìm được điều kiện → ghi là câu hỏi mở.
- **Khoảng trống:** chủ đề này còn thiếu gì quan trọng mà kho chưa có? Tối đa 3 câu hỏi mở.
- **Chưa làm:** các Hành động thuộc chủ đề còn Mới lưu / Đang thử — liệt kê, vì nguyên tắc chỉ thành thật khi được thử.

## Bước 5 — Ghi trang Notion

Tên trang: **"Nguyên tắc · <Chủ đề>"**, đặt cạnh database Read-thing · Insights.

Cấu trúc:
```
# Nguyên tắc · <Chủ đề>
Cập nhật <dd/mm/yyyy> · từ N ý, M nguồn

## Nguyên tắc
1. **<KHI … THÌ …>** [Đã kiểm chứng]
   Căn cứ: <ý 1> (<nguồn>), <ý 2> (<nguồn>) · Kết quả tự áp dụng: <nếu có>
2. …

## Mâu thuẫn
- <ý A> ↔ <ý B> → <điều kiện mỗi bên đúng, hoặc "câu hỏi mở">

## Câu hỏi mở
- …

## Chưa thử
- <hành động> — <trạng thái>

## Ý lẻ
- …
```
Mỗi căn cứ liên kết (mention) tới dòng gốc trong database nếu công cụ cho phép.

- **Trang chưa có** → tạo mới, không cần hỏi (tạo trang rẻ và sửa được).
- **Trang đã có** → đọc trước. **Giữ nguyên những gì người dùng tự sửa hoặc tự viết.** Chỉ cập nhật theo kiểu delta: thêm nguyên tắc mới, đổi nhãn độ chắc khi có bằng chứng mới, thêm mâu thuẫn mới, cập nhật ngày. Không viết lại cả trang.

## Bước 6 — Báo cáo trong chat

```
Đã tổng hợp <chủ đề> từ N ý (<link trang>)
Nguyên tắc chắc nhất: <1–2 nguyên tắc [Đã kiểm chứng] hoặc [Nhiều nguồn]>
Mâu thuẫn: <số> · Câu hỏi mở: <số> · Hành động chưa thử: <số>
Nên thử tiếp: <một hành động có thể biến nguyên tắc [Một nguồn] thành [Đã kiểm chứng]>
```

Lỗi khi ghi Notion → vẫn đưa bản tổng hợp trong chat và nói rõ trang chưa được ghi.

## Nguyên tắc

- Ngắn hơn là tốt hơn: 5 nguyên tắc dùng được hơn 15 nguyên tắc đúng.
- Viết bằng tiếng Việt, bằng lời của người dùng khi có thể; giữ thuật ngữ gốc trong ngoặc nếu cần.
- Không thêm kiến thức ngoài kho vào nguyên tắc. Muốn bổ sung thì đưa vào "Câu hỏi mở", ghi rõ là gợi ý ngoài kho.
