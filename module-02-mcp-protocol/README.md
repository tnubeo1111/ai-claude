# [EN] Module 02: MCP Protocol / [VI] Giao thức MCP

**Mục tiêu:** Hiểu tại sao MCP là bước nhảy vọt của AI agent —
từ "AI chỉ nói chuyện" sang "AI có thể làm việc thật".

**Goal:** Understand why MCP is the leap that turns AI from chatbot to agent —
from "AI that talks" to "AI that acts."

---

## Nội dung module / Contents

1. [How Tools Work](how-tools-work.md) — Tool use flow, JSON-RPC, MCP protocol
2. [MCP Gateway Explained](mcp-gateway-explained.md) — Giải thích sibling repo `../mcp-gateway`

---

## Bạn sẽ học được / What you'll learn

- Tool use là gì và tại sao nó quan trọng hơn chat thông thường
- Flow hoàn chỉnh: Claude → quyết định gọi tool → tool chạy → kết quả → Claude trả lời
- MCP server, client, gateway là gì — vai trò của từng thành phần
- mcp-gateway của bạn hoạt động thế nào từ góc nhìn kỹ thuật

---

## Tại sao điều này quan trọng với sysadmin?

MCP = cách AI tương tác với hệ thống thật, không chỉ chat.
Hiểu MCP = biết cách "nối dây" giữa AI và các hệ thống bạn đang quản lý.

→ **Bắt đầu:** [how-tools-work.md](how-tools-work.md)
