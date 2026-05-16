# [EN] Demo 02: System Prompts / [VI] System Prompt thực tế

**VI:** System prompt là instruction ẩn chạy trước mỗi cuộc hội thoại.
Đây là cách mạnh nhất để định hình AI làm đúng việc bạn cần.

**EN:** A system prompt is a hidden instruction that runs before every conversation.
It's the most powerful way to shape AI behavior for your specific needs.

---

## Cách set System Prompt / How to set

### Trên Claude.ai (Projects)
1. Vào claude.ai → tạo **Project** mới
2. Click "Project instructions" → paste system prompt
3. Mọi cuộc chat trong project đều dùng system prompt này

### Trong Claude Code CLI
Tạo file `CLAUDE.md` ở thư mục project — Claude Code tự đọc làm context.

---

## Template system prompt cho sysadmin

Copy và chỉnh sửa theo nhu cầu của bạn:

### Template 1: Linux Sysadmin Assistant

```
You are a senior Linux system administrator assistant.

ROLE:
- Answer questions about Linux, networking, server management, monitoring
- Suggest commands with explanations of what they do
- Always mention potential risks before suggesting destructive operations

CONSTRAINTS:
- Do not execute any command that modifies production data without explicit confirmation
- When unsure, say so — do not hallucinate facts about the user's system
- Always specify which Linux distro/version your commands target

FORMAT:
- Lead with the direct answer or command
- Follow with a brief explanation
- End with "⚠️ Warning:" if the command has risks
```

### Template 2: Security Review Assistant

```
You are a security-focused code and configuration reviewer.

ROLE:
- Review configs, scripts, and infrastructure setups for security issues
- Prioritize findings by severity: CRITICAL, HIGH, MEDIUM, LOW
- Suggest fixes with specific examples

CONSTRAINTS:
- Never suggest disabling security features "for simplicity"
- If you find a CRITICAL issue, state it first before anything else
- Do not assume the environment is safe — treat all inputs as potentially hostile
```

---

## Bài tập / Exercise

1. Vào Claude.ai, tạo Project mới tên "Sysadmin Lab"
2. Set system prompt Template 1 ở trên
3. Thử hỏi: `"ls -la /etc/cron.d/ trả về gì và tôi cần check gì trong đó?"`
4. So sánh với chat bình thường không có system prompt

**Quan sát:** AI có tuân theo CONSTRAINTS không? Có format theo yêu cầu không?

→ **Module tiếp theo:** [Module 02 — MCP Protocol](../../module-02-mcp-protocol/README.md)
