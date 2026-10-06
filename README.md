<p align="center"><img src="logo.png" width="120" alt="MiningBridge"></p>

# MiningBridge Intelligence MCP server

Critical-mineral and rare-earth trade intelligence for your AI assistant. You can ask about lithium, cobalt, nickel, rare earths (NdPr), graphite inputs, gallium and germanium, and battery scrap. It answers with trade flows, commodity snapshots, supply-concentration risk (including China exposure), counterparty screening, sourcing briefs, research reports and a sourced evidence base.

- **Endpoint:** `https://intel.miningbridge.in/api/mcp`
- **Transport:** Streamable HTTP (MCP 2025-06-18). This is a hosted server, so there's nothing to install or run.
- **Sign-in:** OAuth 2.1 ("Sign in with MiningBridge"), discovered automatically. A free account works. You can also use an API key as a Bearer token.
- **Tools:** 9, all read-only, each with an output schema
- **Official MCP Registry:** `in.miningbridge/intel`, and listed on [Smithery](https://smithery.ai/servers/miningbridge/intel)
- **Setup guide:** https://intel.miningbridge.in/connect

> Figures are screening magnitudes derived from UN Comtrade and public disclosures. They are not price targets, valuations or investment advice.

This repository holds documentation and client configuration only. The server itself is hosted by MiningBridge Private Limited.

## Tools

| Tool | What it answers |
|---|---|
| `list_commodities` | Which critical-mineral commodities are tracked (primary and secondary/scrap), with HS codes |
| `search_trade_flows` | US monthly import/export values for a commodity |
| `get_commodity_snapshot` | Imports, exports, net position and lead partner for one commodity |
| `assess_supply_risk` | Concentration risk (Herfindahl-Hirschman index) with a China-exposure read |
| `screen_suppliers` | Screens the counterparty directory by country or keyword |
| `generate_market_report` | Full sourcing brief: trade position, risk, corridors, feedstock alternatives |
| `list_reports` | Research reports on critical minerals and rare earths |
| `read_report` | Reads a published report, or its opening section and contents |
| `search_evidence` | Searches individual sourced claims on production, processing and trade measures |

The free plan gives a daily allowance and summary answers. Pro unlocks full series, numeric risk scores, named counterparties and sourcing briefs.

## Connect

Every client below uses the same address. Clients that support MCP sign-in open a MiningBridge login the first time you connect. For clients that don't support it, create a key at https://intel.miningbridge.in/account/keys and send it as the header `Authorization: Bearer <your key>`.

**Claude (web, desktop, mobile):** Settings → Connectors → Add custom connector → paste `https://intel.miningbridge.in/api/mcp`.

**ChatGPT:** Settings → Apps & Connectors → Advanced → Developer mode → Create, then paste the same URL and choose OAuth.

**Claude Code**
```bash
claude mcp add --transport http miningbridge https://intel.miningbridge.in/api/mcp
```

**Cursor:** `~/.cursor/mcp.json`
```json
{ "mcpServers": { "miningbridge": { "url": "https://intel.miningbridge.in/api/mcp" } } }
```

**VS Code / VS Code Insiders:** `.vscode/mcp.json`
```json
{ "servers": { "miningbridge": { "type": "http", "url": "https://intel.miningbridge.in/api/mcp" } } }
```

**Gemini CLI**
```bash
gemini extensions install https://github.com/miningbridge/intel-mcp
```
Or add this to `~/.gemini/settings.json`: `{ "mcpServers": { "miningbridge": { "httpUrl": "https://intel.miningbridge.in/api/mcp" } } }`

**Windsurf:** `~/.codeium/windsurf/mcp_config.json`
```json
{ "mcpServers": { "miningbridge": { "serverUrl": "https://intel.miningbridge.in/api/mcp" } } }
```

**Cline / Roo Code:** MCP Servers → Remote Servers → name `miningbridge`, URL `https://intel.miningbridge.in/api/mcp`, type Streamable HTTP.

**Codex:** `~/.codex/config.toml`
```toml
[mcp_servers.miningbridge]
url = "https://intel.miningbridge.in/api/mcp"
```

**goose:** Extensions → Add custom extension → type Streamable HTTP → URL `https://intel.miningbridge.in/api/mcp`.

**Any other MCP client** (LM Studio, Zed, Kiro, OpenCode, Cherry Studio, LibreChat, Raycast and others): add a remote / Streamable HTTP server with the URL above. If the client can't do the browser sign-in, add the Bearer-key header.

## Example prompts

- "Using MiningBridge, what is the US trade position in lithium carbonate, and who is the lead partner?"
- "Assess supply concentration risk for cobalt hydroxide, including China exposure."
- "Screen MiningBridge counterparties for rare-earth refiners in Australia."
- "List MiningBridge research reports on nickel and summarise the free brief."

## Support

- Website: https://intel.miningbridge.in
- Email: support@miningbridge.in
- Privacy: https://intel.miningbridge.in/privacy

© MiningBridge Private Limited. The documentation in this repository is released under the MIT licence. The MiningBridge service and data are subject to the website terms.
