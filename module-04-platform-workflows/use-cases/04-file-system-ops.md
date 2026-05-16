# [EN] Use Case 04: File System Ops / [VI] Thao tác file system có kiểm soát

**Context:** AI đọc, so sánh, và đề xuất thay đổi file config —
bạn review và quyết định có apply không.

---

## Pattern an toàn: Đề xuất trước, apply sau

```
VI: Không để AI tự sửa file config quan trọng.
Pattern: AI đề xuất diff → bạn review → bạn apply (hoặc không).

EN: Never let AI auto-edit critical config files.
Pattern: AI proposes diff → you review → you apply (or reject).
```

---

## Prompt: So sánh hai config file

```
So sánh /etc/nginx/nginx.conf với /etc/nginx/nginx.conf.bak
Liệt kê sự khác biệt theo format:
- Dòng X: [nội dung cũ] → [nội dung mới]
Đánh giá: thay đổi nào có thể gây vấn đề?
```

---

## Prompt: Review config trước khi apply

```
Đọc file /etc/nginx/sites-available/myapp.conf
Review cấu hình này và tìm:
1. Security issues (missing headers, weak TLS config, etc.)
2. Performance improvements có thể áp dụng
3. Lỗi cú pháp tiềm năng

Đề xuất dưới dạng diff (format unified diff).
KHÔNG tự sửa file — chỉ đề xuất.
```

---

## Prompt: Tìm file theo pattern

```
Tìm tất cả file .conf trong /etc/
- Có chứa "password" hoặc "secret" trong plaintext
- Liệt kê file path và dòng cụ thể
- Đây là security audit — không thay đổi gì
```

---

## Permission cần thiết

```json
// .claude/settings.json
{
  "permissions": {
    "allow": [
      "Read(/etc/**)",
      "Read(/var/log/**)"
    ],
    "deny": [
      "Write(/etc/**)"
    ]
  }
}
```

→ **Module tiếp theo:** [Module 05 — Control & Safety](../../module-05-control-and-safety/README.md)
