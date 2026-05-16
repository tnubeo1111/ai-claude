# [EN] Human-in-the-Loop / [VI] Luôn có người kiểm soát

---

## Nguyên tắc cốt lõi / Core principle

```
Read → OK để AI tự chạy
Write / Execute / Delete → Phải có xác nhận của bạn trước
```

---

## Pattern 1: Confirm trước action có side effect

Luôn thêm vào prompt:

```
Trước khi thực hiện bất kỳ thay đổi nào (ghi file, chạy command có side effect,
submit form), dừng lại và mô tả chính xác bạn sẽ làm gì.
Chờ tôi xác nhận "OK" trước khi tiếp tục.
```

---

## Pattern 2: Propose diff, không tự apply

```
Đề xuất thay đổi cần thiết cho file này dưới dạng unified diff.
Giải thích từng thay đổi.
KHÔNG tự apply — tôi sẽ review và apply thủ công.
```

---

## Pattern 3: Dry-run trước

Với các command có thể gây hại:

```
Trước tiên chạy lệnh ở chế độ dry-run (nếu có) hoặc
simulate để tôi thấy kết quả trước khi chạy thật.

Ví dụ: thay vì `rm -rf /path`, chạy `find /path -type f` trước
để tôi thấy danh sách file sẽ bị xóa.
```

---

## Red flags — Dấu hiệu AI đi ra ngoài lề

Ngừng và kiểm tra lại nếu AI:
- Tự động chạy command không được yêu cầu
- Giải thích mờ nhạt về những gì nó vừa làm
- Đề xuất disable security feature "cho đơn giản"
- Báo cáo kết quả không khớp với những gì bạn thấy
- Dùng `sudo` mà không hỏi

---

## Claude Code permission prompt

Mặc định, Claude Code hỏi confirm trước mỗi tool call:

```
Claude wants to run: rm -rf /tmp/old_logs/
[Allow once] [Allow always] [Deny]
```

Nguyên tắc:
- **Allow once**: cho phép lần này, hỏi lại lần sau — dùng khi không chắc
- **Allow always**: thêm vào allowlist session — chỉ dùng cho read-only tools
- **Deny**: từ chối và giải thích với Claude tại sao

→ **Tiếp theo:** [role-patterns.md](role-patterns.md)
