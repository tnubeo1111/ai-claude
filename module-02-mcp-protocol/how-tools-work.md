# [EN] How Tools Work / [VI] Tool Use hoạt động thế nào

---

## Vấn đề với chatbot thuần túy / The chatbot problem

**VI:** Khi bạn hỏi chatbot "disk /var còn bao nhiêu?", nó chỉ có thể đoán
hoặc trả lời chung chung — nó không thể thực sự SSH vào server của bạn.

**Tool use** giải quyết điều này: AI có thể gọi một hàm thực sự, nhận kết quả thực sự,
rồi trả lời dựa trên dữ liệu thực.

---

## Flow hoàn chỉnh / Complete flow

```
User: "Disk /var còn bao nhiêu?"
         │
         ▼
    Claude suy nghĩ:
    "Tôi cần gọi tool check_disk với path=/var"
         │
         ▼
    Tool: check_disk(path="/var")
    → chạy: df -h /var
    → trả về: "Used: 45GB / Total: 100GB (45%)"
         │
         ▼
    Claude nhận kết quả và trả lời:
    "Disk /var hiện dùng 45GB trên 100GB (45%), còn thoải mái."
```

**EN:** The AI doesn't run the command itself — it *requests* a tool call,
the host executes it, returns the result, and the AI incorporates it into its response.

---

## MCP là gì? / What is MCP?

**VI:** **Model Context Protocol (MCP)** là giao thức chuẩn do Anthropic phát triển
để định nghĩa cách AI agent giao tiếp với tools bên ngoài.

Thay vì mỗi AI vendor tự làm cách riêng, MCP chuẩn hóa:
- Cách khai báo tool (tên, params, description)
- Cách AI gọi tool (JSON-RPC request)
- Cách tool trả kết quả (JSON-RPC response)

**EN:** MCP is an open protocol that standardizes how AI agents communicate with external tools.

---

## Các thành phần MCP / MCP Components

```
┌─────────────────────────────────────────┐
│           MCP Host (Claude Code)        │  ← Chạy trên máy bạn
│  ┌──────────┐      ┌─────────────────┐  │
│  │  Claude  │◄────►│   MCP Client    │  │
│  │  (LLM)   │      │ (manages tools) │  │
│  └──────────┘      └────────┬────────┘  │
└───────────────────────────  │  ─────────┘
                              │ JSON-RPC over stdio/HTTP/SSE
                ┌─────────────▼─────────────┐
                │       MCP Server          │  ← Tool provider
                │  (chrome-devtools, fs,    │
                │   git, mcp-gateway, ...)  │
                └───────────────────────────┘
```

| Thành phần | Vai trò |
|------------|---------|
| **MCP Host** | App chứa LLM và quản lý connections (Claude Code, Claude Desktop) |
| **MCP Client** | Phần trong Host kết nối đến MCP Server |
| **MCP Server** | Cung cấp tools cho AI (mỗi server = một bộ tools) |

---

## Tool Definition — Ví dụ thực tế

Đây là cách một MCP server khai báo tool `get_disk_usage`:

```json
{
  "name": "get_disk_usage",
  "description": "Get disk usage for a specific path on the server",
  "inputSchema": {
    "type": "object",
    "properties": {
      "path": {
        "type": "string",
        "description": "Filesystem path to check, e.g. /var"
      }
    },
    "required": ["path"]
  }
}
```

Claude đọc description này, tự quyết định khi nào nên gọi tool này,
và tự điền đúng params từ context câu hỏi của user.

---

## Tại sao điều này quan trọng với sysadmin?

Bạn có thể tạo MCP server expose các tools cụ thể cho hệ thống của mình:
- Kiểm tra service status
- Đọc log file
- Query monitoring API

AI sau đó có thể dùng các tools đó trong workflow tự nhiên mà không cần bạn
phải biết cú pháp API hay CLI cụ thể.

→ **Tiếp theo:** [mcp-gateway-explained.md](mcp-gateway-explained.md)
