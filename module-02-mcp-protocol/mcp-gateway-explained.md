# [EN] MCP Gateway Explained / [VI] Giải thích mcp-gateway

**VI:** Repo `../mcp-gateway` mà bạn đang có là một **gateway** — một proxy
kết nối nhiều MCP server thành một endpoint duy nhất.

**EN:** The `../mcp-gateway` repo is a **gateway** — a proxy that aggregates
multiple MCP servers into a single endpoint.

---

## Vấn đề gateway giải quyết / The problem it solves

```
Không có gateway:               Có gateway:

Claude Code                     Claude Code
  ├── kết nối server A            │
  ├── kết nối server B            └── kết nối mcp-gateway
  ├── kết nối server C                     │
  └── kết nối server D                     ├── server A
                                           ├── server B
                                           ├── server C
                                           └── server D
```

Thay vì Claude Code phải quản lý N kết nối riêng lẻ,
gateway nhận một kết nối và fan-out đến tất cả upstream servers.

---

## Kiến trúc thực tế / Real architecture

```
AI Agent (Hermes / Claude Code)
         │
         │ SSE / Streamable HTTP
         ▼
    mcp-gateway :3010
         │
         ├── ceph-alpha    (fastmcp  → http://172.25.155.214:8000/mcp)
         ├── sequential-thinking (stdio → docker run mcp/sequentialthinking)
         └── markitdown    (stdio    → uvx markitdown-mcp)
```

*Đây là cấu hình thực tế trong `../mcp-gateway/servers.json` của bạn.*

---

## Namespace Tool — Cách tránh xung đột tên

**VI:** Nếu server A và server B đều có tool tên `get_status`,
gateway sẽ rename chúng để tránh xung đột:

```
server A: ceph-alpha          → ceph_alpha__get_status
server B: monitoring-server   → monitoring_server__get_status
```

Rule: `server-id` → replace `-` bằng `_` → thêm `__` → tên tool gốc

**Ví dụ thực tế từ ceph-alpha:**
- `get_health_summary` → `ceph_alpha__get_health_summary`
- `get_cluster_capacity` → `ceph_alpha__get_cluster_capacity`

---

## Kết nối vào gateway / Connecting to the gateway

Gateway đang chạy tại `http://localhost:3010`. Để kết nối từ Claude Code:

```json
// ~/.claude/claude_desktop_config.json hoặc settings.json
{
  "mcpServers": {
    "mcp-gateway": {
      "url": "http://localhost:3010/sse?apiKey=mcp_gateway_secret_123",
      "transport": "sse"
    }
  }
}
```

Sau khi kết nối, Claude Code sẽ thấy **tất cả tools** từ tất cả upstream servers,
được namespace rõ ràng.

---

## 4 loại transport / 4 transport types

| Transport | Dùng khi |
|-----------|---------|
| `streamable-http` | Server hỗ trợ MCP 2025-11-25 |
| `sse` | Server dùng SSE protocol 2024-11-05 |
| `fastmcp` | Ceph Storage Assistant (custom) |
| `stdio` | Local process: npx, python, docker |

---

## Tại sao điều này quan trọng với sysadmin?

Gateway pattern = **single point of control**. Thay vì cấu hình AI client
mỗi lần thêm tool mới, bạn chỉ cần thêm server vào gateway một lần.
Tất cả AI clients kết nối vào gateway tự động thấy tools mới.

→ **Module tiếp theo:** [Module 03 — Browser Automation](../../module-03-browser-automation/README.md)
