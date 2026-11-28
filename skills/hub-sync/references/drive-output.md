# Lưu kết quả task lên Google Drive

Áp dụng khi agent tải **kết quả của một task người dùng giao** lên Drive: report, kết quả tính toán, xlsx đặc tính,
PDF đã tách… Mục đích: người dùng nhìn tên là biết tài liệu nào, cập nhật ngày nào, phiên bản mấy.
Không áp dụng cho memory (`memory-drive.md`) và state (Notion Agent Hub).

## Quy tắc đặt tên

Mỗi lần cập nhật = **một folder phiên bản mới**, file bên trong mang cùng tên + ngày.

| | Mẫu | Ví dụ |
|---|---|---|
| Folder phiên bản | `<Loại>_<mã>_<MM.DD.YYYY>[_vN]` | `ECNs/ECN_015033003_11.28.2026/` |
| File | `<Loại>_<mô tả> <mã>_<MM.DD.YYYY>[_vN].<ext>` | `ECN_design release 015033003_11.28.2026.pdf` |

- `<Loại>`: viết tắt loại tài liệu — `ECN`, `FAI`, `8D`, `MSA`, `CALC`, `REPORT`…
- `<mã>`: số ECN, hoặc part number + rev. Không có mã → tên ngắn của task.
- `<mô tả>`: vài chữ nói file là gì, được giữ khoảng trắng. Các phần cố định nối bằng `_`.
- **Ngày** = ngày cập nhật / tải lên, múi `+07:00`. Định dạng `MM.DD.YYYY`, luôn đủ 2 chữ số (`01.05.2027`).
  Khác với `YYYY-MM-DD` của tên memory — không lẫn.
- **Trùng ngày** (đã có bản cùng `<Loại>_<mã>_<ngày>`): thêm `_v2`, `_v3`… sau ngày, cho **cả folder và file**.
  Không ghi đè, không xoá bản cũ.

Ví dụ khác:
- `FAI_P-4471 RevC_11.28.2026/` → `FAI_report P-4471 RevC_11.28.2026.xlsx`
- Lần 2 trong ngày: `FAI_P-4471 RevC_11.28.2026_v2/` → `FAI_report P-4471 RevC_11.28.2026_v2.xlsx`
- Assistant: `REPORT_weekly status_11.28.2026/` → `REPORT_weekly status_11.28.2026.pdf`

**Folder chứa gì:** chỉ kết quả — file chính + phụ lục (xlsx, ảnh render…), mọi file cùng hậu tố `_<ngày>[_vN]`.
Không copy file gốc của người dùng vào.

## Đặt folder ở đâu

1. **Có bản cũ:** `search_files` theo `<mã>` / `<Loại>_<mã>` tìm folder các phiên bản trước → đặt folder mới
   **cùng thư mục cha** với chúng.
2. **Chưa có:** tạo folder trong thư mục dự án của task (thư mục con hợp lý, vd. `03_FAI`, `04_ISSUE & ANALYSIS`,
   hoặc thư mục loại như `ECNs/`; tạo nếu chưa có).
3. **Không chắc thư mục dự án nào:** hỏi người dùng.

Không đặt ở gốc Drive, không đặt vào thư mục memory hay thư mục dữ liệu của repo (`memory-drive.md`).

Kiểm tra trùng ngày: `search_files` với
`'<parentId>' in parents and title contains '<Loại>_<mã>_<MM.DD.YYYY>'` → lấy số `_vN` kế tiếp.

## Gọi connector (`create_file`)

- Folder: `title = <tên folder>`, `contentMimeType = application/vnd.google-apps.folder`, `parentId = <thư mục cha>`.
- File: `parentId = <ID folder phiên bản>`, `contentMimeType` đúng loại file.
  PDF / xlsx / docx / ảnh: `disableConversionToGoogleType = true` (không bị đổi sang Google Doc / Sheet, giữ đuôi file).
- File nhị phân: `base64Content = sha256:<hash>:<đường dẫn tuyệt đối>` (tham chiếu file, không gõ base64).

## Hỏi trước, báo sau

1. **Trước khi tải:** hỏi người dùng, đề xuất luôn đường dẫn đầy đủ + tên folder + tên file để duyệt một lần.
2. **Sau khi tải:** luôn gửi người dùng **link thư mục phiên bản** (nhất là khi vừa tạo folder mới).
3. **Hub:** `Output link` của Task = link thư mục phiên bản; Event `done` / `review` nêu tên file chính.
