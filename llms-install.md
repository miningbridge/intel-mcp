# Installing MiningBridge Intelligence (for AI agents)

This is a **hosted remote MCP server**. You don't need to clone, build or run anything locally.

1. Add a remote MCP server named `miningbridge`:
   - URL: `https://intel.miningbridge.in/api/mcp`
   - Transport: Streamable HTTP (`streamableHttp` / `http`)
2. Authentication, in order of preference:
   - **OAuth (preferred):** connect without credentials. The server answers `401` with a `WWW-Authenticate` header that points to `/.well-known/oauth-protected-resource`. Follow standard MCP authorization (dynamic client registration, PKCE S256). The user signs in at intel.miningbridge.in and clicks **Allow**.
   - **API key (fallback):** if the client can't do OAuth, ask the user to create a key at https://intel.miningbridge.in/account/keys (it starts with `mb_live_`), then set the header `Authorization: Bearer <key>`. Never invent or guess a key.
3. Verify by calling `list_commodities`. It should return the tracked commodities, for example "MiningBridge tracks 15 traded commodities...".

Example Cline settings entry (`cline_mcp_settings.json`):

```json
{
  "mcpServers": {
    "miningbridge": {
      "type": "streamableHttp",
      "url": "https://intel.miningbridge.in/api/mcp",
      "disabled": false
    }
  }
}
```

With an API key instead of OAuth, add:

```json
"headers": { "Authorization": "Bearer mb_live_..." }
```

All tools are read-only. No environment variables, local dependencies or system permissions are required.
