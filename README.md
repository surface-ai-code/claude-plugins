# Surface AI for Claude Code

Set up and manage [Surface AI](https://surface-ai.io) from Claude Code. Surface serves a
different version of chosen page content to each visitor and learns which one gets more visitors
to the page's goal. This plugin lets Claude add a surface to a page of your codebase, write the
variants, and manage them afterwards.

## Install

1. Create a management key at [app.surface-ai.io/account](https://app.surface-ai.io/account),
   under **Management API keys**. It starts with `mak_live_` and is shown once.
2. In Claude Code:

   ```
   /plugin marketplace add surface-ai-code/claude-plugins
   /plugin install surface-ai@surface-ai
   ```

3. Paste the key when Claude Code asks for it. It's stored in your system keychain, not in a file.
4. Restart Claude Code, then run `/mcp` to check that `surface` is connected.

## Use

Ask Claude in your project, for example:

- "Set up Surface on the pricing page."
- "List my surfaces."
- "Add two new headline variants to the homepage surface."
- "Open the homepage surface in the dashboard."

| Included | |
|---|---|
| MCP server | `surface`, at `https://mcp.surface-ai.io/mcp/` |
| Skill `surfaces` | Sets up a surface on a page and manages variants |
| Skill `surface-setup` | Connects Claude Code and fixes a missing or invalid key |

## Changing or replacing the key

Run `/plugin`, choose **surface-ai**, configure it with the new key, and restart Claude Code.
Revoke the old key on the account page.

## Without the plugin

```bash
claude mcp add --transport http surface https://mcp.surface-ai.io/mcp/ \
  --header "Authorization: Bearer $SURFACE_MANAGEMENT_KEY"
```

## License

MIT
