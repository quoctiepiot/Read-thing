# Agent Hub trên Notion — ID và schema

Tạo ngày 2026-11-26. Đổi tên / chuyển chỗ trên Notion thì ID không đổi; xoá và tạo lại thì cập nhật file này
ở **cả 3 repo** (NPD-Engineering, Assistant, Read-thing), vì mỗi repo giữ một bản copy của skill `hub-sync`.

| Thành phần | Database URL | Data source (dùng để query / tạo dòng) |
|---|---|---|
| Page Agent Hub | `https://app.notion.com/p/42405074f7ed8169a4b7d1b53abf2ef3` | — |
| Tasks | `https://app.notion.com/p/42405074f7ed817887cadcf2552d907f` | `collection://42405074-f7ed-81f4-8501-000b4d5ef55b` |
| Events | `https://app.notion.com/p/42405074f7ed8153b4aef5472d7cf32d` | `collection://42405074-f7ed-81a1-8ccb-000bb99c5274` |
| Agents | `https://app.notion.com/p/42405074f7ed8104b2fde0aafeaf3aae` | `collection://42405074-f7ed-8167-8c5e-000bcd2ea0cb` |

Không tìm thấy ID → `notion-search` "Agent Hub", báo người dùng ID mới để sửa file này.
Schema thực tế khác bảng dưới (người dùng sửa tay) → `notion-fetch` data source, dùng tên cột thực tế,
không tự thêm cột lại.

## Tasks

| Cột | Kiểu | Giá trị |
|---|---|---|
| `Task` | title | Tên việc ngắn, có mã: "FAI review P-4471 Rev C (SUP-001)" |
| `Task ID` | unique id | Tự sinh, hiển thị `HUB-<n>` |
| `Status` | select | `todo` · `claimed` · `in_progress` · `blocked` · `review` · `done` · `cancelled` |
| `Repo` | select | `NPD-Engineering` · `Assistant` · `Read-thing` · `other` |
| `Domain` | select | `general` · `design` · `quality` · `metrology` · `project` · `logistics` · `other` · `personal` |
| `Skill` | text | Skill / chuỗi: `scan-doc-sorter > drawing-extract > fai-review` |
| `Owner` | text | `<repo>/<skill> @ <session>`; trống = chưa ai giữ |
| `Lease until` | date (datetime) | Hết hạn → agent khác được nhận lại |
| `Tags` | text | Mã cách nhau bằng dấu phẩy: `P-4471, SUP-001, CUS-002, <dự án>`. Text, không phải multi-select: multi-select bắt sửa schema mỗi khi có mã mới |
| `Progress` | text | Một dòng tiến độ mới nhất |
| `Next step` | text | Hành động tiếp theo, bắt đầu bằng động từ |
| `Blocker` | text | Đang chờ gì / chờ `HUB-x` |
| `Depends on` / `Blocks` | relation (Tasks ↔ Tasks) | Phụ thuộc giữa các Task |
| `Events` | relation | Tự liên kết từ Events.Task |
| `Output link` | url | Link Drive tới kết quả |
| `Requested by` | select | `user` · `agent` |
| `Updated by` | text | Agent ghi lần cuối |
| `Due` | date | Hạn (nếu có) |
| `Created`, `Last edited` | hệ thống | Chỉ đọc |

## Events (append-only)

| Cột | Kiểu | Giá trị |
|---|---|---|
| `Event` | title | `<type> — <tóm tắt>`: "progress — drawing-extract xong 24 đặc tính, 2 RISK" |
| `Task` | relation → Tasks | Bắt buộc (trừ event chung) |
| `Type` | select | `create` · `claim` · `progress` · `blocker` · `unblock` · `handoff` · `review` · `done` · `release` · `note` · `correction` |
| `Agent` | text | `<repo>/<skill> @ <session>` |
| `Repo` | select | Repo của **agent ghi event** (không phải repo của Task) |
| `Detail` | text | 1–3 dòng, chỉ mã |
| `Link` | url | Link Drive / PR / session |
| `Created` | hệ thống | Thời điểm ghi |

## Agents

| Cột | Kiểu | Giá trị |
|---|---|---|
| `Agent` | title | `<repo>/<skill>` (đã có sẵn 1 dòng cho mỗi skill hiện có) |
| `Repo` | select | như trên |
| `Skills` | text | Skill agent chạy |
| `Surface` | multi-select | `claude.ai` · `Claude Code` · `Cowork` · `scheduled` |
| `Last session` | text | Session gần nhất |
| `Last heartbeat` | date (datetime) | Cập nhật mỗi lần ghi hub |
| `Note` | text | |

Agent mới (skill mới) chưa có dòng → tạo dòng.

## Công cụ Notion

- Tìm Task: `notion-query-data-sources` mode `rows` trên data source Tasks, filter `Status` (select, `enum_is_not`
  `done` / `cancelled`) và `Tags` (text, `string_contains`, vd `P-4471`) hoặc `Task` (title, `string_contains`).
  Mode `sql` cũng được nếu workspace còn quota.
- Tạo Task / Event / Agent: `notion-create-pages` với `parent = {type: data_source_id, data_source_id: <uuid>}`.
  Date: `"date:Lease until:start": "2026-11-26T15:00:00+07:00"`, `"date:Lease until:is_datetime": 1`.
  Relation: mảng URL page, vd `"Task": ["https://app.notion.com/p/<task page id>"]`.
- Sửa Task: `notion-update-page` command `update_properties`. Xoá giá trị: `null`.
- Đọc lại sau claim: `notion-fetch` page Task.
