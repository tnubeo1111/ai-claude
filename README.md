# [EN] AI Agent Learning Course / [VI] Khóa học AI Agent

Khóa học thực hành về AI agent dành cho sysadmin và platform engineer —
hiểu cơ chế, không build sản phẩm, học cách dùng AI như một công cụ có kiểm soát.

A hands-on AI agent course for sysadmins and platform engineers —
understand the mechanics, use AI as a controlled tool, not just a chatbot.

---

## Prerequisites / Điều kiện

- Claude Pro subscription (claude.ai)
- Claude Code CLI đã cài và đăng nhập (`claude --version`)
- Không cần API key riêng / No separate API key needed

---

## Bản đồ học / Learning Map

```
Module 01 → Module 02 → Module 03 → Module 04 → Module 05
AI Cơ bản   MCP Protocol  Browser     Platform    Control &
                          Automation  Workflows   Safety
```

| Module | Chủ đề | Thời gian ước tính |
|--------|--------|-------------------|
| [01 — AI Fundamentals](module-01-ai-fundamentals/README.md) | LLM là gì, agent là gì, context window, roles | 1-2 giờ |
| [02 — MCP Protocol](module-02-mcp-protocol/README.md) | Tool use, MCP flow, mcp-gateway | 1-2 giờ |
| [03 — Browser Automation](module-03-browser-automation/README.md) | Chrome DevTools MCP, điều khiển trình duyệt | 1-2 giờ |
| [04 — Platform Workflows](module-04-platform-workflows/README.md) | Log analysis, server check, report | 2-3 giờ |
| [05 — Control & Safety](module-05-control-and-safety/README.md) | Human-in-the-loop, role patterns, permissions | 1 giờ |

---

## Cách dùng repo này / How to use

1. Đọc từng module theo thứ tự — mỗi module build trên kiến thức module trước
2. Mỗi module có README tổng quan → đọc trước
3. Thử các ví dụ trực tiếp trên Claude.ai hoặc qua Claude Code CLI
4. Không cần chạy code phức tạp — copy prompt, thử, quan sát kết quả

---

## Success Criteria / Bạn đã học xong khi

- [ ] Giải thích được LLM, agent, MCP cho người khác
- [ ] Cài và cấu hình được MCP server mới vào Claude Code
- [ ] Dùng AI điều khiển trình duyệt thực hiện task cụ thể
- [ ] Xây dựng workflow AI cho ít nhất 1 task sysadmin thực tế
- [ ] Viết được system prompt kiểm soát AI đúng scope, an toàn
