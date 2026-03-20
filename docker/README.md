# forgejo-mcp

A Dockge-compatible stack that builds and runs [`forgejo-mcp`](https://codeberg.org/goern/forgejo-mcp) — an MCP (Model Context Protocol) server providing AI assistants with direct access to your self-hosted Forgejo instance.

## What It Does

Exposes Forgejo operations as MCP tools consumable by any MCP-compatible AI client (Claude Desktop, Cursor, Continue, etc.):

- **Repos** — list, create, fork, search
&- **Files** — get, create, update, delete
- **Branches** — list, create, delete, list commits
- **Issues** — get, list, create, comment
- **Pull Requests** — get, list, create
- **Orgs/Teams** — search users and teams

## Prerequisites

- The `cti-net` Docker network must exist (`docker network create cti-net`)
- A Forgejo Personal Access Token with `repo`, `issue`, and `user` scopes
- Docker Buildx (for multi-stage build)

## Setup

1. Copy `.env.example` to `.env` and fill in your values:
   ```bash
   cp .env.example .env
   ```

2. In Dockge, create a new stack pointing to this directory, or deploy manually:
   ```bash
   docker compose up -d --build
   ```

3. The SSE endpoint will be available at:
   ```
   http://<your-host>:8089/sse
   ```

## MCP Client Configuration

Add to your MCP client config (e.g. Claude Desktop `claude_desktop_config.json`):

```json
{
  "mcpServers": {
    "forgejo": {
      "url": "http://<your-homelab-ip>:8089/sse"
    }
  }
}
```

## Notes

- The image is built locally from source since no official Docker image is published upstream
- Rebuild after upstream updates: `docker compose up -d --build --force-recreate`
- Runs on `cti-net` alongside your other CTI stack services for internal cross-stack access
