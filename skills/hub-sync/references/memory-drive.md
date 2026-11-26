# Memory trên Google Drive

Memory = kinh nghiệm dạng chữ, ngắn, rút ra sau task: **fact** (đặc điểm part / supplier / khách hàng theo mã),
**decision** (quyết định đã chốt), **lesson** (bài học, case tóm tắt), **preference** (quy ước, cách làm người dùng muốn).
Không phải knowledge (cái đúng chung → `knowledge/` hoặc `references/` trong repo), không phải file gốc.

Repo chỉ chứa skill, instruction, hướng dẫn. **Không** ghi memory vào repo.

## Thư mục (tìm bằng ID, tên và vị trí có thể đổi)

| Repo | Skill thuộc repo | Thư mục `memory/` (ID) | Thư mục dữ liệu gốc của repo (ID) |
|---|---|---|---|
| NPD-Engineering | scan-doc-sorter, drawing-extract, fai-review, mọi skill mảng Engineering | `1ZsaNENEhJRrkUwEwqVdegO5r2lEEHu2t` | `1MYhY_QvlNspiYDhLqbvkcRpT_ElHuQxI` (`01_WORK - TTI data/repo NPD-Engineering-History-Data/`; có thêm `registry/`, `cases/`, `files/`) |
| Assistant | thu-ky-du-an | `1URUoawg3uNJsiOCN5e7bpyIMvEx5eRbD` | `15-a4w9pBGE_oHfw4GLRBixGKTvWk6cnE` (`AI AGENT DATA/repo_assistant data/`) |
| Read-thing | desire-check, decision-check, content-value-check, insight-capture, weekly-review, synthesize | `1wqCOSXs2ynSI8y7F6NLREKXr5nD5MEqO` | `1VzVrfLEebfmdBsAcjdKW47zqW_V8nPR3` (`AI AGENT DATA/repo_read thing data/`) |

`hub-sync` tự nó không thuộc repo nào: ghi vào thư mục của repo đang chạy task.
Thư mục không mở được → `search_files` `title = 'memory' and mimeType = 'application/vnd.google-apps.folder'`,
báo người dùng ID mới để sửa file này ở cả 3 repo.

## Một mục = một Google Doc

Connector Drive không sửa được nội dung file đã có, nên mỗi mục memory là **một file mới** (không ghi đè, không xung đột
khi nhiều agent ghi cùng lúc).

**Tên file:** `YYYY-MM-DD | <loại> | <mảng> | <tiêu đề ngắn>`
vd. `2026-11-27 | lesson | quality | SUP-001 hay thiếu cert shot peen trong Form 2`

**Tạo:** `create_file` với `parentId = <ID memory của repo>`, `contentMimeType = text/markdown`, `textContent` theo mẫu
(Drive tự chuyển sang Google Doc).

```markdown
## YYYY-MM-DD — <tiêu đề ngắn>
- Repo: <repo>
- Loại: fact | decision | lesson | preference
- Tag: #<mảng> #<SUP-xxx> #<P-xxxx>
- Nguồn: <task / HUB-id / file>
- Drive: <link file gốc / case đầy đủ nếu có>
- <nội dung 1–5 dòng>
- Thay cho: <tên file mục cũ, nếu có>
- Trạng thái: mở
```

## Đọc

- `search_files` với `'<ID memory>' in ancestors and fullText contains '<P-4471 | SUP-001 | từ khoá>'`.
- Theo loại / mảng: `'<ID memory>' in ancestors and title contains '| lesson | quality |'`.
- Mới nhất trước: `orderBy = modifiedTime desc`. Đọc nội dung: `read_file_content`.
- Xem `description` của file: có "thay thế bởi" / "đã nâng cấp" thì mục đó không còn hiệu lực.

## Sửa, thay thế, nâng cấp

- Không sửa nội dung file cũ. Tạo mục mới có dòng `Thay cho: <tên file cũ>`, rồi `update_file` file cũ với
  `description = "Trạng thái: thay thế bởi <tên file mới>"`.
- Bài học lặp lại 2–3 lần, hoặc làm đổi cách một skill chạy → đề xuất đưa vào `SKILL.md` / `knowledge/` (người dùng
  duyệt, commit repo). Sau khi đã đưa vào: `update_file` với `description = "Trạng thái: đã nâng cấp → <đường dẫn trong repo>"`.

## Quy tắc nội dung

- Supplier / khách hàng ghi bằng mã `SUP-xxx` / `CUS-xxx`. Bảng mã → tên thật chỉ ở `registry/` của NPD.
  Part number ghi nguyên.
- Không giá, không thông tin cá nhân, trừ khi người dùng bảo.
- Case study: memory chỉ giữ tóm tắt (bối cảnh, vấn đề, cách xử lý, bài học); bản đầy đủ ở `cases/` (NPD) hoặc thư mục
  dữ liệu gốc của repo.
- Ghi memory không cần hỏi trước. Tải file gốc (PDF, xlsx, ảnh) lên Drive vẫn phải hỏi.
