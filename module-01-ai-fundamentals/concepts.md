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
