# [EN] Use Case 02: Server Health Check / [VI] Kiểm tra sức khỏe server

**Context:** Bạn muốn AI chạy một loạt lệnh kiểm tra và tổng hợp kết quả
thay vì bạn phải chạy từng lệnh thủ công.

---

## Prompt: Quick health check

```
Chạy các lệnh sau và tổng hợp kết quả thành health report:

1. uptime                          # Load average
2. df -h                           # Disk usage
3. free -h                         # RAM usage
4. ss -tlnp | grep LISTEN          # Open ports
5. systemctl list-units --failed   # Failed services

Format kết quả:
- ✅ OK nếu trong giới hạn bình thường
- ⚠️ WARNING nếu cần chú ý
- ❌ CRITICAL nếu cần action ngay

Ngưỡng: disk > 80% = WARNING, > 90% = CRITICAL. Load > số CPU = WARNING.
```

**Lưu ý:** Claude Code cần Bash permission. Xác nhận từng lệnh hoặc allowlist trước.

---

## Prompt: Service-specific check

```
Kiểm tra PostgreSQL service:
1. systemctl status postgresql
2. Kết nối test: psql -U postgres -c "SELECT version();"
3. Số connections hiện tại: psql -U postgres -c "SELECT count(*) FROM pg_stat_activity;"
4. Database size: psql -U postgres -c "SELECT pg_size_pretty(pg_database_size('mydb'));"

Báo cáo: service healthy hay có vấn đề gì cần xử lý?
```

---

## Tại sao dùng AI thay vì script thông thường?

Script cố định → output cố định → bạn vẫn phải đọc và interpret.
AI → interpret luôn → chỉ cần đọc summary + action items.

Dùng cả hai: script collect data, AI interpret.
