---
sidebar_position: 5
---

# Troubleshooting

Solutions to common issues with Flowbaby.

## Installation Issues

### Extension Not Appearing

**Symptom**: Flowbaby doesn't show up in the extensions list after installation.

**Solutions**:

1. Reload VS Code (`Ctrl+Shift+P` → "Reload Window")
2. Check that you're running VS Code 1.85.0 or later
3. Try uninstalling and reinstalling the extension

### MCP Tools Not Available

**Symptom**: AI agents don't seem to have access to Flowbaby's memory tools.

**Solutions**:

1. Ensure GitHub Copilot is in agent mode
2. Restart VS Code after installing Flowbaby
3. Check the Output panel (View → Output → Flowbaby) for errors

## Memory Issues

### Memories Not Being Stored

**Symptom**: The agent completes work but doesn't store memories.

**Possible causes**:

1. **Extension disabled**: Check `flowbaby.enabled` setting
2. **Auto-store disabled**: Check `flowbaby.autoStore` setting
3. **Workspace not open**: Flowbaby requires a workspace folder

**Solutions**:

1. Verify settings in VS Code preferences
2. Open a folder/workspace (not just a file)
3. Check the Output panel for errors

### Memories Not Being Retrieved

**Symptom**: The agent doesn't seem to recall past context.

**Possible causes**:

1. **No relevant memories**: The knowledge graph may be empty or not have matching content
2. **Query too vague**: The retrieval query isn't finding matches
3. **Database corrupted**: The knowledge graph file may be damaged

**Solutions**:

1. Ask the agent directly: "What do you remember about [topic]?"
2. Be more specific in your questions
3. Check if `.flowbaby/knowledge-graph.db` exists and has content
4. Try clearing and rebuilding the knowledge graph

### Knowledge Graph Too Large

**Symptom**: VS Code becomes slow or memories are being dropped.

**Solutions**:

1. Increase `flowbaby.maxMemories` if you have the resources
2. Export old memories and clear the graph
3. Consider using `Superseded` status for outdated memories

## Performance Issues

### Slow Response Times

**Symptom**: AI agents take longer to respond when Flowbaby is active.

**Possible causes**:

1. Large knowledge graph
2. Many memories being retrieved

**Solutions**:

1. Reduce `maxResults` in retrieval queries
2. Clean up old or irrelevant memories
3. Check system resources

### High Memory Usage

**Symptom**: VS Code uses more memory with Flowbaby active.

**Solutions**:

1. The knowledge graph is loaded into memory; this is expected
2. Clear old memories if the graph is very large
3. Restart VS Code periodically for long sessions

## Data Issues

### Corrupted Knowledge Graph

**Symptom**: Errors when reading or writing memories.

**Solutions**:

1. Back up the current `.flowbaby/` folder
2. Try the `Flowbaby: Clear All Memories` command
3. If that fails, delete `.flowbaby/` and restart

### Lost Memories

**Symptom**: Previously stored memories are gone.

**Possible causes**:

1. Working in a different workspace
2. Knowledge graph was cleared or deleted
3. Git checkout changed the `.flowbaby/` folder

**Solutions**:

1. Check you're in the correct workspace
2. Check Git history for `.flowbaby/` changes
3. Restore from backup if available

## Agent Integration Issues

### Agent Not Using Memory Tools

**Symptom**: The AI agent doesn't call `flowbaby_storeMemory` or `flowbaby_retrieveMemory`.

**Possible causes**:

1. MCP tools not registered
2. Agent mode not active
3. Extension not initialized

**Solutions**:

1. Restart VS Code
2. Ensure you're using GitHub Copilot in agent mode
3. Check Output panel for Flowbaby initialization messages

### Incorrect Memory Retrieval

**Symptom**: The agent retrieves unrelated memories.

**Solutions**:

1. Be more specific in your questions
2. The semantic search may match on tangential content
3. Consider clearing outdated or low-quality memories

## Getting Help

If you're still having issues:

1. **Check the logs**: View → Output → select "Flowbaby" from the dropdown
2. **GitHub Issues**: Report bugs at [github.com/lsalsich/flowbaby/issues](https://github.com/lsalsich/flowbaby/issues)
3. **GitHub Discussions**: Ask questions at [github.com/lsalsich/flowbaby/discussions](https://github.com/lsalsich/flowbaby/discussions)

When reporting issues, please include:

- VS Code version
- Flowbaby version
- Relevant logs from the Output panel
- Steps to reproduce the issue
