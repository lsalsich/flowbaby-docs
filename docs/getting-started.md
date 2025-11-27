---
sidebar_position: 2
---

# Getting Started

This guide will help you install and configure Flowbaby for your VS Code workspace.

## Prerequisites

Before installing the extension, ensure you have:

- **VS Code** 1.85.0 or higher
- **Python** 3.8+ installed and available in PATH

:::note
Flowbaby now manages its own Python environment automatically. You no longer need to manually install `cognee` globally.
:::

## Installation

### Method 1: Install from VSIX (Recommended)

1. Download the latest `.vsix` file from [GitHub Releases](https://github.com/lsalsich/flowbaby/releases)
2. Open VS Code
3. Press `Ctrl+Shift+P` (or `Cmd+Shift+P` on macOS)
4. Type **"Install from VSIX"** and select the command
5. Navigate to the downloaded `.vsix` file and select it
6. Reload VS Code when prompted

### Method 2: Build from Source

See [CONTRIBUTING.md](https://github.com/lsalsich/flowbaby/blob/main/CONTRIBUTING.md) for developer setup instructions.

## Setup

### 1. Initialize Workspace (Automated)

Flowbaby now manages its own Python environment automatically.

1. Open the Command Palette (`Ctrl+Shift+P` / `Cmd+Shift+P`)
2. Run **"Flowbaby: Initialize Workspace"**
3. The extension will:
   - Check for Python 3.8+
   - Create a dedicated `.flowbaby/venv` in your workspace (isolated from project venvs)
   - Install `cognee` and dependencies
   - Verify the environment is ready

### 2. Configure API Key

**Recommended: Global API Key (Stored Securely)**

Use the built-in command to set your API key once, securely stored via VS Code's SecretStorage:

1. Open Command Palette (`Ctrl+Shift+P` / `Cmd+Shift+P`)
2. Run **"Flowbaby: Set API Key"**
3. Enter your API key when prompted

This stores the key securely and applies to all workspaces automatically.

**Alternative: Workspace-Specific `.env` File**

For per-workspace configuration, create a `.env` file in your workspace root:

```env
LLM_API_KEY=sk-your-key-here
```

**Priority Order**: Workspace `.env` file > SecretStorage (global) > System environment variable

### 3. Verify Extension Activation

1. Check the status bar for **"Flowbaby: Ready"** (green checkmark)
2. If you see **"Flowbaby: Setup Required"** (yellow warning), click it to run setup
3. Open the Output panel (**View → Output**) and select **"Flowbaby Memory"** to see logs

## First Memory

To test that everything is working:

### Keyboard Shortcut (Primary Method)

1. View a valuable chat message (from any participant: @workspace, @terminal, GitHub Copilot, etc.)
2. Press **Ctrl+Alt+C** (or **Cmd+Alt+C** on macOS)
3. Paste the message content in the input box (or leave empty to use clipboard)
4. Press Enter to capture
5. See "Memory staged – processing will finish in ~1–2 minutes" confirmation

### Command Palette (Alternative)

1. Open Command Palette (`Ctrl+Shift+P` / `Cmd+Shift+P`)
2. Type "Flowbaby: Capture to Memory"
3. Follow the same workflow as keyboard shortcut

## Test Retrieval

1. Open GitHub Copilot Chat (`Ctrl+Alt+I` or click chat icon)
2. Type: `@flowbaby-memory What did I capture earlier?`
3. The participant retrieves and displays your memory!

## What Gets Captured

- Chat conversations from ANY participant (@workspace, @terminal, GitHub Copilot, etc.)
- Manual notes and observations you type
- Code explanations and discussions
- Only content YOU choose to capture (selective, user-controlled)

## Next Steps

- Learn about [Configuration](./configuration) options
- Explore [Workflows](./workflows) for common use cases
- Check [Troubleshooting](./troubleshooting) if you run into issues
