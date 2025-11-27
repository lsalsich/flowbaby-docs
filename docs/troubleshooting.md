---
sidebar_position: 5
---

# Troubleshooting

Common issues and solutions for Flowbaby.

## Extension Not Activating

### Check the Output Channel

1. Go to **View → Output**
2. Select **"Flowbaby Memory"** from the dropdown
3. Look for initialization errors

### Enable Debug Logging

If you need more detailed information:

1. Enable `Flowbaby.debugLogging` in settings
2. Use **"Flowbaby: Show Debug Logs"** command

## Common Issues

### "LLM_API_KEY not found"

**Solution**: Use the **"Flowbaby: Set API Key"** command (recommended), or create a `.env` file in your workspace root with:

```env
LLM_API_KEY=sk-your-key-here
```

Then reload VS Code: `Ctrl+Shift+P` → **"Reload Window"**

:::note
As of v0.2.1, `OPENAI_API_KEY` is no longer supported. Use `LLM_API_KEY` to align with Cognee 0.4.0.
:::

### "Python not found" or "cognee module not found"

**Solution**: 

- Run **"Flowbaby: Initialize Workspace"** to set up the environment automatically
- If using a custom Python environment, set `Flowbaby.pythonPath` to your Python path

### "No workspace folder open"

**Solution**: The extension requires a workspace (not single-file mode). Open a folder:

- **File → Open Folder**
- Or use the command: `code /path/to/your/project`

### Slow Performance

**Solutions**:

- Check that `Flowbaby.logLevel` is not set to `"debug"` (this slows down operations)
- Reduce `maxContextResults` to 1-2 for faster retrieval
- Reduce `maxContextTokens` to 1000 for lighter processing

### Python Jedi Language Server Conflict

**Symptom**: Flowbaby stops working after using Python IntelliSense; the `.venv` or Python environment gets overwritten with different packages.

**Cause**: The Python Jedi language server (Pylance) may modify or replace packages in the active virtual environment.

**Solution**: Flowbaby now uses an isolated environment at `.flowbaby/venv` (instead of `.venv`) to prevent conflicts:

1. Run **"Flowbaby: Initialize Workspace"** to create the isolated environment
2. If prompted about an existing `.venv`, choose "Use Flowbaby's .flowbaby/venv (Recommended)"

### Capture or Retrieval Not Working

#### Capture Issues

1. Verify keyboard shortcut (Ctrl+Alt+C / Cmd+Alt+C) is not conflicting with other extensions
2. Check Command Palette for "Flowbaby: Capture to Memory" as alternative
3. Ensure you see confirmation message after capture ("✅ Captured to memory")
4. Check Output Channel logs for ingestion errors

#### Retrieval Issues

1. Verify `Flowbaby.enabled` is `true` in settings
2. Type `@flowbaby-memory` in chat to invoke the participant explicitly
3. Check Output Channel logs for retrieval attempts and timing
4. Remember: The first conversation in a new workspace has no context (memory starts empty)
5. Each workspace has separate memory—switching workspaces means different context
6. If retrieval fails, you'll see "⚠️ Memory retrieval unavailable" but participant continues without context

## Common Error Patterns

| Symptom | Likely Cause | Recommended Action |
|---------|--------------|-------------------|
| "Python script exited with code 1" (empty stderr) | Interpreter mismatch: `cognee` or `python-dotenv` not installed | Set `Flowbaby.pythonPath` to correct interpreter |
| "No module named 'cognee'" | Missing `cognee` package | Install with: `pip install cognee==0.3.4` |
| "LLM_API_KEY not found" | Missing API key in `.env` or environment | Create `.env` file with valid `LLM_API_KEY` |
| Script timeout (retrieval: 15s, ingestion: 120s) | Network issues, slow LLM provider | Check Output Channel for timing metrics |
| JSON parse error in logs | Script produced non-JSON output | Report as bug |

:::note
Auto-detection works for standard `.venv` setups on Linux, macOS, and Windows. For remote contexts (Remote-SSH, WSL, Dev Containers), conda, or pyenv, use explicit `Flowbaby.pythonPath` configuration.
:::

## Clearing Memory

To reset your workspace memory (e.g., to start fresh or clear sensitive data):

```bash
rm -rf .flowbaby/
```

The extension will reinitialize on next activation, creating a fresh knowledge graph.

## Known Limitations

- **Workspace Required** — Extension doesn't work in single-file mode
- **Python Dependency** — Python and Cognee must be installed separately (not bundled)
- **Manual Capture** — Keyboard shortcut requires copy-paste workflow; cannot extract message from chat UI directly (VS Code API limitation)
- **Explicit Participant Invocation** — Must type `@flowbaby-memory` to trigger retrieval; cannot inject context into other participants
- **First Conversation** — The first conversation in a new workspace has no context (memory starts empty)
- **Step 6 Auto-Ingestion Disabled by Default** — Automatic capture of @flowbaby-memory conversations is experimental
- **Platform Support** — Primarily tested on macOS and Linux; Windows support may require additional configuration

## Known Issues

### Cognee 0.4.0 File Hashing Bug (Auto-Ingestion)

**Issue**: Cognee v0.4.0 has an intermittent file hashing bug that causes ingestion to fail unpredictably when the same conversation is ingested multiple times.

**Symptoms**:

- Conversations fail to ingest with hash mismatch errors
- Intermittent failures (some ingests succeed, others fail for identical content)
- Errors logged in Output Channel: "File not found" or hash-related issues

**Workaround**:

- **Default**: `Flowbaby.autoIngestConversations` is set to `false` (auto-ingestion disabled)
- **Manual Capture**: Use keyboard shortcut (Ctrl+Alt+C) to capture conversations manually—this does NOT trigger the bug
- **Experimental Testing**: Set `Flowbaby.autoIngestConversations` to `true` to test feedback loop (may experience intermittent failures)
- **Graceful Degradation**: Ingestion failures are logged but do NOT crash the extension

**Status**: Monitoring Cognee updates for bug fix; will enable auto-ingestion by default when resolved.

## Getting Help

- **Report Bugs**: [GitHub Issues](https://github.com/lsalsich/flowbaby/issues)
- **Feature Requests**: [GitHub Discussions](https://github.com/lsalsich/flowbaby/discussions)
- **Cognee Documentation**: [docs.cognee.ai](https://docs.cognee.ai)
