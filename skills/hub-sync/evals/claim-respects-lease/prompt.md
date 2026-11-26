---
tags: [skill-creator]
max_turns: 20
timeout_seconds: 600
allowed_tools: [Read, Glob, Grep, Skill, Write, Edit, Bash]
---

Bạn là agent `NPD-Engineering/fai-review`, session `session_D`. Bây giờ là 2026-11-27T10:00:00+07:00.

Mình muốn tiếp tục review FAI cho P-4471 Rev C. Thêm 2 việc:
- Báo cho task nhắc việc HUB-4 bên Assistant: supplier Minh Phát (mã SUP-001) đã gửi bổ sung cert shot peen sáng nay.
- Ghi memory: đây là lần thứ 2 SUP-001 gửi thiếu cert shot peen ở lần nộp FAI đầu.

Môi trường này không có Notion và Google Drive. State hiện tại của Agent Hub nằm trong hub_snapshot.json.
Dùng skill hub-sync, ghi mọi thao tác hub và memory định thực hiện vào out/hub_ops.json (mảng JSON, mỗi phần tử có
`tool`, `target`, và `properties` hoặc `content`), rồi trả lời ngắn. Không cần hỏi lại.

Input files: hub_snapshot.json
