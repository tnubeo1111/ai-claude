# [EN] Demo 01: Basic Prompting / [VI] Prompt cơ bản

Thử trực tiếp trên [claude.ai](https://claude.ai) — không cần setup gì thêm.

---

## Nguyên tắc prompt tốt / Good prompting principles

**VI:** Prompt tốt = **Ngữ cảnh + Mục tiêu + Ràng buộc**
**EN:** Good prompt = **Context + Goal + Constraints**

---

## Ví dụ thực tế cho sysadmin / Sysadmin prompt examples

### ❌ Prompt tệ

```
tại sao server chậm?
```

AI sẽ đưa ra danh sách chung chung 10 nguyên nhân có thể — không hữu ích.

### ✓ Prompt tốt

```
Server Linux Ubuntu 22.04, có triệu chứng: load average cao (~8.0 trên 4 core),
disk I/O wait khoảng 60%, RAM còn 2GB/16GB. Service chính là PostgreSQL 15.
Tôi cần bước triage theo thứ tự ưu tiên để tìm bottleneck.
```

AI sẽ đưa ra quy trình triage cụ thể với commands thực tế.

---

### ❌ Prompt tệ

```
viết script backup
```

### ✓ Prompt tốt

```
Viết bash script backup cho thư mục /var/www/myapp, nén bằng tar.gz,
tên file format: backup-YYYY-MM-DD.tar.gz, lưu vào /mnt/backup/,
giữ tối đa 7 bản gần nhất, xóa bản cũ hơn. Thêm logging ra /var/log/backup.log.
```

---

## Bài tập / Exercise

Thử các prompt sau trên Claude.ai và quan sát kết quả:

1. **Dùng prompt tệ trước:** `explain kubernetes`
2. **Sau đó dùng prompt tốt:**
   ```
   Tôi là sysadmin quen với Docker Compose nhưng chưa dùng Kubernetes.
   Giải thích các concept sau theo thứ tự từ đơn giản đến phức tạp:
   Pod, Service, Deployment, Namespace. Mỗi concept 2-3 câu + so sánh với Docker.
   ```
3. So sánh chất lượng 2 câu trả lời.

→ **Tiếp theo:** [Demo 02 — System Prompts](02-system-prompts.md)
