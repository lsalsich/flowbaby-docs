---
sidebar_position: 6
---

# Changelog

Track version history and release notes for Flowbaby.

For the most up-to-date changelog, see the [CHANGELOG.md](https://github.com/lsalsich/flowbaby/blob/main/extension/CHANGELOG.md) in the source repository.

## Recent Highlights

### v0.3.14

- **Environment Management**: Added status bar health indicators and refresh dependencies command
- **Background Safety**: Refresh operations automatically pause background tasks

### v0.3.3

- **Async Ingestion**: Memory capture now operates asynchronously (5-10 second response, 60-90 second background processing)
- **Staged Messaging**: Clear feedback about memory processing status
- **Completion Notifications**: Info/warning notifications when background processing finishes

### v0.2.1

- **Workspace-Local Storage**: All data now stored in `.flowbaby/system/` and `.flowbaby/data/`
- **API Key Migration**: `OPENAI_API_KEY` deprecated in favor of `LLM_API_KEY`
- **Isolated Environment**: `.flowbaby/venv` prevents conflicts with project virtual environments

### v0.2.0

- **Chat Participant**: `@flowbaby-memory` for explicit context retrieval
- **Keyboard Capture**: Ctrl+Alt+C / Cmd+Alt+C for quick memory capture
- **Hybrid Search**: Graph-vector search combining relationship traversal with semantic similarity

## Links

- [Full Changelog](https://github.com/lsalsich/flowbaby/blob/main/extension/CHANGELOG.md)
- [GitHub Releases](https://github.com/lsalsich/flowbaby/releases)
- [Contributing Guide](https://github.com/lsalsich/flowbaby/blob/main/CONTRIBUTING.md)
