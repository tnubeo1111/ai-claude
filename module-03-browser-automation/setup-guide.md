# [EN] Setup Guide: Chrome DevTools MCP / [VI] Hướng dẫn cài đặt

**VI:** Chrome DevTools MCP là MCP server cho phép Claude Code điều khiển
Chrome/Chromium thông qua Chrome DevTools Protocol.

**EN:** Chrome DevTools MCP is an MCP server that lets Claude Code control
Chrome/Chromium via the Chrome DevTools Protocol.

---

## Yêu cầu / Requirements

- Chrome hoặc Chromium đã cài
- Claude Code CLI đang chạy
- Node.js >= 18 (check: `node --version`)

---

## Bước 1: Cài Chrome DevTools MCP

```bash
npx @anthropic-ai/claude-code --add-mcp-server chrome-devtools
```

Hoặc thêm thủ công vào Claude Code settings:

```bash
claude mcp add chrome-devtools npx @modelcontextprotocol/server-chrome-devtools
```

---

## Bước 2: Verify cài đặt

Trong Claude Code, gõ:
```
/mcp
```

Bạn sẽ thấy `chrome-devtools` trong danh sách MCP servers connected.

---

## Bước 3: Mở Chrome với remote debugging

Chrome phải chạy với remote debugging port mở:

```bash
# Linux
google-chrome --remote-debugging-port=9222 &

# Hoặc Chromium
chromium-browser --remote-debugging-port=9222 &
```

Verify Chrome đang expose DevTools:
```bash
curl http://localhost:9222/json
```
Expected: JSON list của các tab đang mở.

---

## Test kết nối / Test connection

Trong Claude Code chat, thử:
```
List all open browser tabs
```

Claude sẽ gọi tool `chrome-devtools__list_pages` và trả về danh sách tabs.
Nếu thấy tên tab của bạn → setup thành công.

---

## Troubleshooting

| Vấn đề | Giải pháp |
|--------|-----------|
| `Connection refused :9222` | Chrome chưa mở với `--remote-debugging-port=9222` |
| MCP server không thấy trong `/mcp` | Restart Claude Code sau khi cài |
| Không có quyền kết nối | Kiểm tra firewall, port 9222 phải accessible từ localhost |

→ **Tiếp theo:** [Workflow 01 — Navigate & Screenshot](workflows/01-navigate-screenshot.md)
