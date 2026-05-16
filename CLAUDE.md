# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Status

This project is not yet initialized — no source files exist yet. The `.claude/` directory is the only content.

## Context

This project (`mcp-plugin-ai`) sits alongside [`mcp-gateway`](../mcp-gateway) in the same workspace. `mcp-gateway` is a TypeScript/Express aggregator that proxies multiple upstream MCP servers into a single endpoint for AI agents. `mcp-plugin-ai` is likely a plugin or client that integrates with that gateway or with the MCP protocol directly.

The `.claude/settings.local.json` grants read access across all projects under `/home/thalt/env-lab/`, which can be useful for cross-referencing sibling projects during development.

## Sibling Reference: mcp-gateway

Key patterns from `mcp-gateway` that may be reused here:

- **Transport types**: `streamable-http` (MCP 2025-11-25), `sse` (MCP 2024-11-05), `fastmcp` (Ceph custom), `stdio`
- **Tool namespacing**: tools are prefixed with server ID, e.g. `ceph_alpha__get_health_summary`
- **Gateway endpoint**: `http://localhost:3010/sse?apiKey=mcp_gateway_secret_123`
- **Stack**: TypeScript, Node.js, Express, Zod for config validation
