# [EN] Use Case 01: Log Analysis / [VI] Phân tích Log

**Context:** Server có vấn đề, bạn có log file và muốn AI tìm pattern lỗi nhanh hơn grep.

---

## Cách 1: Paste log trực tiếp vào Claude Code chat

Dùng khi log file nhỏ (< 500 dòng):

```
Phân tích log sau và tìm:
1. Tất cả ERROR và CRITICAL messages
2. Pattern lặp lại (cùng error xuất hiện nhiều lần)
3. Time range xảy ra nhiều lỗi nhất
4. Nguyên nhân gốc rễ có thể

<paste log vào đây>
```

---

## Cách 2: Claude Code đọc file trực tiếp

Dùng khi log file lớn — Claude Code có file read access:

```
Đọc file /var/log/nginx/error.log (500 dòng cuối cùng)
và tìm tất cả 5xx errors trong 1 giờ vừa qua.
Group theo error type và đếm số lần xuất hiện.
```

Điều kiện: Claude Code phải có read permission cho `/var/log/nginx/`.
Check trong `.claude/settings.json`:
```json
{
  "permissions": {
    "allow": ["Read(/var/log/**)", "Bash(tail:*)"]
  }
}
```

---

## Cách 3: Pipe output vào Claude Code

```bash
tail -n 1000 /var/log/syslog | claude "Tìm pattern lỗi bất thường trong log này"
```

---

## Prompt nâng cao — Triage theo priority

```
Tôi có log từ production server bị chậm từ 14:00 hôm nay.
Đọc /var/log/app/application.log

Phân tích:
1. CRITICAL: có lỗi nào có thể gây downtime không?
2. HIGH: bottleneck performance ở đâu?
3. INFO: request nào tốn thời gian nhất?

Format kết quả: mỗi mục có timestamp, message gốc, và đề xuất action.
```
