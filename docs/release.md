# Release and catalog submission

## Listing copy

**Name:** Mind Your Now

**Summary:** Manage tasks and daily planning in Mind Your Now. Connect your
account to review priorities, capture tasks, and work through your daily debrief.

**Category:** Productivity

**Homepage:** https://mindyournow.com

**Source repository:** https://github.com/mindyournow/grok-bot-plugin

**Support:** support@mindyournow.com

**Authentication:** Browser-based OAuth with each user's MYN account.

**MCP endpoint:** https://api.mindyournow.com/mcp

**Logo:** `assets/logo-square.png` (512x512, white plate)

## Submission

1. Use the public source repository at
   https://github.com/mindyournow/grok-bot-plugin. It includes the manifest,
   MCP configuration, skill, logo, README, and license.
2. Submit that repository URL through xAI's
   [Submit a Plugin form](https://x.ai/bot/marketplace/submit-a-plugin) and
   choose **Grok Bot** as the listing destination. The form takes the
   repository URL, a 1:1 logo URL (`assets/logo-square.png`), a description,
   and testing instructions, and asks you to confirm the plugin was tested
   locally and in-app.
3. Before you submit, add `https://api.mindyournow.com/mcp` in Grok Bot as a
   custom connector (**Connect apps → Add a custom connector → Remote HTTPS**)
   and run the in-app checks below, so the form's tested-in-app confirmation
   is true.
4. Complete the authenticated checks below using the actual Grok Bot client.
5. After acceptance, record the catalog listing URL, tested Grok Bot version,
   and release commit. Replace the candidate status in the README.

Do not submit this package to the Grok Build marketplace as a substitute. Its
`.grok-plugin` index belongs to a different product. Likewise, Cursor IDE local
plugin discovery is not evidence of installation inside Grok Bot.

## Authenticated release checks

Use a dedicated MYN test account and a catalog-provided preview or installed
plugin. No live task changes were performed while preparing this candidate.

1. Install through Grok Bot. Confirm the name, logo, skill, and MCP connection
   are discovered, and capture the tested app version.
2. Complete browser authentication. Verify the callback finishes, the connection
   becomes installed, and a read returns only the signed-in test account's data.
3. Reconnect with a second test account. Confirm that it cannot read or alter
   the first account's private tasks, including by supplying a first-account ID.
4. Ask for Critical Now tasks. Confirm the returned IDs and priorities match
   the MYN test account and that the request causes no task changes.
5. Explicitly request creation of one task titled “Grok Bot integration check,”
   with Opportunity Now priority. Read it back by its returned ID, then explicitly
   request completion and verify its completed state. Keep it as test evidence.
6. Request a daily debrief review. Confirm that results are readable as text,
   and suggested changes remain unapplied until requested.
7. Verify token refresh and reconnect behavior using the platform's supported
   test path. Disconnect/revoke the test connection and confirm later access
   requires authorization. Do not edit token stores manually.
8. Check missing-tool and authentication failures: the skill must explain the
   limitation without claiming a successful action or asking for credentials in chat.

Record results without account content, tokens, cookies, or authorization codes.
The public endpoint probes are useful prerequisites, not substitutes for these checks.
