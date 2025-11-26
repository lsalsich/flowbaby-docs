---
sidebar_position: 1
slug: /
---

# Introduction

**Flowbaby** is a VS Code extension that gives your AI coding agents long-term memory. It creates a persistent knowledge graph that stores context, decisions, and implementation details across sessions.

## The Problem

AI coding assistants like GitHub Copilot are powerful, but they forget everything between sessions. Every time you start a new conversation, you lose:

- **Context** about what you were working on
- **Decisions** you made and why
- **Implementation details** that took time to figure out
- **Project-specific knowledge** that the AI learned

This leads to repetitive explanations, inconsistent suggestions, and lost productivity.

## The Solution

Flowbaby solves this by providing two MCP tools that AI agents can use:

### `flowbaby_storeMemory`
Agents use this to save important context, decisions, and rationale to the knowledge graph. Memories are stored with rich metadata including topics, decisions, and status tracking.

### `flowbaby_retrieveMemory`
Agents use this to query past context before answering questions. This grounds their responses in your project's history and previous decisions.

## Key Features

- 🧠 **Automatic memory persistence** — AI agents remember context across sessions
- 📊 **Knowledge graph storage** — Memories are structured and queryable
- 🔍 **Semantic search** — Find relevant past context using natural language
- 📁 **Workspace-scoped** — Each project has its own memory
- 🔒 **Local-first** — Your data stays on your machine

## How It Works

1. **Install Flowbaby** from the VS Code Marketplace
2. **Enable agent mode** in GitHub Copilot
3. **Start coding** — agents will automatically store and retrieve memories
4. **Build up context** — the more you use it, the smarter your agents become

## Quick Example

When you ask your AI agent about a previous decision:

> "How did we implement caching?"

The agent will:
1. Call `flowbaby_retrieveMemory` with a relevant query
2. Get back structured memories with context, decisions, and rationale
3. Use that information to give you an accurate, contextual answer

No more re-explaining your project setup. No more inconsistent suggestions. Just intelligent, context-aware AI assistance.

---

Ready to get started? Head to the [Getting Started](/docs/getting-started) guide.
