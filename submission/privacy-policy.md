# AurelianFlo Privacy Policy

This privacy policy applies to the AurelianFlo remote MCP server and its paid
HTTP endpoints.

## Data Collected

- Tool input payloads required to execute compliance screening, enhanced due
  diligence memos, exposure reports, review queues, and document generation
- Account data, if you sign in: your email address, an account ID, and your
  usage and charges against your free allowance or credits. API keys and
  sign-in tokens are stored only as one-way hashes
- Saved results, only when you ask for them (`save: true` or an account
  setting): the result data, its provenance, and any generated document
- Watchlists, if you create one: the watched wallet addresses, their labels,
  and your webhook URL and its signing secret
- Operational logs required for uptime, debugging, abuse prevention, and billing
  reconciliation, plus daily usage counts (sign-ups, active accounts, accounts
  at their limit)
- Payment metadata required by x402 settlement flows

## Data Minimization

- We collect only the data required to execute the requested tool call and
  support the service
- Results are not kept unless you save them
- We do not intentionally collect unrelated conversation history beyond the MCP
  payload sent to the server

## Use of Data

- To execute the requested MCP tool call
- To return structured tool results and document artifacts
- To sign you in, track your allowance, and send sign-in codes and watchlist
  alerts
- To monitor uptime, prevent abuse, and investigate failures
- To reconcile paid usage and settlement events

## Data Sharing

- Data may be processed by infrastructure and payment providers necessary to
  execute the service
- Sign-in codes and alert emails are sent through our email provider (Resend)
- For indirect exposure checks, the screened wallet address and its
  counterparties are looked up through a blockchain indexer (Blockscout for
  EVM chains, TronGrid for TRON, Blockstream for Bitcoin)
- Watchlist alerts are sent to the webhook URL and email address you configure
- Data is not sold for advertising purposes

## Retention and Deletion

- Saved results are kept for 365 days by default (configurable per account from
  1 day to 7 years) and can be deleted at any time with the `saved_results_delete` tool
- A generated PDF or DOCX is held for 15 minutes behind a private, unguessable
  download link and then deleted. Anyone with the link can download the file
  during that time
- Sign-in codes expire after 10 minutes, access tokens after 1 hour, and refresh
  tokens after 30 days
- To delete your account, email address, saved results, and watchlist, contact
  `support@aurelianflo.com`
- Operational logs and request records are retained only as long as needed for
  reliability, billing, fraud prevention, and compliance

## Contact

- Support email: `support@aurelianflo.com`
- Documentation: `https://api.aurelianflo.com/mcp/docs`
