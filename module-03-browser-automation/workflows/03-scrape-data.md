# [EN] Workflow 03: Scrape Data / [VI] Trích xuất dữ liệu

**Use case:** Lấy dữ liệu từ trang web không có API —
status page của vendor, bảng giá, danh sách server trên web console.

---

## Prompt mẫu — Scrape bảng dữ liệu

```
Trang hiện tại có bảng danh sách servers. Trích xuất toàn bộ bảng đó,
format thành Markdown table với các cột: Name, Status, IP, Last Updated.
Nếu có nhiều trang (pagination), chỉ lấy trang hiện tại thôi.
```

---

## Prompt mẫu — Theo dõi status

```
Vào trang https://status.example.com
Liệt kê tất cả services và status hiện tại của chúng (operational/degraded/down).
Format: "- [service name]: [status]"
```

---

## Những gì AI sẽ làm

1. `chrome-devtools__navigate_page` → mở URL
2. `chrome-devtools__take_snapshot` → lấy DOM
3. Phân tích DOM, trích xuất data
4. Format và trả về cho bạn

---

## Giới hạn cần biết / Limitations

- Trang dùng JavaScript render phức tạp: AI cần đợi load đủ (thêm `wait_for`)
- CAPTCHA / login: bạn phải login thủ công trước, AI dùng session đó
- Dynamic content update liên tục: AI chụp snapshot tại một thời điểm, không realtime

→ **Module tiếp theo:** [Module 04 — Platform Workflows](../../module-04-platform-workflows/README.md)
