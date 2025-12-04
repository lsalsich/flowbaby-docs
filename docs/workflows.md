---
sidebar_position: 4
---

# Workflows

Learn effective patterns for using Flowbaby in your daily development.

## Usage

### 1. Context-Aware Automatic Memory Search

Flowbaby can automatically search your workspace memory and surface relevant context into GitHub Copilot chats.

**How it works**:
- Flowbaby watches for conversation cues (e.g., "How did I implement…?", "What did we decide about…?").
- When it detects a good opportunity, it runs a background search against your knowledge graph.
- Retrieved memories are added to the Copilot request as additional context so you don't have to restate prior work.

**What you'll see**:
- In Copilot Chat, Flowbaby shows a section like **"📚 Retrieved memories"** with short previews.
- Copilot's answer incorporates those memories directly into its response.

### 2. Context-Aware Automatic Memory Storage

Flowbaby can also decide when to summarize and store parts of the conversation as long-term memory.

**How it works**:
- Flowbaby looks for moments where you've reached a decision, finished a debugging session, or explained an important concept.
- It generates a structured summary and stores it in your workspace knowledge graph (after any required confirmation, depending on settings).

**Benefits**:
- You build up high-value memory over time with minimal manual effort.
- Later queries can retrieve these summaries instead of raw, noisy chat logs.

### 3. Using the @flowbaby Chat Participant

The `@flowbaby` participant lets you directly query your workspace memory.

**How to use**:
1. Open GitHub Copilot Chat (`Ctrl+Alt+I` or click the chat icon).
2. Address Flowbaby explicitly: `@flowbaby How did I implement caching?`
3. Flowbaby:
   - Retrieves relevant memories from your knowledge graph.
   - Shows previews under **"📚 Retrieved memories"**.
   - Augments your question with that context.
   - Generates a context-aware response.

**Example queries**:
- `@flowbaby What problems did we discuss about the authentication system?`
- `@flowbaby What solutions did we consider for rate limiting?`
- `@flowbaby Summarize our decisions about database architecture`

### 4. Keyboard Shortcut and Command Palette Capture

Use these flows when you want to explicitly capture important information.

**Keyboard shortcut**:
1. View a valuable chat message (from any participant: @workspace, @terminal, GitHub Copilot, etc.).
2. Press **Ctrl+Alt+F** (or **Cmd+Alt+F** on macOS).
3. Paste or confirm the content in the capture input.
4. Press Enter to capture.
5. You'll see a staged message (e.g., "Memory staged - processing will finish in ~1–2 minutes").

**Command Palette**:
1. Open Command Palette (`Ctrl+Shift+P` / `Cmd+Shift+P`).
2. Run **"Flowbaby: Capture to Memory"**.
3. Follow the same flow as the keyboard shortcut.

### 5. Background Async Ingestion

Flowbaby processes captured memories asynchronously so your editor stays responsive.

**Timeline**:
- Capture confirmation: ~5–10 seconds.
- Background processing and graph construction: ~60–90 seconds.
- Total time from capture to searchable memory: ~1–2 minutes.

You'll receive a notification when ingestion finishes (success or failure), including a brief digest and basic metrics in the logs.

### 6. Viewing Background Operations

To inspect everything Flowbaby is doing in the background:
1. Open Command Palette.
2. Run **"Flowbaby: View Background Operations"**.
3. Review pending, running, completed, and failed ingestion tasks.

### 7. How Flowbaby Stores Summaries

In normal use, Flowbaby creates and maintains summaries for you automatically.

**Automatic summary creation**:
- When you reach an important conclusion, finish a debugging session, or make a design decision, Flowbaby may create a structured summary in the background.
- These summaries capture topic, key decisions, rationale, open questions, and next steps.
- They are stored in your workspace knowledge graph and later used by automatic search and the `@flowbaby` participant.

**Manual and agent-driven summaries (optional)**:
- You can still ask Flowbaby to create a summary explicitly if you want tighter control.
- In Copilot Chat, you can say things like:
  - `@flowbaby summarize this conversation`
  - `@flowbaby remember this session`
  - `@flowbaby create summary for this plan`
- Custom agents can also store summaries directly using Flowbaby's tools and APIs (see the Flowbaby docs at [docs.flowbaby.ai](https://docs.flowbaby.ai)).

The key idea: you don't need to manage summaries manually unless you want to - Flowbaby's automatic storage is usually enough.

### 8. How Flowbaby Retrieves Summaries

Flowbaby uses summaries as a primary source of truth when answering questions about past work.

**Automatic retrieval**:
- When context-aware search (Section 1) or the `@flowbaby` participant runs a query, Flowbaby searches both raw captured conversations and structured summaries.
- When a good match is found, you'll see a **"📚 Retrieved memories"** section with previews of the most relevant items.

**What summaries look like**:
- Organized sections: topic, key decisions, open questions, next steps, rationale.
- Rich, human-readable text designed to be useful both to you and to the LLM.

**How to prompt for past work**:
- `@flowbaby What did we decide about Plan 013?`
- `@flowbaby What questions are still open about memory transparency?`
- `@flowbaby What are the next steps for the authentication system?`
- `@flowbaby Show me the rationale for using enriched text format`

You don't need a separate "retrieve summary" command-just ask `@flowbaby` questions about previous sessions or decisions, and Flowbaby will use summaries automatically when available.

### 9. Memory Management Commands

**Toggle Memory On/Off**:
- Command Palette → "Flowbaby: Toggle Memory"
- Flips `Flowbaby.enabled` setting

**Clear Workspace Memory**:
- Command Palette → "Flowbaby: Clear Workspace Memory"
- Deletes all captured conversations for current workspace (requires confirmation)
