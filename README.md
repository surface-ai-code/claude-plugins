# Surface AI for Claude Code

[![Release](https://img.shields.io/github/v/release/surface-ai-code/claude-plugins)](https://github.com/surface-ai-code/claude-plugins/releases)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue)](LICENSE)
[![Docs](https://img.shields.io/badge/docs-docs.surface--ai.io-1d4fd7)](https://docs.surface-ai.io/mcp/plugin?utm_source=github&utm_medium=readme)

Set up and manage [Surface AI](https://www.surface-ai.io/?utm_source=github&utm_medium=readme) from Claude Code. Surface serves a
different version of chosen page content to each visitor and learns which one gets more visitors
to the page's goal. This plugin lets Claude add a surface to a page of your codebase, write the
variants, and manage them afterwards.

**Docs:** [docs.surface-ai.io/mcp](https://docs.surface-ai.io/mcp) — install, the tools, and
troubleshooting.

## Install

1. Create a management key at [app.surface-ai.io/settings/developers](https://app.surface-ai.io/settings/developers):
   click **Create key**. It starts with `mak_live_` and is shown once.
2. In Claude Code:

   ```
   /plugin marketplace add surface-ai-code/claude-plugins
   /plugin install surface-ai@surface-ai
   ```

3. Paste the key when Claude Code asks for it. It's stored in your system keychain, not in a file.
4. Run `/mcp` to check that `surface` is connected.

Something not working? See [Troubleshooting](https://docs.surface-ai.io/mcp/troubleshooting).

## Use

Ask Claude in your project, for example:

- "Set up Surface on the pricing page."
- "List my surfaces."
- "How is the homepage test doing?"
- "Add two new headline variants to the homepage surface."
- "Open the homepage surface in the dashboard."

| Included | |
|---|---|
| MCP server | `surface`, at `https://mcp.surface-ai.io/mcp/` |
| Skill `surfaces` | Tests and personalizes page content: adds a surface to a page, manages variants, reads results |
| Skill `connect` | Connects Claude Code and fixes a missing or invalid key |

## Changing or replacing the key

Run `/plugin`, choose **surface-ai**, and configure it with the new key.
Revoke the old key under Settings → Developers.

## Without the plugin

With your key in `SURFACE_MANAGEMENT_KEY`. The single quotes store the variable, not the key, in
Claude Code's config:

```bash
claude mcp add --scope user --transport http surface https://mcp.surface-ai.io/mcp/ \
  --header 'Authorization: Bearer ${SURFACE_MANAGEMENT_KEY}'
```

## Links

- [surface-ai.io](https://www.surface-ai.io/?utm_source=github&utm_medium=readme): what Surface is
- [docs.surface-ai.io/mcp](https://docs.surface-ai.io/mcp?utm_source=github&utm_medium=readme): the MCP server, its tools, and troubleshooting
- [Create a free account](https://app.surface-ai.io/register?next=/settings/developers&utm_source=github&utm_medium=readme)
- [Report a bug](https://github.com/surface-ai-code/claude-plugins/issues/new/choose) · [Security](SECURITY.md)

## License

MIT
