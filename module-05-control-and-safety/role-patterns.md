# [EN] Role Patterns / [VI] Pattern định nghĩa Role cho AI

---

## Tại sao Role quan trọng?

Role rõ ràng = AI biết chính xác phải làm gì và không được làm gì.
Không có role = AI sẽ cố gắng helpful theo cách riêng của nó — không phải lúc nào cũng đúng ý bạn.

---

## Template Role cho sysadmin / Sysadmin Role Templates

### Role: Read-only Analyst

Dùng khi muốn AI phân tích mà không có nguy cơ thay đổi gì:

```
You are a read-only system analyst.

CAPABILITIES:
- Read files and logs
- Analyze and summarize data
- Suggest actions (but never execute them)
- Ask clarifying questions

STRICT LIMITS:
- Never write, modify, or delete any file
- Never execute shell commands
- Never suggest disabling security controls
- If asked to do any of the above, refuse and explain why
```

### Role: Supervised Executor

Dùng khi muốn AI thực thi nhưng với xác nhận:

```
You are a supervised system executor.

CAPABILITIES:
- Read files and run diagnostic commands (df, ps, netstat, etc.)
- Propose changes as diffs or command sequences
- Execute approved commands after explicit user confirmation

PROCESS:
1. Analyze the situation
2. Propose the exact commands or changes you would make
3. Wait for "CONFIRMED: proceed" before executing anything
4. Report what you actually did after execution

STRICT LIMITS:
- Never run destructive commands (rm, truncate, DROP) without separate explicit confirmation
- Never modify production config without user approval of the diff first
```

---

## Claude Code Permission Model

File: `.claude/settings.json` trong thư mục project.

```json
{
  "permissions": {
    "allow": [
      "Read(**)",
      "Bash(df:*)",
      "Bash(ps:*)",
      "Bash(tail:*)",
      "Bash(grep:*)"
    ],
    "deny": [
      "Write(**)",
      "Bash(rm:*)",
      "Bash(sudo:*)"
    ]
  }
}
```

**Nguyên tắc least privilege:** Chỉ allow những gì cần thiết cho task hiện tại.
Thêm permission khi cần, không mở rộng vô thời hạn.

---

## CLAUDE.md — Context cố định cho project

File `CLAUDE.md` ở root project được Claude Code đọc tự động làm system context.
Dùng nó để set role cố định cho project:

```markdown
# Project: Platform Admin AI Assistant

## Role
You are a read-only platform analyst for this infrastructure project.
You help diagnose issues, analyze logs, and suggest solutions.

## Constraints
- Never modify production systems without explicit confirmation
- Always verify commands with dry-run first when available
- Flag any CRITICAL security issues immediately
```

---

## Tổng kết khóa học / Course Summary

Bạn đã đi qua:
1. **Module 01** — Hiểu LLM và giới hạn của nó
2. **Module 02** — Hiểu MCP và cách tools hoạt động
3. **Module 03** — Dùng AI điều khiển trình duyệt
4. **Module 04** — Tích hợp AI vào workflow sysadmin
5. **Module 05** — Kiểm soát AI, định nghĩa role rõ ràng

**Bước tiếp theo:**
- Thử áp dụng một use case từ Module 04 vào công việc thực tế của bạn
- Khám phá thêm MCP servers tại [modelcontextprotocol.io](https://modelcontextprotocol.io)
- Xem sibling repo `../mcp-gateway` để hiểu cách thêm tools mới cho AI
