# Forgejo-MCP: GitHub Mirroring & Integration

## Overview
This module provides the definitive integration between internal Forgejo research repositories and external GitHub organizations within the ThreatLabs CTI ecosystem.

## Key Features
- **GitHub Mirroring**: Real-time mirroring of `jamz/forgejo-mcp` to GitHub.
- **MCP Provider**: Acts as a Model Context Protocol server for Flowise and other CTI sub-agents.
- **Enterprise Sync**: Integrated with the `/enterprise-sync` workflow for seamless secret management.

## Integration State
- **Mirror Target**: https://github.com/jamz/forgejo-mcp
- **Secrets**: Managed via Infisical (`GITHUB_MIRROR_TOKEN`).

## Deployment
Deployed as a Docker service within the `forgejo-mcp` stack, connected to the `cti-net` shared network.

---
*Verified: 2026-03-21*
