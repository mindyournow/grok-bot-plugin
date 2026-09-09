# Mind Your Now for Grok Bot

Connect your Mind Your Now account to manage tasks, review priorities, and work
through your daily debrief from Grok Bot.

**Status:** Version 0.1.0 is a local submission candidate. It is not published
or listed in Grok Bot. Package validation and public OAuth discovery checks
have passed; installation and authenticated use inside Grok Bot remain untested.

## What it includes

- An MCP connection to `https://api.mindyournow.com/mcp` with browser-based OAuth.
- A workflow skill for MYN priorities, task capture, completion, and daily debriefs.
- MYN's existing logo and metadata for the plugin listing.

The package contains configuration and instructions, with no executable hooks,
local server, runtime dependencies, or bundled credentials. Your MCP client
handles sign-in and token storage; MYN handles account access and tool execution.

The server determines which tools are available. Its full configuration includes
tasks, debriefs, timers, memories, goals, and comments. A reduced configuration
can expose fewer tools. This package does not provide complete feature parity
with the separate Hermes and OpenClaw plugins: it adds no calendar-event,
grocery-list, YNAB, or agent-pairing adapters.

## Connect after catalog approval

These steps apply once the plugin is accepted and visible in Grok Bot:

1. Open **Plugins** in Grok Bot (or **Settings → Plugins**, depending on the app version).
2. Search for **Mind Your Now** and add it.
3. Choose **Authorize** or **Authenticate**, then sign in to MYN in your browser.
4. Confirm the connection appears under **Installed**. If authorization is
   waiting, use **Reopen** to return to the browser flow.
5. Attach the connector with `@` if needed, and ask: **“What are my Critical Now tasks?”**

An MYN account is required. A team administrator may need to enable the plugin.
Do not paste credentials into a conversation.

Try these requests:

- “Show me today's tasks, with Critical Now first.”
- “Add a task to call the dentist tomorrow, under Opportunity Now.”
- “Walk me through my daily debrief. Suggest changes before applying them.”

## Packaging and release

This is a single Cursor-format plugin: `.cursor-plugin/plugin.json` declares
`mcp.json`, the logo, and the skill directory. Grok Bot's official help describes
its account connections and Cursor team plugin controls. Cursor documents this
package format and its marketplace submission process. Catalog acceptance and
availability in Grok Bot still require confirmation during submission; a valid
Cursor package alone does not prove that Grok Bot will list it.

See [release instructions](docs/release.md) for the submission route and remaining
validation, and [verification](docs/verification.md) for completed checks.

## Troubleshooting

- **Not in the catalog:** This candidate needs publication and catalog approval.
- **Disabled by team admin:** Ask the team administrator to enable the plugin.
- **Authorization required:** Reopen the provider sign-in from the plugin connection.
- **HTTP 403 before sign-in:** MYN's edge protection can reject some client
  signatures. Capture the failing URL, time, and Cloudflare Ray ID for support.
  Do not put tokens in a report.
- **A tool is missing:** Use the tools actually returned by MYN. This package
  does not expand the backend's enabled tool set.
- **No widget appears:** Ask for a text summary of the tool's response.

Support: [support@mindyournow.com](mailto:support@mindyournow.com).

## Sources

- [Grok Bot: connect plugins](https://cursor.com/help/grok-bot/connect-plugins)
- [Grok Bot: use the computer and apps](https://docs.x.ai/grok-bot/computer-and-apps)
- [Cursor plugin format and submission](https://cursor.com/docs/reference/plugins)

## License

[MIT](LICENSE).
