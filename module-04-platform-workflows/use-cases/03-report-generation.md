# [EN] Use Case 03: Report Generation / [VI] Tạo báo cáo tự động

**Context:** Bạn có data thô (CSV, JSON, log) và cần report có format đẹp
để gửi cho team hoặc lưu lại.

---

## Prompt: Weekly server report từ log

```
Đọc /var/log/nginx/access.log

Tạo weekly report với:
1. Tổng số requests trong tuần
2. Top 10 endpoints được gọi nhiều nhất
3. Top 5 IP address có nhiều request nhất
4. Tỷ lệ status codes: 2xx / 3xx / 4xx / 5xx
5. Thời điểm traffic cao nhất trong ngày (theo giờ)

Format: Markdown report với headers, tables, và bullet points.
Thêm ngày tháng vào tiêu đề report.
```

---

## Prompt: Tổng hợp từ nhiều nguồn

```
Tôi có 3 file sau:
- /tmp/disk_usage.txt   (output của df -h)
- /tmp/memory.txt       (output của free -h)
- /tmp/top_processes.txt (output của ps aux --sort=-%cpu | head -20)

Tổng hợp thành Infrastructure Status Report ngày hôm nay.
Format Markdown, có thể gửi email cho manager.
Highlight bất kỳ điều gì đáng chú ý.
```

---

## Tạo report định kỳ với Claude Code + cron

Kết hợp bash script collect data + Claude Code generate report:

```bash
#!/bin/bash
# collect-and-report.sh
DATE=$(date +%Y-%m-%d)
df -h > /tmp/disk_$DATE.txt
free -h > /tmp/mem_$DATE.txt
# Gọi Claude Code để tạo report
claude "Đọc /tmp/disk_$DATE.txt và /tmp/mem_$DATE.txt, tạo daily report" \
  > /tmp/report_$DATE.md
```
