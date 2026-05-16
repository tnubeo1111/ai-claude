# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

`mcp-plugin-ai` là một **khóa học AI có cấu trúc**, song ngữ (Tiếng Việt / English), dành cho sysadmin và platform engineer muốn hiểu và tích hợp AI vào công việc thực tế.

Mục tiêu: không phải build sản phẩm — mà là hiểu cơ chế AI agent và dùng AI như công cụ có kiểm soát.

## Structure

```
mcp-plugin-ai/
├── README.md                          # Landing page, bản đồ học
├── module-01-ai-fundamentals/         # LLM, token, context window, roles + 2 demos
├── module-02-mcp-protocol/            # Tool use flow, MCP components, gateway
├── module-03-browser-automation/      # Chrome DevTools MCP setup + 3 workflows
├── module-04-platform-workflows/      # 4 use cases: log, health check, report, file ops
├── module-05-control-and-safety/      # Human-in-the-loop, role patterns, permissions
└── docs/superpowers/                  # Design spec + implementation plan
```

## Content Conventions

- Tiêu đề: `# [EN] Title / [VI] Tiêu đề`
- Lý thuyết trước, ví dụ sau
- Mỗi file có section "Tại sao điều này quan trọng với sysadmin?"
- Links dùng relative path
- Không có code phức tạp — shell commands, config files, prompt examples

## Target Audience

- Background: system admin / platform engineer
- Dùng Claude Pro + Claude Code CLI (không cần Anthropic API key)
- Chưa có kinh nghiệm AI agent, LLM, MCP

## GitHub

Repo: `https://github.com/tnubeo1111/ai-claude` (branch: master)
