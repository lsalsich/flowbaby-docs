---
sidebar_position: 1
slug: /
---

# Flowbaby Chat Memory

> Memory-augmented chat for VS Code using knowledge graphs

Flowbaby Chat Memory is a VS Code extension that lets you selectively capture important chat conversations and retrieve them as context through the `@flowbaby-memory` participant. Each workspace maintains its own isolated memory, creating a personalized knowledge graph that grows with your project.

## Features

- **Selective Capture** — Use keyboard shortcut (Ctrl+Alt+C / Cmd+Alt+C) to capture valuable conversations worth remembering
- **@flowbaby-memory Participant** — Retrieves relevant context and generates informed responses when you explicitly invoke it
- **Keyboard Shortcut Workflow** — Press Ctrl+Alt+C, paste or type content, instant capture with confirmation
- **Command Palette Alternative** — Run "Flowbaby: Capture to Memory" for the same capture workflow
- **Workspace Isolation** — Each workspace has its own separate memory—no cross-project leakage
- **Hybrid Graph-Vector Search** — Combines relationship traversal with semantic similarity for superior context relevance
- **User Control** — You decide what gets captured; explicit memory actions put you in full control
- **Privacy-First Design** — All data stays on your local machine; no cloud services or telemetry

## Prerequisites

Before installing the extension, ensure you have:

- **VS Code** 1.85.0 or higher
- **Python** 3.8+ installed and available in PATH

:::note
Flowbaby now manages its own Python environment automatically. You no longer need to manually install `cognee` globally.
:::

## Quick Example

When you ask your AI agent about a previous decision:

> "@flowbaby-memory How did we implement caching?"

The participant will:

1. Retrieve relevant memories from your workspace knowledge graph
2. Show previews: "📚 Retrieved 3 memories"
3. Augment your question with retrieved context
4. Generate a contextually-aware response

No more re-explaining your project setup. No more inconsistent suggestions. Just intelligent, context-aware AI assistance.

---

Ready to get started? Head to the [Getting Started](./getting-started) guide.
