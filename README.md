# Read-thing

Bộ skill cá nhân cho Claude: lọc trước khi bỏ công, lưu cái đáng giữ, quay lại để làm, và gom thành nguyên tắc của riêng mình.

## Luồng

```
desire-check ──► decision-check ──┐
                                  ├──► insight-capture ──► weekly-review ──► synthesize
content-value-check ──────────────┘          (Notion: Read-thing · Insights)
```

| Skill | Dùng khi | Gõ |
|---|---|---|
| [`desire-check`](skills/desire-check/SKILL.md) | Phân biệt cái mình thực sự muốn với cái mình nghĩ mình muốn. Kết thúc bằng phép thử nhỏ. | "mình có thật sự muốn X không?" |
| [`decision-check`](skills/decision-check/SKILL.md) | Chốt có làm không và làm cách nào: phương án, đảo ngược, pre-mortem, hối tiếc, điều kiện đổi ý. | "chọn A hay B?", "có nên X không?" |
| [`content-value-check`](skills/content-value-check/SKILL.md) | Chấm giá trị một bài viết: đáng đọc không, chắt ra được gì, có câu view không, nên làm gì. | "check bài này" |
| [`insight-capture`](skills/insight-capture/SKILL.md) | Lưu ý mới, hành động, phép thử, quyết định vào Notion; gộp trùng; tìm lại; cập nhật trạng thái. | "lưu", "mình đã lưu gì về X?" |
| [`weekly-review`](skills/weekly-review/SKILL.md) | Hỏi kết quả các dòng tới hạn, cập nhật, báo số liệu tuần, chốt 1–3 ưu tiên. Có thể đặt lịch. | "review tuần" |
| [`synthesize`](skills/synthesize/SKILL.md) | Gom ý về một chủ đề thành trang "Nguyên tắc · <chủ đề>", có nhãn độ chắc. | "tổng hợp X" |
| [`hub-sync`](skills/hub-sync/SKILL.md) | General: ghi / đọc state trên Notion Agent Hub và memory của repo trên Drive, để agent các repo làm song song. | "agent khác đang làm gì?", "cập nhật hub" |

## Dữ liệu và agent hub

| Kho | Ở đâu |
|---|---|
| Insight, phép thử, quyết định, trang Nguyên tắc (sản phẩm của các skill) | Notion `Read-thing · Insights` |
| **Memory** của agent (bài học về cách chạy skill, quy ước người dùng muốn) | Google Drive `AI-Agent-Data/repo Read-thing-Data/memory/` |
| **State / tiến độ** dùng chung với agent repo khác | Notion **Agent Hub**, skill [`hub-sync`](skills/hub-sync/SKILL.md) |

Repo chỉ chứa skill, instruction, hướng dẫn. `hub-sync` là bản copy giống hệt ở repo NPD-Engineering, Assistant.

## Cài lên claude.ai

Mỗi skill là một thư mục có `SKILL.md`. Nén thư mục đó thành zip (thư mục nằm ở gốc file zip) rồi tải lên ở Settings → Skills. Tên skill giữ nguyên nên bản mới sẽ thay bản cũ.

```bash
cd skills && for s in */; do zip -r "${s%/}.zip" "$s"; done
```
