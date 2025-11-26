---
sidebar_position: 2
---

# Getting Started

Get Flowbaby up and running in under 5 minutes.

## Prerequisites

- **VS Code** 1.85.0 or later
- **GitHub Copilot** extension with agent mode enabled
- A workspace/project folder open in VS Code

## Installation

### From VS Code Marketplace

1. Open VS Code
2. Go to Extensions (`Ctrl+Shift+X` / `Cmd+Shift+X`)
3. Search for "Flowbaby"
4. Click **Install**

### From Command Line

```bash
code --install-extension flowbaby.flowbaby
```

## First-Time Setup

Once installed, Flowbaby works automatically with GitHub Copilot's agent mode. No additional configuration is required.

### Verify Installation

1. Open a workspace in VS Code
2. Open the Command Palette (`Ctrl+Shift+P` / `Cmd+Shift+P`)
3. Type "Flowbaby" — you should see available commands

### Check the Knowledge Graph Location

Flowbaby stores memories in a `.flowbaby/` folder in your workspace root:

```
your-project/
├── .flowbaby/
│   └── knowledge-graph.db
├── src/
├── package.json
└── ...
```

:::tip
Add `.flowbaby/` to your `.gitignore` if you don't want to commit the knowledge graph, or keep it tracked for team-shared context.
:::

## Using Flowbaby

Once installed, Flowbaby integrates seamlessly with GitHub Copilot's agent mode.

### Storing Memories

When you complete significant work, the AI agent will automatically call `flowbaby_storeMemory` to save:

- What was done
- Key decisions made
- Rationale behind choices
- Important files and components

### Retrieving Memories

When you ask questions about your project, the agent will call `flowbaby_retrieveMemory` to:

- Find relevant past context
- Look up previous decisions
- Recall implementation details

### Example Workflow

**Session 1: Initial Setup**

You: "Set up Redis caching for our API responses"

The agent:
1. Implements the caching solution
2. Stores a memory: *"Implemented Redis caching for API responses. Used ioredis client with 5-minute TTL. Decided on cache-aside pattern for simplicity."*

**Session 2: Days Later**

You: "How does our caching work?"

The agent:
1. Retrieves the stored memory about Redis caching
2. Responds with accurate, contextual information

No more re-explaining or inconsistent answers!

## Next Steps

- [Configuration](/docs/configuration) — Customize Flowbaby's behavior
- [Workflows](/docs/workflows) — Learn effective patterns for using Flowbaby
- [Troubleshooting](/docs/troubleshooting) — Common issues and solutions
