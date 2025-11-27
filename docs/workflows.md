---
sidebar_position: 4
---

# Workflows

Learn effective patterns for using Flowbaby in your daily development.

## Capturing Conversations

### Keyboard Shortcut (Primary Method)

1. View a valuable chat message (from any participant: @workspace, @terminal, GitHub Copilot, etc.)
2. Press **Ctrl+Alt+C** (or **Cmd+Alt+C** on macOS)
3. Paste the message content in the input box (or leave empty to use clipboard)
4. Press Enter to capture
5. See "Memory staged – processing will finish in ~1–2 minutes" confirmation
6. Continue working—you'll receive a completion notification when ready

### Command Palette (Alternative)

1. Open Command Palette (`Ctrl+Shift+P` / `Cmd+Shift+P`)
2. Type "Flowbaby: Capture to Memory"
3. Follow the same workflow as keyboard shortcut

## Retrieving Context with @flowbaby-memory

### How to Use

1. Open GitHub Copilot Chat (`Ctrl+Alt+I` or click chat icon)
2. Type: `@flowbaby-memory How did I implement caching?`
3. The participant:
   - Retrieves relevant memories from your workspace knowledge graph
   - Shows previews: "📚 Retrieved 3 memories"
   - Augments your question with retrieved context
   - Generates a contextually-aware response

### Example Queries

- `@flowbaby-memory What problems did we discuss about the authentication system?`
- `@flowbaby-memory What solutions did we consider for rate limiting?`
- `@flowbaby-memory Summarize our decisions about database architecture`

## Creating Conversation Summaries

Conversation summaries are structured records that capture the essence of a chat session.

### What's Included in a Summary

- Main topic and context
- Key decisions made
- Rationale behind decisions
- Open questions still unresolved
- Next steps to take
- References to files, plans, or other resources

### When to Create Summaries

Create a summary when you've:

- Completed a design discussion with important decisions
- Resolved a complex debugging issue with lessons learned
- Made architectural choices that should be remembered
- Discussed tradeoffs between different approaches
- Reached conclusions about implementation direction

### Summary Schema

Each summary follows this structured format:

```markdown
Summary: [Short title]

Topic: [Main focus of the conversation]
Context: [1-3 sentences explaining what you were working on and why]
Decisions:
- [Key decision 1]
- [Key decision 2]
Rationale:
- [Why decision 1 was made]
Open Questions:
- [Unresolved question 1]
Next Steps:
- [Action item 1]
References:
- [File path, plan ID, or other reference]
Time Scope: [Time range, e.g., "Nov 17 14:00-16:30"]
```

### How to Create a Summary

1. **Open GitHub Copilot Chat** (`Ctrl+Alt+I` / `Cmd+Alt+I`)
2. **Start a conversation with @flowbaby-memory** and type:
   - `@flowbaby-memory summarize this conversation`
   - Or: `@flowbaby-memory remember this session`
   - Or: `@flowbaby-memory create summary`
3. **Review the scope preview**: Extension shows "I'll summarize the last 15 turns"
4. **Adjust turn count (optional)**: Type a number to change scope
5. **Review the generated summary**
6. **Confirm storage**: Reply `yes`, `store it`, or `save` to confirm

### Turn Count Guidance

- **Short sessions (5-15 turns)**: Good for focused discussions, bug fixes, quick decisions
- **Medium sessions (15-30 turns)**: Typical for feature planning, architecture discussions
- **Long sessions (30-50 turns)**: Complex multi-topic conversations; consider breaking into multiple summaries

### Best Practices

- **Create summaries at natural breakpoints**: After reaching a decision, completing a design, or resolving an issue
- **Keep summaries focused**: One main topic per summary for better retrieval precision
- **Review before storing**: Check that LLM correctly identified key points
- **Include explicit references**: Mention plan IDs, file paths, or issue numbers in conversation for automatic extraction
- **Balance detail and brevity**: Aim for 300-600 tokens total

## Async Ingestion Behavior

Starting in v0.3.3, memory ingestion operates asynchronously to prevent blocking your workflow.

### Timing Expectations

- **Capture Response**: 5-10 seconds—you can continue working immediately after capture
- **Background Processing**: 60-90 seconds—knowledge graph construction happens in the background
- **Total Time**: ~1-2 minutes from capture to searchable memory

### Staged Messaging

When you capture a memory, you'll see:

> **"Memory staged – processing will finish in ~1–2 minutes. You'll get a notification when it's done."**

This means:

- ✅ Your content has been safely staged for processing
- ✅ You can continue working without waiting
- ⏳ Knowledge graph construction is running in the background
- 🔔 You'll receive a notification when processing completes

### Completion Notifications

After background processing finishes, you'll receive one of two notifications:

- **Success** (ℹ️ Info): "✅ Cognify finished" with workspace name, summary digest, elapsed time, and entity count
- **Failure** (⚠️ Warning): "⚠️ Cognify failed" with workspace name, summary digest, and remediation guidance

### Background Status

To check all in-flight operations:

1. Press `Cmd+Shift+P` (or `Ctrl+Shift+P` on Linux/Windows)
2. Type "Flowbaby: View Background Operations"
3. View pending, running, completed, and failed operations

## Using Flowbaby Tools with Custom Agents

Flowbaby provides **Language Model Tools** that allow GitHub Copilot and custom agents to autonomously access workspace memory.

### Quick Start

1. **Enable Tools via Configure Tools UI**:
   - Open Copilot chat → Click "Tools" (⚙️ icon) → "Configure Tools"
   - Find "Store Memory in Flowbaby" and "Retrieve Flowbaby Memory"
   - Toggle tools on/off individually (disabled by default for privacy)

2. **Use in Chat**:
   - Type `#flowbaby` to see autocomplete suggestions
   - Select `#flowbabyStoreSummary` or `#flowbabyRetrieveMemory`
   - Tools appear only when enabled via Configure Tools

### Custom Agent Example

Create a `.agent.md` file in your workspace to define a memory-aware agent:

```markdown
---
name: Memory-Aware Code Assistant
description: Copilot assistant with access to workspace memory
tools: ['search', 'flowbabyStoreSummary', 'flowbabyRetrieveMemory']
---

You are a code assistant with access to workspace-specific memory.

When the user asks about past decisions or implementations:
1. Use #flowbaby_retrieveMemory to search for relevant context
2. Ground your answer in the retrieved memories
3. If no memories exist, use your training data but clarify it's not workspace-specific

When the user completes an important implementation or makes a decision:
1. Offer to store a summary using #flowbaby_storeMemory
2. Include topic, context, and key decisions in the summary
```

### Available Tools

#### Store Memory Tool (`#flowbabyStoreSummary`)

Stores conversation summaries in Flowbaby knowledge graph.

**Parameters**:

- `topic` (required): Summary title
- `context` (required): Summary description
- `decisions` (optional): Key decisions made
- `rationale` (optional): Reasoning behind decisions
- `metadata` (optional): Plan ID, status, etc.

#### Retrieve Memory Tool (`#flowbabyRetrieveMemory`)

Searches Flowbaby knowledge graph for relevant memories.

**Parameters**:

- `query` (required): Natural language search query
- `maxResults` (optional): Max results to return (default: 3, max: 10)

**Returns**: Both narrative markdown and structured JSON for agent parsing.
