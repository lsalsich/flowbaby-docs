---
sidebar_position: 2
---

# Getting Started

This guide will help you install and configure Flowbaby for your VS Code workspace.

## Installation

### Method 1: Install from VS Code Marketplace (Recommended)

1. Open VS Code
2. Go to the Extensions view (`Ctrl+Shift+X` / `Cmd+Shift+X`)
3. Search for **"Flowbaby"**
4. Click **Install**
5. Reload VS Code when prompted

### Method 2: Install from VSIX

1. Download the latest `.vsix` file from [GitHub Releases](https://github.com/lsalsich/flowbaby/releases)
2. Open VS Code
3. Press `Ctrl+Shift+P` (or `Cmd+Shift+P` on macOS)
4. Type **"Install from VSIX"** and select the command
5. Navigate to the downloaded `.vsix` file and select it
6. Reload VS Code when prompted

## Setup

After installation, configure your workspace:

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

**Global API Key (Stored Securely)**

Use the built-in command to set your API key once, securely stored via VS Code's SecretStorage:

1. Open Command Palette (`Ctrl+Shift+P` / `Cmd+Shift+P`)
2. Run **"Flowbaby: Set API Key"**
3. Enter your API key when prompted

This stores the key securely and applies to all workspaces automatically.

### 3. Verify Extension Activation

1. Check the status bar for **"Flowbaby"** (checkmark)
2. If you see **"Flowbaby: Setup Required"** (yellow warning), click it to run setup
3. Optional: Open the Output panel (**View → Output**) and select **"Flowbaby"** to see logs
## Setup

After installation, configure your workspace:

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

**Global API Key (Stored Securely)**

Use the built-in command to set your API key once, securely stored via VS Code's SecretStorage:

1. Open Command Palette (`Ctrl+Shift+P` / `Cmd+Shift+P`)
2. Run **"Flowbaby: Set API Key"**
3. Enter your API key when prompted

This stores the key securely and applies to all workspaces automatically.

### 3. Verify Extension Activation

1. Check the status bar for **"Flowbaby"** (checkmark)
2. If you see **"Flowbaby: Setup Required"** (yellow warning), click it to run setup
3. Optional: Open the Output panel (**View → Output**) and select **"Flowbaby"** to see logs
