---
name: Provision agent access to SPOTIO's MCP server
description: Mint, read, rotate and revoke the SPOTIO-MCP-KEY that authenticates an AI agent to SPOTIO's first-party remote MCP server at https://app.spotio2.com/mcp.
api: openapi/spotio-mcp-api-openapi.yml
generated: '2026-08-13'
method: generated
source: openapi/_original/spotio-swagger.json + probe of https://app.spotio2.com/mcp on 2026-08-13
operations:
  - POST /api/Mcp/keys/generate
  - GET /api/Mcp/keys/current
  - PUT /api/Mcp/keys/regenerate
  - DELETE /api/Mcp/keys/current
---

# Provision agent access to SPOTIO's MCP server

SPOTIO runs a **remote** MCP server - an agent connects to a URL, with nothing to
install. This skill covers the credential lifecycle, which is the part SPOTIO exposes
through its REST API.

## The endpoint

```
https://app.spotio2.com/mcp
```

Verified 2026-08-13: a JSON-RPC `tools/list` POST returns

```
401 Unauthorized: Missing SPOTIO-MCP-KEY header or mcpkey query parameter
```

That error is the contract. Authenticate with either:

- header `SPOTIO-MCP-KEY: <key>`, or
- query parameter `?mcpkey=<key>`

Prefer the header. A key in a query string ends up in logs, proxies and browser history.

There is **no OAuth** - `/.well-known/oauth-authorization-server` and
`/.well-known/oauth-protected-resource` return 404 on every SPOTIO host. The MCP key is
a tenant-scoped API key, so treat it as a bearer secret with no scoping, no expiry
metadata and no consent screen.

## Lifecycle

Run **spotio-authenticate-and-read-workflow** first; all four operations require a
normal SPOTIO bearer token.

| Action | Call |
|---|---|
| Mint a key | `POST /api/Mcp/keys/generate` |
| Read the current key | `GET /api/Mcp/keys/current` |
| Rotate | `PUT /api/Mcp/keys/regenerate` |
| Revoke | `DELETE /api/Mcp/keys/current` |

The paths are singular - `keys/current`, not `keys/{id}` - so a tenant holds **one**
active MCP key at a time. Consequences you must design around:

- **Rotation is a cutover, not an overlap.** `PUT /api/Mcp/keys/regenerate` invalidates
  the previous key. Every agent using it breaks at the same instant. Sequence the
  rotation, or accept the gap.
- **You cannot issue per-agent keys.** Two agents sharing one tenant key are
  indistinguishable to SPOTIO. If you need attribution, put it in your own layer.
- **Revocation is total.** `DELETE /api/Mcp/keys/current` cuts off every agent at once -
  which is exactly what you want as an incident kill switch. Wire it to your break-glass
  runbook.

## Privilege inheritance

The bearer token used to mint the MCP key comes from an API key that inherits the role
and privileges of the SPOTIO user who created it. That privilege chain reaches the
agent. **Mint the MCP key from an account holding the least privilege the agent needs**,
not from a full Admin, because there is no scope parameter to narrow it afterwards.

## What the agent can do

Unknown from outside. `tools/list` is auth-gated, SPOTIO publishes no llms.txt and no MCP
tool reference page, so the tool names, descriptions and input schemas are not publicly
observable. Once you hold a key:

```bash
curl -X POST https://app.spotio2.com/mcp \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -H "SPOTIO-MCP-KEY: $SPOTIO_MCP_KEY" \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/list"}'
```

Reconcile what comes back against `mcp/spotio-tool-crosswalk.yml`, which enumerates all
295 REST operations across 39 capabilities as the binding target. Expect the MCP surface
to be a **subset** - it will not cover everything REST does - and record which
capabilities have no tool before assuming an agent can reach them.

## Do not confuse this with the Zapier MCP

`https://zapier.com/mcp/spotio2` is Zapier's MCP server wrapping SPOTIO actions. It is a
third-party surface with a different auth model, a different tool set and Zapier in the
data path. The server described above is SPOTIO's own.
