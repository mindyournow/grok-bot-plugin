# Candidate verification

Checked on 2026-09-09 UTC. These results cover the local package and public
authentication endpoints, not an installed Grok Bot connection.

| Check | Result |
| --- | --- |
| Cursor template validator | Passed: manifest, component paths, logo, and skill frontmatter |
| Skill frontmatter validator | Passed |
| MCP configuration | Valid JSON; one HTTPS remote endpoint; no credentials or executable server |
| OAuth authorization metadata | HTTP 200; authorization, token, registration, and refresh support advertised; S256 PKCE advertised |
| Protected-resource metadata at `/.well-known/oauth-protected-resource/mcp` | HTTP 200; identifies MYN's authorization server |
| Unauthenticated `GET /mcp` | HTTP 401 with a `WWW-Authenticate` resource-metadata URL |
| Unauthenticated MCP `initialize` request | HTTP 401 with the same discovery challenge; JSON body reports `unauthorized` |
| Grok Bot catalog installation | Not tested; no listing or preview access yet |
| Browser login, authenticated tool use, token refresh, account isolation, and revocation in Grok Bot | Not tested |

The Cursor check used the unmodified
[official template validator](https://github.com/cursor/plugin-template/blob/main/scripts/validate-template.mjs),
downloaded on 2026-09-09. The validator expects a marketplace, so the single
plugin was referenced from a temporary one-entry marketplace outside this
repository. That wrapper was only a validation fixture; this package remains
a single plugin. The only warning was the absence of optional hooks, which
this package does not use. The validator checks structure, not catalog approval.

The MCP initialization probe used protocol version `2025-06-18`, JSON-RPC
method `initialize`, and no credentials. It did not invoke any account tools
or register an OAuth client. Protocol negotiation after authentication has
not been tested.

## Edge protection observation

Requests made with Python's default urllib client received Cloudflare error
1010 (`browser_signature_banned`). Curl requests to the same public endpoints
succeeded or returned the expected HTTP 401 authentication challenge. This
distinguishes an edge client-signature rejection from a missing OAuth endpoint.
Grok Bot's actual network path remains unverified; record any edge rejection
during the authenticated release check. No edge rules were changed.

## Release boundary

The package is prepared in Cursor's documented plugin format for submission
targeting Grok Bot. Its source is published at
https://github.com/mindyournow/grok-bot-plugin. It has not been submitted to or
accepted into a catalog, or certified as compatible with Grok Bot. Follow
[release instructions](release.md) before claiming user installation is available.
