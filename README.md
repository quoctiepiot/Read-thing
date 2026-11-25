# Read-thing

Bộ skill cá nhân cho Claude.

| Skill | Dùng khi |
|---|---|
| [`desire-check`](skills/desire-check/SKILL.md) | Phân biệt cái mình thực sự muốn với cái mình nghĩ mình muốn, trước một quyết định lớn. |
| [`content-value-check`](skills/content-value-check/SKILL.md) | Chấm giá trị một bài viết: đáng đọc không, chắt ra được gì, có câu view không, nên làm gì sau khi đọc. |

## Cài lên claude.ai

Mỗi skill là một thư mục có `SKILL.md`. Nén thư mục đó thành zip (thư mục nằm ở gốc file zip) rồi tải lên ở Settings → Skills. Tên skill giữ nguyên nên bản mới sẽ thay bản cũ.

```bash
cd skills && zip -r desire-check.zip desire-check && zip -r content-value-check.zip content-value-check
```
