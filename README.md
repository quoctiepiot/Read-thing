# Read-thing

Bộ skill cá nhân cho Claude.

| Skill | Dùng khi |
|---|---|
| [`desire-check`](skills/desire-check/SKILL.md) | Phân biệt cái mình thực sự muốn với cái mình nghĩ mình muốn, trước một quyết định lớn. |
| [`content-value-check`](skills/content-value-check/SKILL.md) | Chấm giá trị một bài viết: đáng đọc không, chắt ra được gì, có câu view không, nên làm gì sau khi đọc. |
| [`insight-capture`](skills/insight-capture/SKILL.md) | Lưu các ý mới và hành động vào database Notion "Read-thing · Insights", gộp ý trùng, tìm lại và theo dõi trạng thái áp dụng. |

Luồng đọc: **content-value-check → insight-capture → (duyệt lại hằng tuần)**.

## Cài lên claude.ai

Mỗi skill là một thư mục có `SKILL.md`. Nén thư mục đó thành zip (thư mục nằm ở gốc file zip) rồi tải lên ở Settings → Skills. Tên skill giữ nguyên nên bản mới sẽ thay bản cũ.

```bash
cd skills && zip -r desire-check.zip desire-check && zip -r content-value-check.zip content-value-check
```
