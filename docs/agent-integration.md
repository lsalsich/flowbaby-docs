---
sidebar_position: 7
---

# Agent Integration

Flowbaby provides an API for GitHub Copilot agents and third-party VS Code extensions to store and retrieve structured summaries programmatically.

## Use Cases

- **Agent Continuity**: Agents can maintain context across sessions without requiring manual capture
- **Multi-Agent Collaboration**: Different agents can share memory via a common knowledge base
- **Custom Workflows**: Extensions can build custom agent memory patterns

## Agent Ingestion API

The `Flowbaby.ingestForAgent` command allows agents to write structured summaries to Flowbaby:

```typescript
const payload = {
  topic: "Plan 015 Implementation Discussion",
  context: "User discussed agent ingestion command design with architect.",
  decisions: [
    "Use VS Code commands as primary surface",
    "Implement workspace-global access model"
  ],
  rationale: [
    "Commands are accessible to Copilot agents",
    "VS Code doesn't expose caller identity"
  ],
  metadata: {
    topicId: "plan-015-implementation",
    sessionId: "session-2025-11-19-001",
    planId: "015",
    status: "Active",
    createdAt: new Date().toISOString(),
    updatedAt: new Date().toISOString()
  }
};

const responseJson = await vscode.commands.executeCommand<string>(
  'Flowbaby.ingestForAgent',
  JSON.stringify(payload)
);

const response = JSON.parse(responseJson);

if (response.success) {
  console.log(`✅ Ingested ${response.ingested_chars} characters`);
} else {
  console.error(`❌ Error: ${response.error} (${response.errorCode})`);
}
```

## Agent Retrieval API

The `Flowbaby.retrieveForAgent` command allows agents to query the knowledge graph:

```typescript
const query = {
  query: "How did we implement authentication?",
  maxResults: 5
};

const responseJson = await vscode.commands.executeCommand<string>(
  'Flowbaby.retrieveForAgent',
  JSON.stringify(query)
);

const response = JSON.parse(responseJson);

if (response.success) {
  console.log(`📚 Retrieved ${response.results.length} memories`);
  for (const memory of response.results) {
    console.log(`- ${memory.topic}: ${memory.context}`);
  }
}
```

## Language Model Tools

Flowbaby also exposes tools that appear in VS Code's "Configure Tools" dialog for use with GitHub Copilot.

### Store Memory Tool (`#flowbabyStoreSummary`)

Stores conversation summaries in Flowbaby knowledge graph.

**Parameters**:

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `topic` | string | Yes | Short 3-7 word title for this memory |
| `context` | string | Yes | 300-1500 character summary describing the work |
| `decisions` | string[] | No | List of durable decisions made (0-5 items) |
| `rationale` | string[] | No | List of reasons for decisions (0-5 items) |
| `metadata` | object | No | Optional metadata (plan_id, status) |

### Retrieve Memory Tool (`#flowbabyRetrieveMemory`)

Searches Flowbaby knowledge graph for relevant memories.

**Parameters**:

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `query` | string | Yes | Natural language search query |
| `maxResults` | number | No | Max results to return (default: 3, max: 10) |

**Returns**: Both narrative markdown and structured JSON for agent parsing.

## Enabling Tools

Tools are controlled via VS Code's Configure Tools UI:

1. Open Copilot chat
2. Click "Tools" (⚙️ icon) → "Configure Tools"
3. Find "Store Memory in Flowbaby" and "Retrieve Flowbaby Memory"
4. Toggle tools on/off individually (disabled by default for privacy)

## Transparency

When agents use Flowbaby:

- **Output Channel**: All tool invocations logged in "Flowbaby Agent Activity"
- **Configure Tools UI**: Visual feedback for which tools are enabled/disabled
- **Chat Autocomplete**: `#flowbaby*` commands only appear when tools are enabled

## Further Documentation

- [AGENT_INTEGRATION.md](https://github.com/lsalsich/flowbaby/blob/main/extension/AGENT_INTEGRATION.md) — Complete API documentation with TypeScript examples
- [Bridge Contract](https://github.com/lsalsich/flowbaby/blob/main/extension/bridge/INGEST_CONTRACT.md) — JSON schema specification and error codes
- [Test Agent](https://github.com/lsalsich/flowbaby/tree/main/test-agent) — Reference implementation
