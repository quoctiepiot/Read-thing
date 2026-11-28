# CLAUDE.md — Read-thing

Repo chứa skill, instruction và hướng dẫn cho bộ skill đọc / quyết định / tổng hợp. Chỉ một mình tôi dùng.
Luồng skill và cách cài: `README.md`.

## Dữ liệu không nằm trong repo

| Kho | Ở đâu |
|---|---|
| Insight, phép thử, quyết định, trang Nguyên tắc | Notion `Read-thing · Insights` (skill `insight-capture`, `weekly-review`, `synthesize`) |
| **Memory** của agent | Notion **Agent Hub → Memory**, cột `Repo = Read-thing` |
| **State / tiến độ** của mọi agent (3 repo) | Notion **Agent Hub** (Tasks, Events, Agents) |

Insight của tôi ≠ memory của agent: ý rút ra từ bài đọc → `insight-capture`; bài học về cách skill chạy,
quy ước tôi muốn → memory (Notion Agent Hub → Memory). Hai database khác nhau, không trộn.

Protocol state + memory: skill `hub-sync`; giao việc / rà các agent: skill `dieu-phoi`. Cả hai **không nằm trong
repo này**: nguồn duy nhất là repo private `agent-core`, cài ở claude.ai Settings → Skills. Tóm tắt:
- Đầu task nhiều bước: tìm Task trùng trên hub, nhận việc bằng lease; đọc memory liên quan.
- Update tiến độ của agent khác (repo khác): chỉ ghi **Event**, không ghi đè Status / Owner / Lease.
- Cuối task: cập nhật hub; ghi memory nếu có điều đáng nhớ. Không ghi memory vào repo.
- Ghi hub / memory không cần hỏi.

## Cách làm việc

- Trả lời tiếng Việt, ngắn, kết luận trước.
- Repo public: không thêm ID Notion / Drive vào repo; ID nằm trong skill `hub-sync` đã cài.
- **Git:** agent tự commit và push lên **nhánh riêng**, rồi mở PR, không cần hỏi. Không push thẳng `main`,
  không tự merge. Tôi duyệt khi merge. Mô tả PR liệt kê file thay đổi và lý do.
