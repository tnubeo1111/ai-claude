# [EN] Workflow 02: Fill Forms / [VI] Điền form với kiểm soát

**Use case:** Điền form trên web UI lặp đi lặp lại — ví dụ: tạo user mới,
submit ticket, điền config trên admin panel.

---

## Pattern quan trọng: Confirm before submit

**VI:** Luôn yêu cầu AI xác nhận với bạn trước khi submit form.
Đây là "human-in-the-loop" cho browser automation.

---

## Prompt mẫu

```
Trên trang hiện tại, điền form tạo user mới với:
- Username: testuser01
- Email: testuser01@example.com
- Role: viewer

Sau khi điền xong, dừng lại và cho tôi xem trước khi submit.
KHÔNG submit cho đến khi tôi xác nhận.
```

---

## Những gì AI sẽ làm

1. `chrome-devtools__take_snapshot` → đọc DOM để tìm form fields
2. `chrome-devtools__fill` → điền từng field
3. **Dừng lại, báo cáo với bạn** — không tự submit
4. Chờ xác nhận của bạn
5. Sau khi bạn confirm: `chrome-devtools__click` → submit

---

## Tại sao "KHÔNG submit cho đến khi tôi xác nhận" quan trọng?

Với form read-only (search, filter): submit ít rủi ro.
Với form write (tạo user, xóa resource, deploy): luôn phải confirm trước.

Thêm câu này vào mọi prompt liên quan đến form có side effect trên production.

→ **Tiếp theo:** [Workflow 03 — Scrape Data](03-scrape-data.md)
