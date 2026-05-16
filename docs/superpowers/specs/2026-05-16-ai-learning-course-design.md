# AI Learning Course Design
# Thiết kế Khóa học AI

**Date:** 2026-05-16  
**Repo:** `mcp-plugin-ai`  
**Status:** Approved — ready for implementation planning

---

## Goal / Mục tiêu

Biến repo `mcp-plugin-ai` thành một khóa học có cấu trúc, song ngữ (Tiếng Việt / English), giúp người có nền tảng kỹ thuật (sysadmin/platform) hiểu sâu về AI agent và tích hợp AI vào công việc thực tế — không phải để build sản phẩm, mà để **dùng AI như một công cụ có kiểm soát**.

## Target Audience / Đối tượng

- Background: System admin / platform engineer
- Biết kỹ thuật, quen với CLI, config, server
- Chưa có kinh nghiệm với AI agent, LLM, MCP
- Không cần build sản phẩm — muốn hiểu cơ chế và tích hợp vào workflow cá nhân

## Prerequisites / Điều kiện

- Claude Pro subscription (đang có)
- Claude Code CLI (đang có, OAuth)
- mcp-gateway sibling repo (đang có tại `../mcp-gateway`)
- Không cần Anthropic API key riêng

## Approach

Module-based curriculum: mỗi module là một nhóm concept độc lập, có lý thuyết + ví dụ thực tế + liên hệ công việc sysadmin.

---

## Structure / Cấu trúc

```
mcp-plugin-ai/
│
├── README.md                          # Landing page: bản đồ học, cách dùng repo
│
├── module-01-ai-fundamentals/
│   ├── README.md                      # Overview module
│   ├── concepts.md                    # LLM, token, context window, system prompt, role
│   └── demos/                         # Prompt examples để thử trực tiếp trên Claude.ai
│
├── module-02-mcp-protocol/
│   ├── README.md                      # Overview module
│   ├── how-tools-work.md              # Tool use flow: agent → tool → result → agent
│   └── mcp-gateway-explained.md       # Giải thích sibling repo mcp-gateway
│
├── module-03-browser-automation/
│   ├── README.md                      # Overview module
│   ├── setup-guide.md                 # Cài Chrome DevTools MCP vào Claude Code
│   └── workflows/                     # Task cụ thể: fill form, navigate, scrape, screenshot
│
├── module-04-platform-workflows/
│   ├── README.md                      # Overview module
│   └── use-cases/                     # Log analysis, server check, report generation, file ops
│
└── module-05-control-and-safety/
    ├── README.md                      # Overview module
    ├── human-in-the-loop.md           # Khi nào cần confirm trước khi AI hành động
    └── role-patterns.md               # System prompt patterns để giới hạn scope AI
```

---

## Module Details / Nội dung chi tiết

### Module 01 — AI Fundamentals

**Mục tiêu:** Hiểu AI hoạt động thế nào trước khi chạm vào bất kỳ tool nào.

Concepts:
- **LLM là gì:** pattern prediction engine, không phải "AI biết hết" — hiểu điều này giúp prompt tốt hơn
- **Token & context window:** tại sao AI "quên" nếu chat quá dài
- **System prompt & role:** cách định hình "tính cách" và giới hạn của AI
- **Chatbot vs AI Agent vs Autonomous Agent:** sự khác biệt thực chất

Sysadmin relevance: Biết giới hạn của AI = biết khi nào tin được, khi nào phải verify.

---

### Module 02 — MCP Protocol

**Mục tiêu:** Hiểu tại sao MCP là bước nhảy vọt của AI agent.

Concepts:
- **Tool use:** AI không chỉ trả lời — nó có thể *gọi công cụ* và nhận kết quả
- **Flow:** `Claude → quyết định dùng tool → tool thực thi → kết quả trả về → Claude trả lời`
- **MCP server / client / gateway:** vai trò của từng thành phần
- **mcp-gateway explained:** tại sao repo đó tồn tại, nó giải quyết vấn đề gì, namespace tool hoạt động thế nào (`ceph_alpha__get_health_summary`)

Sysadmin relevance: MCP = cách AI tương tác với hệ thống thật — không chỉ chat.

---

### Module 03 — Browser Automation

**Mục tiêu:** AI điều khiển trình duyệt theo lệnh của bạn, với sự kiểm soát rõ ràng.

Nội dung:
- Cài và cấu hình Chrome DevTools MCP vào Claude Code
- Task thực tế: điền form, navigate, scrape thông tin, chụp screenshot
- Pattern kiểm soát: bạn ra lệnh → AI thực thi → bạn xác nhận trước bước tiếp theo

Sysadmin relevance: Tự động hóa task lặp lại trên web UI mà không cần script phức tạp.

---

### Module 04 — Platform Workflows

**Mục tiêu:** Tích hợp AI vào công việc sysadmin/platform hàng ngày.

Use cases được xây dựng:
- Đọc log file → AI phân tích → đề xuất action
- AI kiểm tra trạng thái server/service
- Tạo report tự động từ dữ liệu thô
- AI làm việc với file system có kiểm soát (đọc config, so sánh, đề xuất thay đổi)

Sysadmin relevance: Đây là core module — trực tiếp áp dụng vào công việc.

---

### Module 05 — Control & Safety

**Mục tiêu:** Bạn là người quyết định, AI là công cụ.

Nội dung:
- **Human-in-the-loop patterns:** khi nào cần xác nhận trước khi AI hành động
- **Role definition:** cách viết system prompt giới hạn AI đúng scope, tránh hallucination nguy hiểm
- **Red flags:** dấu hiệu AI đang "đi ra ngoài lề"
- **Claude Code permission model:** allowlist, hooks, settings.json — cơ chế kiểm soát đang có sẵn

Sysadmin relevance: Với quyền truy cập hệ thống, kiểm soát AI không phải tùy chọn — đây là bắt buộc.

---

## Conventions / Quy ước

### Ngôn ngữ
- Tiêu đề: `# [EN] Title / [VI] Tiêu đề`
- Giải thích: song ngữ, Tiếng Việt trước, English sau (hoặc block riêng)
- Code/command: không dịch, giữ nguyên

### Cấu trúc mỗi trang
1. Concept (lý thuyết ngắn gọn)
2. Ví dụ thực tế
3. Liên hệ công việc sysadmin: *"Tại sao điều này quan trọng với bạn?"*

### Tech stack
- Không có code phức tạp
- Shell command và config file là chính
- Claude Code CLI + MCP config là runtime chính
- Không cần API key riêng

---

## Success Criteria / Tiêu chí thành công

Sau khi hoàn thành toàn bộ khóa, người học có thể:
- [ ] Giải thích được LLM, agent, MCP cho người khác
- [ ] Cài và cấu hình MCP server mới vào Claude Code
- [ ] Dùng AI để điều khiển trình duyệt thực hiện task cụ thể
- [ ] Xây dựng workflow AI cho ít nhất 1 task sysadmin thực tế
- [ ] Viết system prompt kiểm soát AI đúng scope, an toàn
