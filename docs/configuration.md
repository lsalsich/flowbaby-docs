---
sidebar_position: 3
---

# Configuration

Customize Flowbaby's behavior through VS Code settings.

## Settings

Access settings via **File → Preferences → Settings → Extensions → Flowbaby Memory**:

| Setting | Description | Default |
|---------|-------------|---------|
| `Flowbaby.enabled` | Toggle memory capture and retrieval on/off | `true` |
| `Flowbaby.maxContextResults` | Maximum number of memory results to retrieve | `3` |
| `Flowbaby.maxContextTokens` | Token budget for retrieved context | `2000` |
| `Flowbaby.recencyWeight` | Weight for prioritizing recent conversations (0-1) | `0.3` |
| `Flowbaby.importanceWeight` | Weight for prioritizing marked conversations (0-1) | `0.2` |
| `Flowbaby.autoIngestConversations` | **Experimental**: Auto-capture @flowbaby-memory conversations | `false` |
| `Flowbaby.pythonPath` | Path to Python interpreter (must have Cognee installed) | `python3` |
| `Flowbaby.logLevel` | Logging verbosity: error, warn, info, debug | `info` |
| `Flowbaby.debugLogging` | Show debug output channel (for troubleshooting) | `false` |

## LLM Configuration

Configure your LLM provider via **File → Preferences → Settings → Extensions → Flowbaby Memory**:

| Setting | Description | Default |
|---------|-------------|---------|
| `Flowbaby.llm.provider` | LLM provider (openai, anthropic, ollama, etc.) | `openai` |
| `Flowbaby.llm.model` | Model name (e.g., gpt-4o-mini, claude-3-opus) | `gpt-4o-mini` |
| `Flowbaby.llm.endpoint` | Custom API endpoint (for self-hosted models) | *(empty)* |

### Provider Examples

- **OpenAI (default)**: Leave provider as `openai`, model as `gpt-4o-mini`
- **Anthropic Claude**: Set provider to `anthropic`, model to `claude-3-opus-20240229`
- **Local Ollama**: Set provider to `ollama`, model to your model name, endpoint to `http://localhost:11434`

## Python Environment

The extension requires Python 3.8+ with the following packages:

- `cognee` (version 0.3.4 or compatible)
- `python-dotenv`

### Automatic Detection

The extension automatically detects your Python interpreter in this order:

1. **Explicit Setting**: `Flowbaby.pythonPath` if configured (highest priority)
2. **Flowbaby Environment**: `.flowbaby/venv/bin/python` (isolated from project venvs)
3. **Legacy Location**: `.venv/bin/python` (Linux/macOS) or `.venv/Scripts/python.exe` (Windows)
4. **System Python**: `python3` as fallback

:::tip Why `.flowbaby/venv`?
This location prevents conflicts with project virtual environments (e.g., Python Jedi language server overwriting Flowbaby's dependencies). The `.flowbaby/` directory is also automatically added to `.gitignore`.
:::

### When to Configure Manually

Set `Flowbaby.pythonPath` explicitly if:

- Virtual environment is outside workspace directory
- Using conda or pyenv environments (not auto-detected)
- Want to share a Python environment across multiple workspaces

Example configuration in VS Code settings:

```json
{
  "Flowbaby.pythonPath": "/path/to/your/.flowbaby/venv/bin/python"
}
```

Platform-specific examples:

- Linux/macOS: `/home/user/project/.flowbaby/venv/bin/python`
- Windows: `C:\Users\user\project\.flowbaby\venv\Scripts\python.exe`

## Environment Management

Flowbaby includes tools to keep your environment healthy:

- **Status Bar**: Shows real-time health (Ready, Setup Required, Refreshing, Error)
- **Refresh Dependencies**: If you encounter issues, run **"Flowbaby: Refresh Bridge Dependencies"** to safely reinstall the environment without losing data
- **Background Safety**: Refresh operations automatically pause background tasks to prevent conflicts

## Memory Management Commands

| Command | Description |
|---------|-------------|
| **Flowbaby: Toggle Memory** | Flips `Flowbaby.enabled` setting on/off |
| **Flowbaby: Clear Workspace Memory** | Deletes all captured conversations for current workspace (requires confirmation) |
| **Flowbaby: Initialize Workspace** | Set up or repair the Flowbaby environment |
| **Flowbaby: Set API Key** | Store API key securely via VS Code SecretStorage |
| **Flowbaby: View Background Operations** | Check status of in-flight memory operations |

## Unsupported Contexts

The following contexts are **not validated or supported** in this release:

- **Remote Development**: VS Code Remote-SSH, WSL, Dev Containers
- **Multi-root Workspaces**: Workspaces with multiple folder roots
- **Conda Environments**: Automatic detection not implemented (use explicit config)
- **Pyenv Environments**: Automatic detection not implemented (use explicit config)

Support for these contexts may be added in future releases.
