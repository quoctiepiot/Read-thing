# CLAUDE.md — Read-thing

Repo chứa skill, instruction và hướng dẫn cho bộ skill đọc / quyết định / tổng hợp. Chỉ một mình tôi dùng.
Luồng skill và cách cài: `README.md`.

## Dữ liệu không nằm trong repo

| Kho | Ở đâu |
|---|---|
| Insight, phép thử, quyết định, trang Nguyên tắc | Notion `Read-thing · Insights` (skill `insight-capture`, `weekly-review`, `synthesize`) |
| **Memory** của agent — riêng repo này | Google Drive `AI AGENT DATA/repo_read thing data/memory/` |
| **State / tiến độ** của mọi agent (3 repo) | Notion **Agent Hub** (Tasks, Events, Agents) |

Insight của tôi ≠ memory của agent: ý rút ra từ bài đọc → `insight-capture`; bài học về cách skill chạy,
quy ước tôi muốn → memory trên Drive.

Protocol state + memory: skill `hub-sync` (`skills/hub-sync/SKILL.md`). Tóm tắt:
- Đầu task nhiều bước: tìm Task trùng trên hub, nhận việc bằng lease; đọc memory liên quan.
- Update tiến độ của agent khác (repo khác): chỉ ghi **Event**, không ghi đè Status / Owner / Lease.
- Cuối task: cập nhật hub; ghi memory nếu có điều đáng nhớ. Không ghi memory vào repo.
- Ghi hub / memory không cần hỏi.

## Cách làm việc

- Trả lời tiếng Việt, ngắn, kết luận trước.
- `skills/hub-sync/` là bản copy giống hệt ở repo NPD-Engineering và Assistant: sửa thì sửa cả 3.
- **Luôn hỏi trước** khi commit hoặc push; liệt kê file thay đổi và commit message đề xuất.
