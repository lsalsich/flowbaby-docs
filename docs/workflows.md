---
sidebar_position: 4
---

# Workflows

Learn effective patterns for using Flowbaby to maximize your AI coding productivity.

## Core Principles

### 1. Let Agents Store Automatically

Flowbaby is designed to work automatically. AI agents will:

- Store memories after completing significant work
- Retrieve context before answering questions
- Update memories when decisions change

You don't need to explicitly ask the agent to "remember" things.

### 2. Be Specific in Your Questions

When you want the agent to recall past context, be specific:

✅ **Good**: "How did we implement the authentication middleware?"

❌ **Less effective**: "What did we do before?"

Specific questions help the agent construct better retrieval queries.

### 3. Reference Past Decisions

When making changes that relate to previous work, reference it:

> "We decided to use Redis for caching. Now I want to add cache invalidation."

This prompts the agent to retrieve relevant memories about the caching implementation.

## Common Workflows

### Starting a New Feature

When beginning new work:

1. Describe what you want to build
2. The agent will check for related past context
3. Existing patterns and decisions will inform the implementation

**Example:**

> "Add a new API endpoint for user preferences. Follow the same patterns we used for the user profile endpoint."

### Continuing Previous Work

When picking up where you left off:

1. Ask about the current state of the feature
2. The agent retrieves progress and decisions
3. Continue from where you stopped

**Example:**

> "What's the status of the checkout flow refactor we started last week?"

### Understanding Past Decisions

When you need to understand why something was built a certain way:

1. Ask about the specific component or decision
2. The agent retrieves the rationale and context
3. You get the full picture, not just the code

**Example:**

> "Why did we choose PostgreSQL over MongoDB for this project?"

### Refactoring with Context

When refactoring code:

1. Ask about the original implementation and its constraints
2. The agent retrieves decisions and trade-offs
3. Refactor with full awareness of why things are the way they are

**Example:**

> "I want to refactor the payment processing module. What constraints and decisions should I be aware of?"

### Onboarding to a Codebase

When joining an existing project:

1. Ask high-level questions about architecture
2. The agent retrieves stored project knowledge
3. Get up to speed faster than reading documentation

**Example:**

> "Give me an overview of how authentication works in this project."

## Memory Management

### When Memories Are Created

Agents automatically store memories when:

- Implementing a significant feature
- Making architecture decisions
- Completing a multi-step task
- Resolving complex bugs

### Memory Quality

Good memories include:

- **Clear topic**: 3-7 word title
- **Rich context**: 300-1500 characters of detail
- **Explicit decisions**: What was decided
- **Rationale**: Why it was decided that way

### Memory Lifecycle

Memories can have different statuses:

| Status | Meaning |
|--------|---------|
| `Active` | Current approach, still relevant |
| `Superseded` | Replaced by a newer decision |
| `DecisionRecord` | Stable, long-term decision |

Agents will mark old memories as `Superseded` when approaches change.

## Team Collaboration

### Shared Knowledge Graph

If your team commits the `.flowbaby/` folder:

- Everyone shares the same project memories
- New team members get context automatically
- Decisions are preserved as team knowledge

### Personal Knowledge Graph

If each developer ignores `.flowbaby/`:

- Memories reflect individual work patterns
- Personal preferences are remembered
- No conflicts on merge

### Hybrid Approach

Some teams use both:

- Track a `team-memory.json` export in Git
- Keep personal `.flowbaby/` ignored
- Periodically sync important team decisions

## Tips for Power Users

### Explicit Memory Requests

You can ask the agent to store something specific:

> "Remember that we're using the repository pattern for data access in this project."

### Querying Memory Directly

Ask the agent to show what it remembers:

> "What do you remember about our testing strategy?"

### Correcting Memories

If a memory is wrong or outdated:

> "That's no longer accurate. We switched from REST to GraphQL last month."

The agent will update the knowledge graph.

### Bulk Context Loading

When starting a session, prime the agent:

> "Retrieve any memories about the payment system, user authentication, and our API design patterns."

This pre-loads relevant context for the session.
