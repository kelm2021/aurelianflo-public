# AurelianFlo Public Metadata

AurelianFlo is a compliance-focused x402 and MCP service for agent workflows.

This repository is the public discovery and support surface for the AurelianFlo
remote MCP server. It intentionally contains metadata, support details, privacy
terms, and integration links only. The production application source is kept in a
private repository.

## Public Production URLs

- UI: `https://aurelianflo.com`
- API origin: `https://api.aurelianflo.com`
- MCP endpoint (sign in with email): `https://api.aurelianflo.com/mcp/account`
- MCP endpoint (no sign-in; API key or x402): `https://api.aurelianflo.com/mcp`
- Server card: `https://api.aurelianflo.com/.well-known/mcp/server-card.json`
- Signing keys for result verification: `https://api.aurelianflo.com/.well-known/aurelianflo-signing-keys.json`
- Setup guide: `https://aurelianflo.com/server-card`
- Documentation: `https://api.aurelianflo.com/mcp/docs`
- Privacy: `https://api.aurelianflo.com/mcp/privacy`
- Support: `https://api.aurelianflo.com/mcp/support`
- Data handling: `https://api.aurelianflo.com/mcp/security`
- Third parties that receive data: `https://api.aurelianflo.com/mcp/subprocessors`
- Service status: `https://api.aurelianflo.com/mcp/status`

## MCP Tools

The server lists 22 tools. Reading and changing are separate tools.

- `server_capabilities` (read-only): Free first-call capability and connection check for AurelianFlo; use it first to see the tools, your daily limits (or prices without an account), free test inputs, sample responses, and how to sign in
- `wallet_screen` (read-only): Screen 1-100 crypto wallet addresses against OFAC sanctions lists (SDN by default)
- `compliance_edd_report` (read-only): Build an enhanced due diligence memo for a subject and its wallets: exact-match OFAC wallet screening, subject-name screening against sanctioned parties, sanctions evidence, and follow-up actions, returned as structured JSON or an inline PDF/DOCX artifact
- `compliance_exposure_report` (read-only): Report each wallet's exposure to sanctioned addresses from evidence: whether it is listed now, and whether its own on-chain transfers in the lookback period were sent to or received from listed addresses
- `compliance_queue_optimize` (read-only): Order a backlog of wallets for manual review
- `screening_verify` (read-only): Free check that a stored AurelianFlo screening, batch or EDD result is authentic and unchanged
- `saved_results` (account, read-only): List the results saved in your account (screening, EDD memo, exposure report or queue), or fetch one by its screening_id
- `saved_results_delete` (account, write, destructive): Permanently delete one saved result from your account by its ID
- `wallet_watchlist` (account, read-only): Show your watchlist: the wallet addresses being watched, any that have since been listed, and the alert settings
- `wallet_watchlist_add` (account, write): Start watching wallet addresses, so you are alerted (signed webhook and/or email) when one is added to a sanctions list
- `wallet_watchlist_remove` (account, write, destructive): Stop watching wallet addresses
- `wallet_watchlist_alerts` (account, write, destructive): Change how watchlist alerts reach you: set or clear the alert webhook, and turn email alerts on or off
- `saved_results_save` (account, write): Keep a result you just produced in your account, by its screening_id, so you can list it, reopen it and verify it later
- `sanctions_party_screen` (read-only): Screen 1-100 person, company or vessel names against the OFAC SDN, UK, EU and UN sanctions lists, without needing a wallet
- `wallet_payee_check` (read-only): Pre-payment check for one wallet address: a short yes/no for an agent or payment flow that is about to send funds
- `sanctions_list_changes` (read-only): List the crypto addresses added to or removed from the OFAC SDN list since a date, with each party's name, programs and asset, and the two list versions compared (publication date, hash, address count)
- `wallet_watchlist_events` (account, read-only): Show the log of what your watchlist did, newest first: each check (when, against which list version, how many addresses), each alert raised (address and listed party), and each delivery attempt (webhook delivered, retry scheduled, dropped, email sent, email failed)
- `wallet_watchlist_test_alert` (account, write): Send one signed test event (type watchlist.test) to your alert webhook and, if email alerts are on, a test email, and report whether each was delivered
- `account_api_keys` (account, read-only): List the API keys on your account: each key's first 12 characters and when it was created (a key issued before keys were listed shows no date, and appears after its first use)
- `account_api_key_create` (account, write): Create an API key for your account
- `account_api_key_revoke` (account, write, destructive): Revoke one of your API keys by its first 12 characters (key_prefix), as listed by account_api_keys, or every key on the account at once (all: true)
- `saved_results_export` (account, read-only): Export results you saved as one JSON bundle for a case file or an audit

Older tool names (`wallet_ofac_screen`, `wallet_ofac_report`, `wallet_ofac_batch`,
`report_pdf_generate`, `report_docx_generate`, `queue_saved_list`,
`report_saved_retrieve`, `compliance_exposure_forecast`) still work but are no
longer listed. Nothing in the server forecasts or predicts.

A result with no match means no exact match was found on the lists checked. It
is not a clearance.

## Install

Claude Custom Connector:

1. Open Claude settings.
2. Go to **Customize** > **Connectors**.
3. Add a custom connector named `AurelianFlo`.
4. Use this MCP server URL:

```text
https://api.aurelianflo.com/mcp/account
```

5. Sign in with your email and enter the 6-digit code you are sent. Signing in
   creates a free account. Every tool is free on an account, within daily
   limits.

Claude Desktop does not use `claude_desktop_config.json` for remote MCP
servers.

Direct Codex MCP install:

```bash
codex mcp add aurelianflo --url https://api.aurelianflo.com/mcp
```

Both endpoints are operated by AurelianFlo. The direct endpoint
(`https://api.aurelianflo.com/mcp`) needs no sign-in to connect. Call
`server_capabilities` to verify the connection for free; it also lists your
daily limits (or prices without an account) and sample responses.

## Free Use and Paying per Call

- **Sign in:** connect to `https://api.aurelianflo.com/mcp/account` and sign in
  with your email. Every tool is then free. Each account has daily limits that
  reset at 00:00 UTC: 100 screened addresses, 10 due diligence memos, 20 wallets read for exposure, 10 review queue runs, 10 PDF or Word files, 100 screened names and 500 payee checks. An account can watch up to
  25 addresses. A failed run does not count.
- **Free test inputs:** calls that use only the test addresses published in
  `server_capabilities` run free for anyone, with real results marked
  `mode: "test"`.
- **Free trial without an account:** a few single-address screenings a day.
- **API key:** created from a signed-in session with `account_api_key_create`,
  then sent as `Authorization: Bearer afk_...`. Calls are free within the same
  daily limits.
- **x402:** for agents with no account. Use an x402-capable client and wallet
  to pay per call in USDC on Base. Payment settles only when the tool succeeds.

Without an account, adding an MCP connection alone does not enable the priced
tools.

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
