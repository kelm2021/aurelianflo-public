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

- `server_capabilities` (free): connection check, prices, how to pay, free test
  inputs, and sample responses
- `wallet_screen`: screen 1-100 wallets against OFAC lists, with address
  validation, a proceed-or-review decision, and signed provenance. Optional
  PDF/DOCX report and, for one EVM wallet, indirect exposure through
  counterparties
- `compliance_edd_report`: enhanced due diligence memo with wallet and
  subject-name screening
- `compliance_exposure_forecast`: OFAC exposure forecast with base rates and
  model limitations
- `compliance_queue_optimize`: review queue prioritization
- `screening_verify` (free): check that a stored result is authentic and
  unchanged
- `saved_results` (account): list, fetch, or delete results saved with
  `save: true`
- `wallet_watchlist` (account): watch wallets and get alerted when one is
  designated

Older tool names (`wallet_ofac_screen`, `wallet_ofac_report`,
`wallet_ofac_batch`, `report_pdf_generate`, `report_docx_generate`,
`queue_saved_list`, `report_saved_retrieve`) still work but are no longer
listed.

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

The direct endpoint is operated by AurelianFlo. No sign-in is required to
connect. Call `server_capabilities` to verify the connection for free; it also
lists current prices, the ways to pay, and sample responses.

## Trying and Paying

- **Free test inputs:** calls that use only the test addresses published in
  `server_capabilities` run free, with real results marked `mode: "test"`.
- **API key:** send `Authorization: Bearer afk_...` with each request. Keys are
  issued on request through support.
- **x402:** use an x402-capable client and wallet to authorize USDC payments on
  Base. Payment settles only when the tool succeeds.

Adding an MCP connection alone does not enable paid execution.

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
