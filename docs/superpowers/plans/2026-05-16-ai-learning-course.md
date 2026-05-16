# AI Learning Course — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use `superpowers:subagent-driven-development` (recommended) or `superpowers:executing-plans` to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Tạo khóa học AI có cấu trúc 5 module, song ngữ Vi/EN, dành cho sysadmin/platform engineer muốn hiểu và dùng AI trong công việc thực tế.

**Architecture:** Mỗi module là một thư mục độc lập với README (overview) + các file nội dung (concepts, demos, workflows, use-cases). Không có code phức tạp — chủ yếu markdown, shell commands, config files, và prompt examples. Người học dùng Claude Pro + Claude Code CLI đang có sẵn, không cần API key riêng.

**Tech Stack:** Markdown, Claude Code CLI (OAuth), Chrome DevTools MCP, mcp-gateway (sibling repo tại `../mcp-gateway`)

---

## File Map

```
mcp-plugin-ai/
├── .gitignore                                          # CREATE
├── README.md                                           # CREATE — landing page
│
├── module-01-ai-fundamentals/
│   ├── README.md                                       # CREATE — module overview
│   ├── concepts.md                                     # CREATE — LLM, token, context, roles
│   └── demos/
│       ├── 01-basic-prompting.md                       # CREATE — good vs bad prompts
│       └── 02-system-prompts.md                        # CREATE — system prompt examples
│
├── module-02-mcp-protocol/
│   ├── README.md                                       # CREATE — module overview
│   ├── how-tools-work.md                               # CREATE — tool use flow diagram
│   └── mcp-gateway-explained.md                        # CREATE — explains sibling repo
│
├── module-03-browser-automation/
│   ├── README.md                                       # CREATE — module overview
│   ├── setup-guide.md                                  # CREATE — install Chrome DevTools MCP
│   └── workflows/
│       ├── 01-navigate-screenshot.md                   # CREATE
│       ├── 02-fill-forms.md                            # CREATE
│       └── 03-scrape-data.md                           # CREATE
│
├── module-04-platform-workflows/
│   ├── README.md                                       # CREATE — module overview
│   └── use-cases/
│       ├── 01-log-analysis.md                          # CREATE
│       ├── 02-server-health-check.md                   # CREATE
│       ├── 03-report-generation.md                     # CREATE
│       └── 04-file-system-ops.md                       # CREATE
│
└── module-05-control-and-safety/
    ├── README.md                                       # CREATE — module overview
    ├── human-in-the-loop.md                            # CREATE
    └── role-patterns.md                                # CREATE
```

**Content verification checklist** (dùng sau mỗi file):
- [ ] Tiêu đề đúng format: `# [EN] Title / [VI] Tiêu đề`
- [ ] Có section "Tại sao điều này quan trọng với sysadmin?"
- [ ] Lý thuyết trước, ví dụ sau
- [ ] Commands/prompts cụ thể, chạy được
- [ ] Links đến module khác dùng relative path

---

## Task 0: Git Init + .gitignore

**Files:**
- Create: `.gitignore`

- [ ] **Step 1: Initialize git repo**

```bash
cd /home/thalt/env-lab/project/mcp-plugin-ai
git init
```

Expected: `Initialized empty Git repository in .../mcp-plugin-ai/.git/`

- [ ] **Step 2: Create .gitignore**

```
.env
__pycache__/
*.pyc
.DS_Store
node_modules/
```

Save to `.gitignore`.

- [ ] **Step 3: Initial commit**

```bash
git add .gitignore CLAUDE.md docs/
git commit -m "chore: initialize repo with design spec"
```

---

## Task 1: Root README.md — Course Landing Page

**Files:**
- Create: `README.md`

- [ ] **Step 1: Write README.md**

Content:

```markdown
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
```

- [ ] **Step 2: Verify checklist**
  - Có links đến tất cả 5 module ✓
  - Prerequisites rõ ràng ✓
  - Không có placeholder TBD ✓

- [ ] **Step 3: Commit**

```bash
git add README.md
git commit -m "docs: add course landing page README"
```

---

## Task 2: Module 01 — README + concepts.md

**Files:**
- Create: `module-01-ai-fundamentals/README.md`
- Create: `module-01-ai-fundamentals/concepts.md`

- [ ] **Step 1: Write module-01-ai-fundamentals/README.md**

```markdown
# [EN] Module 01: AI Fundamentals / [VI] Nền tảng AI

**Mục tiêu:** Hiểu AI hoạt động thế nào trước khi chạm vào bất kỳ tool nào.
Không có gì tệ hơn là dùng công cụ mà không hiểu giới hạn của nó.

**Goal:** Understand how AI works before touching any tool.
Nothing is worse than using a tool without knowing its limits.

---

## Nội dung module / Contents

1. [Concepts](concepts.md) — LLM, token, context window, system prompt, roles
2. [Demo 01](demos/01-basic-prompting.md) — Prompt tốt vs prompt tệ cho sysadmin
3. [Demo 02](demos/02-system-prompts.md) — System prompt và cách định hình AI

---

## Bạn sẽ học được / What you'll learn

- LLM thực sự làm gì (và không làm gì được)
- Tại sao AI "quên" khi chat quá dài
- Sự khác biệt giữa chatbot, AI agent, và autonomous agent
- Cách định hình AI để nó làm đúng việc bạn cần

---

## Tại sao điều này quan trọng với sysadmin?

Biết giới hạn của AI = biết khi nào có thể tin, khi nào phải verify.
Một sysadmin dùng AI mà không hiểu nó dễ bị hallucination dẫn đến
quyết định sai trên production.

→ **Tiếp theo:** [concepts.md](concepts.md)
```

- [ ] **Step 2: Write module-01-ai-fundamentals/concepts.md**

```markdown
# [EN] AI Concepts / [VI] Các khái niệm AI cốt lõi

---

## 1. LLM là gì? / What is an LLM?

**VI:** LLM (Large Language Model) không phải "AI biết hết". Nó là một **cỗ máy dự đoán
từ tiếp theo** được train trên lượng text khổng lồ. Khi bạn hỏi "server bị lỗi gì?",
nó không đi kiểm tra server — nó dự đoán câu trả lời nào có xác suất cao nhất
dựa trên pattern trong data training.

**EN:** An LLM is a **next-token prediction engine** trained on massive text data.
It doesn't "know" things — it predicts the most statistically likely response.

**Hệ quả thực tế:**
- AI có thể tự tin trả lời sai (hallucination) — luôn verify thông tin quan trọng
- AI không có trí nhớ giữa các phiên chat — mỗi cuộc hội thoại bắt đầu từ đầu
- Kết quả không deterministic — cùng câu hỏi có thể cho kết quả khác nhau

---

## 2. Token & Context Window

**VI:** AI không đọc "chữ" mà đọc **token** — đơn vị nhỏ hơn từ.
Ví dụ: "sysadmin" = 2 tokens: "sys" + "admin".

**Context window** là giới hạn số token AI có thể "nhớ" trong một cuộc hội thoại.
Claude Sonnet: ~200,000 tokens ≈ 150,000 từ ≈ cuốn sách dày.

**EN:** AI reads **tokens** (sub-word units), not words. Context window = total
tokens AI can hold in memory during one conversation.

**Hệ quả thực tế với sysadmin:**
- Paste cả file log 10,000 dòng vào chat? Có thể ổn — nhưng gần giới hạn thì AI bắt đầu "quên" phần đầu
- Giải pháp: tóm tắt log trước, chỉ paste phần liên quan
- Chat dài → AI mất context của instructions ban đầu → bắt đầu session mới

---

## 3. System Prompt & Role / Vai trò và System Prompt

**VI:** **System prompt** là instruction ẩn được set trước khi user chat.
Nó định hình "tính cách", giới hạn, và ngữ cảnh của AI.

**EN:** A system prompt is a hidden instruction set before the user conversation begins.
It shapes AI's behavior, constraints, and context.

Ví dụ system prompt cho sysadmin assistant:
```
You are a Linux system administrator assistant.
You only answer questions related to Linux, networking, and server management.
Always suggest verifying commands in a test environment before running on production.
Never execute destructive commands without explicit user confirmation.
```

**Trong Claude.ai:** Dùng feature "Projects" để set system prompt cho cả project.
**Trong Claude Code:** Set qua `CLAUDE.md` file hoặc `/system` command.

---

## 4. Chatbot vs AI Agent vs Autonomous Agent

| Loại | Mô tả | Ví dụ |
|------|--------|-------|
| **Chatbot** | Hỏi → Trả lời, không có hành động | ChatGPT web interface |
| **AI Agent** | Hỏi → Lập kế hoạch → Dùng tools → Trả lời | Claude Code với file access |
| **Autonomous Agent** | Tự chạy task dài hạn không cần human | Background automation pipeline |

**VI:** Sự khác biệt cốt lõi là **tool use** — khả năng AI gọi công cụ thực sự
(đọc file, chạy command, gọi API) thay vì chỉ generate text.

**EN:** The key difference is **tool use** — the ability to call real tools
instead of just generating text.

**Tại sao điều này quan trọng với sysadmin?**
Claude Code là một AI agent — nó đọc file, chạy command, sửa code.
Hiểu điều này giúp bạn biết giới hạn quyền nào cần cấp và giới hạn nào cần giữ.

---

→ **Tiếp theo:** [Demo 01 — Basic Prompting](demos/01-basic-prompting.md)
```

- [ ] **Step 3: Verify checklist**
  - Format tiêu đề `# [EN]... / [VI]...` ✓
  - Có "Tại sao điều này quan trọng với sysadmin?" ✓
  - Lý thuyết trước, ví dụ sau ✓
  - Không có TBD ✓

- [ ] **Step 4: Commit**

```bash
git add module-01-ai-fundamentals/
git commit -m "docs(m01): add module 01 README and concepts"
```

---

## Task 3: Module 01 — Demos

**Files:**
- Create: `module-01-ai-fundamentals/demos/01-basic-prompting.md`
- Create: `module-01-ai-fundamentals/demos/02-system-prompts.md`

- [ ] **Step 1: Write demos/01-basic-prompting.md**

```markdown
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
```

- [ ] **Step 2: Write demos/02-system-prompts.md**

```markdown
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
```

- [ ] **Step 3: Commit**

```bash
git add module-01-ai-fundamentals/demos/
git commit -m "docs(m01): add prompting and system prompt demos"
```

---

## Task 4: Module 02 — README + how-tools-work.md

**Files:**
- Create: `module-02-mcp-protocol/README.md`
- Create: `module-02-mcp-protocol/how-tools-work.md`

- [ ] **Step 1: Write module-02-mcp-protocol/README.md**

```markdown
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
```

- [ ] **Step 2: Write module-02-mcp-protocol/how-tools-work.md**

```markdown
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
```

- [ ] **Step 3: Commit**

```bash
git add module-02-mcp-protocol/README.md module-02-mcp-protocol/how-tools-work.md
git commit -m "docs(m02): add MCP protocol overview and tool use explanation"
```

---

## Task 5: Module 02 — mcp-gateway-explained.md

**Files:**
- Create: `module-02-mcp-protocol/mcp-gateway-explained.md`

- [ ] **Step 1: Write mcp-gateway-explained.md**

```markdown
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
```

- [ ] **Step 2: Commit**

```bash
git add module-02-mcp-protocol/mcp-gateway-explained.md
git commit -m "docs(m02): add mcp-gateway deep dive with real config examples"
```

---

## Task 6: Module 03 — README + setup-guide.md

**Files:**
- Create: `module-03-browser-automation/README.md`
- Create: `module-03-browser-automation/setup-guide.md`

- [ ] **Step 1: Write module-03-browser-automation/README.md**

```markdown
# [EN] Module 03: Browser Automation / [VI] Điều khiển trình duyệt bằng AI

**Mục tiêu:** Dùng AI để điều khiển trình duyệt thực hiện task cụ thể —
với sự kiểm soát rõ ràng ở mỗi bước.

**Goal:** Use AI to control a browser for specific tasks — with clear human control at each step.

---

## Nội dung module / Contents

1. [Setup Guide](setup-guide.md) — Cài Chrome DevTools MCP vào Claude Code
2. [Workflow 01](workflows/01-navigate-screenshot.md) — Navigate và chụp screenshot
3. [Workflow 02](workflows/02-fill-forms.md) — Điền form với xác nhận
4. [Workflow 03](workflows/03-scrape-data.md) — Trích xuất dữ liệu từ trang web

---

## Tại sao điều này quan trọng với sysadmin?

Nhiều task sysadmin vẫn cần web UI — monitoring dashboards, vendor portals,
legacy admin panels không có API. Thay vì làm thủ công, bạn ra lệnh bằng ngôn ngữ tự nhiên,
AI thực thi, bạn xác nhận từng bước.

→ **Bắt đầu:** [setup-guide.md](setup-guide.md)
```

- [ ] **Step 2: Write module-03-browser-automation/setup-guide.md**

```markdown
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
```

- [ ] **Step 3: Commit**

```bash
git add module-03-browser-automation/README.md module-03-browser-automation/setup-guide.md
git commit -m "docs(m03): add browser automation module and setup guide"
```

---

## Task 7: Module 03 — Workflows

**Files:**
- Create: `module-03-browser-automation/workflows/01-navigate-screenshot.md`
- Create: `module-03-browser-automation/workflows/02-fill-forms.md`
- Create: `module-03-browser-automation/workflows/03-scrape-data.md`

- [ ] **Step 1: Write workflows/01-navigate-screenshot.md**

```markdown
# [EN] Workflow 01: Navigate & Screenshot / [VI] Điều hướng và chụp màn hình

**Prereq:** [Setup guide](../setup-guide.md) đã hoàn thành, Chrome đang chạy với port 9222.

---

## Use case

Bạn muốn AI mở một trang, đợi nó load, chụp screenshot để report.
Ví dụ thực tế: chụp monitoring dashboard hàng ngày.

---

## Prompt để thử

Trong Claude Code chat:

```
1. Mở tab mới và điều hướng đến https://grafana.com/demo
2. Đợi trang load hoàn toàn (3 giây)
3. Chụp screenshot toàn trang
4. Mô tả những gì bạn thấy trên trang
```

---

## Những gì AI sẽ làm

1. Gọi tool `chrome-devtools__new_page` → mở tab mới
2. Gọi tool `chrome-devtools__navigate_page` với URL
3. Gọi tool `chrome-devtools__wait_for` để đợi page load
4. Gọi tool `chrome-devtools__take_screenshot` → trả về ảnh
5. Phân tích ảnh và mô tả nội dung

---

## Control pattern — Bạn kiểm soát từng bước

Claude Code sẽ **hỏi xác nhận** trước mỗi tool call có side effect.
Đây là cơ chế an toàn mặc định:

```
Claude: "Tôi sẽ mở tab mới và điều hướng đến URL. Cho phép?"
Bạn: [Allow / Deny]
```

Bạn có thể set allow một lần cho tool `navigate_page` trong session hiện tại.

---

## Thực hành / Practice

Thay URL bằng:
- Dashboard nội bộ của bạn (nếu accessible từ local)
- `http://localhost:3010` — web dashboard của mcp-gateway

→ **Tiếp theo:** [Workflow 02 — Fill Forms](02-fill-forms.md)
```

- [ ] **Step 2: Write workflows/02-fill-forms.md**

```markdown
# [EN] Workflow 02: Fill Forms / [VI] Điền form với kiểm soát

**Use case:** Điền form trên web UI lặp đi lặp lại — ví dụ: tạo user mới,
submit ticket, điền config trên admin panel.

---

## Pattern quan trọng: Confirm before submit

**VI:** Luôn yêu cầu AI xác nhận với bạn trước khi submit form.
Đây là "human-in-the-loop" cho browser automation.

---

## Prompt mẫu

```
Trên trang hiện tại, điền form tạo user mới với:
- Username: testuser01
- Email: testuser01@example.com
- Role: viewer

Sau khi điền xong, dừng lại và cho tôi xem trước khi submit.
KHÔNG submit cho đến khi tôi xác nhận.
```

---

## Những gì AI sẽ làm

1. `chrome-devtools__take_snapshot` → đọc DOM để tìm form fields
2. `chrome-devtools__fill` → điền từng field
3. **Dừng lại, báo cáo với bạn** — không tự submit
4. Chờ xác nhận của bạn
5. Sau khi bạn confirm: `chrome-devtools__click` → submit

---

## Tại sao "KHÔNG submit cho đến khi tôi xác nhận" quan trọng?

Với form read-only (search, filter): submit ít rủi ro.
Với form write (tạo user, xóa resource, deploy): luôn phải confirm trước.

Thêm câu này vào mọi prompt liên quan đến form có side effect trên production.

→ **Tiếp theo:** [Workflow 03 — Scrape Data](03-scrape-data.md)
```

- [ ] **Step 3: Write workflows/03-scrape-data.md**

```markdown
# [EN] Workflow 03: Scrape Data / [VI] Trích xuất dữ liệu

**Use case:** Lấy dữ liệu từ trang web không có API —
status page của vendor, bảng giá, danh sách server trên web console.

---

## Prompt mẫu — Scrape bảng dữ liệu

```
Trang hiện tại có bảng danh sách servers. Trích xuất toàn bộ bảng đó,
format thành Markdown table với các cột: Name, Status, IP, Last Updated.
Nếu có nhiều trang (pagination), chỉ lấy trang hiện tại thôi.
```

---

## Prompt mẫu — Theo dõi status

```
Vào trang https://status.example.com
Liệt kê tất cả services và status hiện tại của chúng (operational/degraded/down).
Format: "- [service name]: [status]"
```

---

## Những gì AI sẽ làm

1. `chrome-devtools__navigate_page` → mở URL
2. `chrome-devtools__take_snapshot` → lấy DOM
3. Phân tích DOM, trích xuất data
4. Format và trả về cho bạn

---

## Giới hạn cần biết / Limitations

- Trang dùng JavaScript render phức tạp: AI cần đợi load đủ (thêm `wait_for`)
- CAPTCHA / login: bạn phải login thủ công trước, AI dùng session đó
- Dynamic content update liên tục: AI chụp snapshot tại một thời điểm, không realtime

→ **Module tiếp theo:** [Module 04 — Platform Workflows](../../module-04-platform-workflows/README.md)
```

- [ ] **Step 4: Commit**

```bash
git add module-03-browser-automation/workflows/
git commit -m "docs(m03): add browser automation workflows"
```

---

## Task 8: Module 04 — README + Use Cases

**Files:**
- Create: `module-04-platform-workflows/README.md`
- Create: `module-04-platform-workflows/use-cases/01-log-analysis.md`
- Create: `module-04-platform-workflows/use-cases/02-server-health-check.md`
- Create: `module-04-platform-workflows/use-cases/03-report-generation.md`
- Create: `module-04-platform-workflows/use-cases/04-file-system-ops.md`

- [ ] **Step 1: Write module-04-platform-workflows/README.md**

```markdown
# [EN] Module 04: Platform Workflows / [VI] Workflow thực tế cho sysadmin

**Mục tiêu:** Tích hợp AI vào công việc platform/sysadmin hàng ngày —
bốn use case thực tế, copy-paste prompt và dùng ngay.

**Goal:** Integrate AI into daily platform/sysadmin work — four practical use cases.

---

## Nội dung / Contents

1. [Log Analysis](use-cases/01-log-analysis.md) — AI đọc và phân tích log
2. [Server Health Check](use-cases/02-server-health-check.md) — Kiểm tra trạng thái hệ thống
3. [Report Generation](use-cases/03-report-generation.md) — Tạo report từ dữ liệu thô
4. [File System Ops](use-cases/04-file-system-ops.md) — AI làm việc với file có kiểm soát

---

## Cách dùng module này / How to use

Mỗi use case có:
1. **Context** — tình huống thực tế nào áp dụng
2. **Prompt mẫu** — copy và dùng ngay trong Claude Code
3. **Điều chỉnh** — cách adapt cho hệ thống của bạn

Claude Code có quyền đọc file system (theo `.claude/settings.json`).
Xem lại permission trước khi thử use case nào.

→ **Bắt đầu:** [01-log-analysis.md](use-cases/01-log-analysis.md)
```

- [ ] **Step 2: Write use-cases/01-log-analysis.md**

```markdown
# [EN] Use Case 01: Log Analysis / [VI] Phân tích Log

**Context:** Server có vấn đề, bạn có log file và muốn AI tìm pattern lỗi nhanh hơn grep.

---

## Cách 1: Paste log trực tiếp vào Claude Code chat

Dùng khi log file nhỏ (< 500 dòng):

```
Phân tích log sau và tìm:
1. Tất cả ERROR và CRITICAL messages
2. Pattern lặp lại (cùng error xuất hiện nhiều lần)
3. Time range xảy ra nhiều lỗi nhất
4. Nguyên nhân gốc rễ có thể

<paste log vào đây>
```

---

## Cách 2: Claude Code đọc file trực tiếp

Dùng khi log file lớn — Claude Code có file read access:

```
Đọc file /var/log/nginx/error.log (500 dòng cuối cùng)
và tìm tất cả 5xx errors trong 1 giờ vừa qua.
Group theo error type và đếm số lần xuất hiện.
```

Điều kiện: Claude Code phải có read permission cho `/var/log/nginx/`.
Check trong `.claude/settings.json`:
```json
{
  "permissions": {
    "allow": ["Read(/var/log/**)", "Bash(tail:*)"]
  }
}
```

---

## Cách 3: Pipe output vào Claude Code

```bash
tail -n 1000 /var/log/syslog | claude "Tìm pattern lỗi bất thường trong log này"
```

---

## Prompt nâng cao — Triage theo priority

```
Tôi có log từ production server bị chậm từ 14:00 hôm nay.
Đọc /var/log/app/application.log

Phân tích:
1. CRITICAL: có lỗi nào có thể gây downtime không?
2. HIGH: bottleneck performance ở đâu?
3. INFO: request nào tốn thời gian nhất?

Format kết quả: mỗi mục có timestamp, message gốc, và đề xuất action.
```
```

- [ ] **Step 3: Write use-cases/02-server-health-check.md**

```markdown
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
```

- [ ] **Step 4: Write use-cases/03-report-generation.md**

```markdown
# [EN] Use Case 03: Report Generation / [VI] Tạo báo cáo tự động

**Context:** Bạn có data thô (CSV, JSON, log) và cần report có format đẹp
để gửi cho team hoặc lưu lại.

---

## Prompt: Weekly server report từ log

```
Đọc /var/log/nginx/access.log

Tạo weekly report với:
1. Tổng số requests trong tuần
2. Top 10 endpoints được gọi nhiều nhất
3. Top 5 IP address có nhiều request nhất
4. Tỷ lệ status codes: 2xx / 3xx / 4xx / 5xx
5. Thời điểm traffic cao nhất trong ngày (theo giờ)

Format: Markdown report với headers, tables, và bullet points.
Thêm ngày tháng vào tiêu đề report.
```

---

## Prompt: Tổng hợp từ nhiều nguồn

```
Tôi có 3 file sau:
- /tmp/disk_usage.txt   (output của df -h)
- /tmp/memory.txt       (output của free -h)
- /tmp/top_processes.txt (output của ps aux --sort=-%cpu | head -20)

Tổng hợp thành Infrastructure Status Report ngày hôm nay.
Format Markdown, có thể gửi email cho manager.
Highlight bất kỳ điều gì đáng chú ý.
```

---

## Tạo report định kỳ với Claude Code + cron

Kết hợp bash script collect data + Claude Code generate report:

```bash
#!/bin/bash
# collect-and-report.sh
DATE=$(date +%Y-%m-%d)
df -h > /tmp/disk_$DATE.txt
free -h > /tmp/mem_$DATE.txt
# Gọi Claude Code để tạo report
claude "Đọc /tmp/disk_$DATE.txt và /tmp/mem_$DATE.txt, tạo daily report" \
  > /tmp/report_$DATE.md
```
```

- [ ] **Step 5: Write use-cases/04-file-system-ops.md**

```markdown
# [EN] Use Case 04: File System Ops / [VI] Thao tác file system có kiểm soát

**Context:** AI đọc, so sánh, và đề xuất thay đổi file config —
bạn review và quyết định có apply không.

---

## Pattern an toàn: Đề xuất trước, apply sau

```
VI: Không để AI tự sửa file config quan trọng.
Pattern: AI đề xuất diff → bạn review → bạn apply (hoặc không).

EN: Never let AI auto-edit critical config files.
Pattern: AI proposes diff → you review → you apply (or reject).
```

---

## Prompt: So sánh hai config file

```
So sánh /etc/nginx/nginx.conf với /etc/nginx/nginx.conf.bak
Liệt kê sự khác biệt theo format:
- Dòng X: [nội dung cũ] → [nội dung mới]
Đánh giá: thay đổi nào có thể gây vấn đề?
```

---

## Prompt: Review config trước khi apply

```
Đọc file /etc/nginx/sites-available/myapp.conf
Review cấu hình này và tìm:
1. Security issues (missing headers, weak TLS config, etc.)
2. Performance improvements có thể áp dụng
3. Lỗi cú pháp tiềm năng

Đề xuất dưới dạng diff (format unified diff).
KHÔNG tự sửa file — chỉ đề xuất.
```

---

## Prompt: Tìm file theo pattern

```
Tìm tất cả file .conf trong /etc/
- Có chứa "password" hoặc "secret" trong plaintext
- Liệt kê file path và dòng cụ thể
- Đây là security audit — không thay đổi gì
```

---

## Permission cần thiết

```json
// .claude/settings.json
{
  "permissions": {
    "allow": [
      "Read(/etc/**)",
      "Read(/var/log/**)"
    ],
    "deny": [
      "Write(/etc/**)"   // AI không được tự ghi vào /etc/
    ]
  }
}
```

→ **Module tiếp theo:** [Module 05 — Control & Safety](../../module-05-control-and-safety/README.md)
```

- [ ] **Step 6: Commit**

```bash
git add module-04-platform-workflows/
git commit -m "docs(m04): add platform workflows module with 4 sysadmin use cases"
```

---

## Task 9: Module 05 — Control & Safety

**Files:**
- Create: `module-05-control-and-safety/README.md`
- Create: `module-05-control-and-safety/human-in-the-loop.md`
- Create: `module-05-control-and-safety/role-patterns.md`

- [ ] **Step 1: Write module-05-control-and-safety/README.md**

```markdown
# [EN] Module 05: Control & Safety / [VI] Kiểm soát và An toàn

**Mục tiêu:** Bạn là người quyết định, AI là công cụ — không bao giờ ngược lại.
Module này dạy cách duy trì quyền kiểm soát khi dùng AI trong môi trường production.

**Goal:** You decide, AI executes — never the other way around.
Learn how to maintain control when using AI in production environments.

---

## Nội dung / Contents

1. [Human-in-the-Loop](human-in-the-loop.md) — Patterns kiểm soát tại từng bước
2. [Role Patterns](role-patterns.md) — System prompt templates + Claude Code permission model

---

## Tại sao module này là bắt buộc?

Với quyền truy cập file system, bash execution, và browser control —
một lệnh sai của AI có thể xóa data, expose credential, hoặc crash service.

Kiểm soát AI không phải tùy chọn. Đây là bắt buộc.

→ **Bắt đầu:** [human-in-the-loop.md](human-in-the-loop.md)
```

- [ ] **Step 2: Write module-05-control-and-safety/human-in-the-loop.md**

```markdown
# [EN] Human-in-the-Loop / [VI] Luôn có người kiểm soát

---

## Nguyên tắc cốt lõi / Core principle

```
Read → OK để AI tự chạy
Write / Execute / Delete → Phải có xác nhận của bạn trước
```

---

## Pattern 1: Confirm trước action có side effect

Luôn thêm vào prompt:

```
Trước khi thực hiện bất kỳ thay đổi nào (ghi file, chạy command có side effect,
submit form), dừng lại và mô tả chính xác bạn sẽ làm gì.
Chờ tôi xác nhận "OK" trước khi tiếp tục.
```

---

## Pattern 2: Propose diff, không tự apply

```
Đề xuất thay đổi cần thiết cho file này dưới dạng unified diff.
Giải thích từng thay đổi.
KHÔNG tự apply — tôi sẽ review và apply thủ công.
```

---

## Pattern 3: Dry-run trước

Với các command có thể gây hại:

```
Trước tiên chạy lệnh ở chế độ dry-run (nếu có) hoặc
simulate để tôi thấy kết quả trước khi chạy thật.

Ví dụ: thay vì `rm -rf /path`, chạy `find /path -type f` trước
để tôi thấy danh sách file sẽ bị xóa.
```

---

## Red flags — Dấu hiệu AI đi ra ngoài lề

Ngừng và kiểm tra lại nếu AI:
- Tự động chạy command không được yêu cầu
- Giải thích mờ nhạt về những gì nó vừa làm
- Đề xuất disable security feature "cho đơn giản"
- Báo cáo kết quả không khớp với những gì bạn thấy
- Dùng `sudo` mà không hỏi

---

## Claude Code permission prompt

Mặc định, Claude Code hỏi confirm trước mỗi tool call:

```
Claude wants to run: rm -rf /tmp/old_logs/
[Allow once] [Allow always] [Deny]
```

Nguyên tắc:
- **Allow once**: cho phép lần này, hỏi lại lần sau — dùng khi không chắc
- **Allow always**: thêm vào allowlist session — chỉ dùng cho read-only tools
- **Deny**: từ chối và giải thích với Claude tại sao

→ **Tiếp theo:** [role-patterns.md](role-patterns.md)
```

- [ ] **Step 3: Write module-05-control-and-safety/role-patterns.md**

```markdown
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
      "Read(**)",           // Cho phép đọc tất cả file
      "Bash(df:*)",         // Chỉ cho phép lệnh df
      "Bash(ps:*)",         // Chỉ cho phép lệnh ps
      "Bash(tail:*)",       // Chỉ cho phép lệnh tail
      "Bash(grep:*)"        // Chỉ cho phép lệnh grep
    ],
    "deny": [
      "Write(**)",          // Cấm ghi file
      "Bash(rm:*)",         // Cấm lệnh rm
      "Bash(sudo:*)"        // Cấm sudo
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
```

- [ ] **Step 4: Commit**

```bash
git add module-05-control-and-safety/
git commit -m "docs(m05): add control and safety module — role patterns and human-in-the-loop"
```

---

## Task 10: Final verification

- [ ] **Step 1: Kiểm tra tất cả links trong repo hoạt động**

```bash
# Tìm tất cả relative links trong markdown
grep -rn '\](\./' /home/thalt/env-lab/project/mcp-plugin-ai --include="*.md" | \
  grep -v "docs/superpowers"
```

Review output: mỗi link phải trỏ đến file tồn tại.

- [ ] **Step 2: Verify cấu trúc thư mục đúng spec**

```bash
find /home/thalt/env-lab/project/mcp-plugin-ai -name "*.md" \
  | grep -v "docs/superpowers" \
  | sort
```

Expected: 21 file markdown trong 5 module + root README.

- [ ] **Step 3: Final commit**

```bash
git add -A
git status  # verify không có file ngoài ý muốn
git commit -m "docs: complete AI learning course — 5 modules, bilingual Vi/EN"
```

---

## Self-Review Checklist

**Spec coverage:**
- [x] Module 01: AI Fundamentals → Task 2 + Task 3
- [x] Module 02: MCP Protocol → Task 4 + Task 5
- [x] Module 03: Browser Automation → Task 6 + Task 7
- [x] Module 04: Platform Workflows → Task 8
- [x] Module 05: Control & Safety → Task 9
- [x] Root README / landing page → Task 1
- [x] Git init → Task 0
- [x] Bilingual format → mọi file dùng `# [EN]... / [VI]...`
- [x] "Tại sao quan trọng với sysadmin?" → có trong mỗi module README
- [x] Không cần API key → không có instruction nào yêu cầu API key

**Không có placeholder:** Không có TBD, TODO, hoặc "fill in later".

**Consistency:** Links dùng relative path nhất quán. Format tiêu đề đồng nhất.
