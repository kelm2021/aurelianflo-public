# AurelianFlo Public Metadata

AurelianFlo is a compliance-focused x402 and MCP service for agent workflows.

This repository is the public discovery and support surface for the AurelianFlo
remote MCP server. It intentionally contains metadata, support details, privacy
terms, and integration links only. The production application source is kept in a
private repository.

## Public Production URLs

- UI: `https://aurelianflo.com`
- API origin: `https://api.aurelianflo.com`
- MCP endpoint: `https://api.aurelianflo.com/mcp`
- Server card: `https://api.aurelianflo.com/.well-known/mcp/server-card.json`
- Documentation: `https://api.aurelianflo.com/mcp/docs`
- Privacy: `https://api.aurelianflo.com/mcp/privacy`
- Support: `https://api.aurelianflo.com/mcp/support`

## MCP Tools

- `server_capabilities`
- `queue_saved_list`
- `report_saved_retrieve`
- `wallet_ofac_report`
- `wallet_ofac_screen`
- `wallet_ofac_batch`
- `compliance_edd_report`
- `compliance_exposure_forecast`
- `compliance_queue_optimize`
- `report_pdf_generate`
- `report_docx_generate`

## Install

Claude Custom Connector:

1. Open Claude settings.
2. Go to **Customize** > **Connectors**.
3. Add a custom connector named `AurelianFlo`.
4. Use this MCP server URL:

```text
https://api.aurelianflo.com/mcp
```

Claude Desktop does not use `claude_desktop_config.json` for remote MCP
servers.

Direct Codex MCP install:

```bash
codex mcp add aurelianflo --url https://api.aurelianflo.com/mcp
```

Smithery listing:

```bash
smithery mcp add aurelianflo/core
```

AgentCash discovery:

```bash
npx agentcash discover https://api.aurelianflo.com
```

## Registry Metadata

The official MCP registry metadata is in
[`submission/server.json`](./submission/server.json).

## Support

Use GitHub issues in this repository for public support requests that do not
contain confidential information. For private or security-sensitive reports, use
`support@aurelianflo.com`.
