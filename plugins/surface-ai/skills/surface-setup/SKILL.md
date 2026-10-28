---
name: surface-setup
description: Connect Claude Code to Surface AI, or fix the connection. Use when the user is getting started with the Surface AI plugin, when the surface MCP server's tools are missing, or when /mcp shows the surface server failed (for example a 401 or "Missing or invalid management key").
---

# Connecting to Surface AI

The plugin connects to Surface's MCP server with a **management key** that the user enters when
they enable the plugin. Claude Code stores it securely; never ask the user to paste the key into
the chat, and never write it to a file.

## Check the connection

If the `surface` tools are available, call `surface_list`. Any result — even an empty list — means
the connection works. Tell the user how many surfaces they have and suggest setting one up on a
page of this codebase.

## The tools are missing, or `/mcp` shows `surface` failed

The key is missing, mistyped or revoked. Claude Code doesn't load the tools until the key works, so
walk the user through:

1. **Get a key.** Open https://app.surface-ai.io/settings/developers and, under
   **Management API keys**, create one. It starts with `mak_live_` and is shown once — copy it then.
2. **Enter it.** Run `/plugin`, choose **surface-ai**, and configure it with the new key.
3. **Restart Claude Code** so the server reconnects with the new key.
4. Run `/mcp` to confirm `surface` is connected, then check the connection as above.

A key belongs to a user, not an organization: revoking one person's key leaves everyone else
connected. If the user revoked a key under Settings → Developers, that key stops working right away.

## Without the plugin

Anyone can connect without the plugin, with the key in the `SURFACE_MANAGEMENT_KEY` environment
variable. Keep the single quotes: they store the variable rather than the key itself.

```bash
claude mcp add --scope user --transport http surface https://mcp.surface-ai.io/mcp/ \
  --header 'Authorization: Bearer ${SURFACE_MANAGEMENT_KEY}'
```
