# Flowbaby Documentation

This is the documentation site for [Flowbaby](https://github.com/groupzer0/flowbaby), a VS Code extension that gives your AI coding agents long-term memory.

**Live site:** [https://docs.flowbaby.ai](https://docs.flowbaby.ai)

## Development

### Prerequisites

- Node.js 18+
- npm

### Local Development

```bash
# Install dependencies
npm install

# Start development server
npm run start
```

This starts a local development server at `http://localhost:3000`. Most changes are reflected live without having to restart the server.

### Build

```bash
npm run build
```

This generates static content into the `build` directory that can be served by any static hosting service.

## Deployment

This site is deployed to Vercel. Pushes to `main` trigger automatic deployments.

### Vercel Configuration

- **Root Directory:** `.` (repository root)
- **Framework Preset:** Docusaurus
- **Build Command:** `npm run build`
- **Output Directory:** `build`

## Documentation Structure

```text
docs/
├── intro.md           # Overview / landing page
├── getting-started.md # Installation & quickstart
├── configuration.md   # Settings, commands, MCP tools
├── workflows.md       # Usage patterns & tips
├── troubleshooting.md # Common issues & solutions
└── changelog.md       # Version history
```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## License

MIT
