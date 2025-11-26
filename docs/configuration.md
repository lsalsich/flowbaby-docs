---
sidebar_position: 3
---

# Configuration

Flowbaby is designed to work out of the box, but you can customize its behavior through VS Code settings.

## Settings

Access Flowbaby settings through:

- **UI**: File → Preferences → Settings → Extensions → Flowbaby
- **JSON**: Add to your `settings.json`

### Available Settings

| Setting | Type | Default | Description |
|---------|------|---------|-------------|
| `flowbaby.enabled` | boolean | `true` | Enable/disable the Flowbaby extension |
| `flowbaby.storageLocation` | string | `.flowbaby` | Folder name for the knowledge graph |
| `flowbaby.maxMemories` | number | `1000` | Maximum number of memories to store |
| `flowbaby.autoStore` | boolean | `true` | Automatically store memories during agent sessions |

### Example Configuration

```json
{
  "flowbaby.enabled": true,
  "flowbaby.storageLocation": ".flowbaby",
  "flowbaby.maxMemories": 1000,
  "flowbaby.autoStore": true
}
```

## Commands

Flowbaby provides the following VS Code commands:

| Command | Description |
|---------|-------------|
| `Flowbaby: Open Documentation` | Opens the Flowbaby documentation site |
| `Flowbaby: View Knowledge Graph` | Opens a view of stored memories |
| `Flowbaby: Clear All Memories` | Removes all stored memories (use with caution) |
| `Flowbaby: Export Memories` | Exports memories to a JSON file |

Access commands via the Command Palette (`Ctrl+Shift+P` / `Cmd+Shift+P`).

## MCP Tools

Flowbaby exposes two MCP (Model Context Protocol) tools that AI agents can use:

### flowbaby_storeMemory

Stores a new memory in the knowledge graph.

**Parameters:**

| Parameter | Required | Type | Description |
|-----------|----------|------|-------------|
| `topic` | Yes | string | Short 3-7 word title for the memory |
| `context` | Yes | string | 300-1500 character summary of what was done |
| `decisions` | No | string[] | List of durable decisions made (0-5 items) |
| `rationale` | No | string[] | Explanation of why decisions were made (0-5 items) |
| `metadata` | No | object | Optional metadata (plan_id, status) |

**Example:**

```json
{
  "topic": "Redis caching implementation",
  "context": "Implemented Redis caching for API responses using ioredis. Set up cache-aside pattern with 5-minute TTL for user data endpoints. Added cache invalidation on user updates.",
  "decisions": [
    "Use ioredis over node-redis for better TypeScript support",
    "5-minute TTL balances freshness and performance"
  ],
  "rationale": [
    "ioredis has better cluster support for future scaling",
    "User data changes infrequently, 5 minutes is acceptable staleness"
  ]
}
```

### flowbaby_retrieveMemory

Retrieves relevant memories from the knowledge graph.

**Parameters:**

| Parameter | Required | Type | Description |
|-----------|----------|------|-------------|
| `query` | Yes | string | Natural language description of what to recall |
| `maxResults` | No | number | Maximum results to return (default: 3, max: 10) |

**Example:**

```json
{
  "query": "Previous decisions about caching strategy and Redis implementation",
  "maxResults": 3
}
```

**Returns:** Structured JSON with matching memories, including topic, context, decisions, rationale, and metadata.

## Storage

### Knowledge Graph Location

By default, Flowbaby stores the knowledge graph at:

```text
{workspace}/.flowbaby/knowledge-graph.db
```

### Git Tracking

You have two options for version control:

**Option 1: Ignore (Personal Memory)**

Add to `.gitignore`:

```gitignore
.flowbaby/
```

Each developer has their own memory. Good for personal preferences and local context.

**Option 2: Track (Shared Memory)**

Commit the `.flowbaby/` folder. The team shares a common knowledge base. Good for project decisions and architecture context.

### Backup

The knowledge graph is a SQLite database. You can back it up by copying the `.flowbaby/` folder.
