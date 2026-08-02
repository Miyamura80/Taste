---
name: usage
description: How to use the CLI, API, and MCP interfaces. Use this skill when interacting with the tool as an end user.
---
# Usage Guide

This skill teaches you how to use the three interfaces provided by this project.

## CLI

```bash
# Install
pip install taste

# Basic usage
taste --help                  # see all commands
taste greet Alice             # run a command
taste config show             # view configuration
taste doctor                  # check system health

# Global flags (go before the subcommand)
taste --verbose greet Alice   # detailed output
taste --format json config show  # JSON output
taste --dry-run greet Bob     # preview without executing
taste --version               # print version
```

## Server (HTTP API + MCP)

```bash
# Start the server: HTTP API and MCP (streamable HTTP) on one port.
taste-serve

# Default http://localhost:8080. See /docs for OpenAPI, /mcp for MCP.
```

## MCP

The MCP server exposes the same services as CLI tools via the Model Context Protocol.

**Primary transport: streamable HTTP at `/mcp`** (started by `taste-serve`).
Stdio is supported via `taste-mcp` for local Claude Desktop / dev only.

```bash
# Legacy stdio transport
taste-mcp

# Debug with the MCP inspector (stdio)
mcp dev mcp_server/server.py
```

### Connecting MCP to your editor

Remote (preferred - works on Claude Desktop 0.7+, Cursor, etc.):

```json
{
  "mcpServers": {
    "taste": {
      "url": "https://YOUR-DEPLOYMENT/mcp",
      "headers": { "X-API-KEY": "sk_..." }
    }
  }
}
```

Local stdio (legacy):

```json
{
  "mcpServers": {
    "taste": {
      "command": "taste-mcp"
    }
  }
}
```

## Updating

```bash
taste update    # check for updates and upgrade
```
