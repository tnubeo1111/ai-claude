# [EN] Workflow 01: Navigate & Screenshot / [VI] Điều hướng và chụp màn hình

**Prereq:** [Setup guide](../setup-guide.md) đã hoàn thành, Chrome đang chạy với port 9222.

---

## Use case

Bạn muốn AI mở một trang, đợi nó load, chụp screenshot để report.
Ví dụ thực tế: chụp monitoring dashboard hàng ngày.

---

## Prompt để thử

Trong Claude Code chat:

```
1. Mở tab mới và điều hướng đến https://grafana.com/demo
2. Đợi trang load hoàn toàn (3 giây)
3. Chụp screenshot toàn trang
4. Mô tả những gì bạn thấy trên trang
```

---

## Những gì AI sẽ làm

1. Gọi tool `chrome-devtools__new_page` → mở tab mới
2. Gọi tool `chrome-devtools__navigate_page` với URL
3. Gọi tool `chrome-devtools__wait_for` để đợi page load
4. Gọi tool `chrome-devtools__take_screenshot` → trả về ảnh
5. Phân tích ảnh và mô tả nội dung

---

## Control pattern — Bạn kiểm soát từng bước

Claude Code sẽ **hỏi xác nhận** trước mỗi tool call có side effect.
Đây là cơ chế an toàn mặc định:

```
Claude: "Tôi sẽ mở tab mới và điều hướng đến URL. Cho phép?"
Bạn: [Allow / Deny]
```

Bạn có thể set allow một lần cho tool `navigate_page` trong session hiện tại.

---

## Thực hành / Practice

Thay URL bằng:
- Dashboard nội bộ của bạn (nếu accessible từ local)
- `http://localhost:3010` — web dashboard của mcp-gateway

→ **Tiếp theo:** [Workflow 02 — Fill Forms](02-fill-forms.md)
