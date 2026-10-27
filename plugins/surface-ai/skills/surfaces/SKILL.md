---
name: surfaces
description: Set up a Surface AI surface on a page of this codebase, or manage existing surfaces and their variants. Use when the user wants to A/B test or personalize page copy (headlines, calls to action, hero images) with Surface, or asks about their surfaces, variants, results or the Surface dashboard.
---

# Surface AI

Surface serves a different version of chosen page content to each visitor and learns which version
gets more visitors to the page's goal. The `surface` MCP server's tools do the work; this skill is
how to use them well.

If no `surface` tools are available, the server isn't connected — follow the `surface-setup` skill
first.

## Setting up a new surface

When the user wants Surface on a page of this codebase, follow
[setup-workflow.md](setup-workflow.md) step by step. It is the same workflow as the server's
`setup_surface` prompt. Don't skip its **Ask** checkpoints: nothing is created until the user has
approved the elements, goals and variants.

## How Surface is organized

- **Surface:** one page placement, identified by `surface_id` — the only id the tools take. It has
  a `page_url`, an `edge_url` (where its bundle is served) and a `dashboard_url`.
- **Variants:** the versions of content a surface serves. Each one sets a value for the surface's
  fields.
- **Control:** one variant per segment is the control — the page's current copy, which the others
  are measured against. Change it with `variant_set_control`; never fake it by editing contents.
- **Goals:** the clicks or form submits that count as success. The first goal is the one the
  surface optimizes.
- **Live state:** `surface_get` returns `live_state`. `LIVE` means the snippet is on the deployed
  page and reporting; anything else means visitors aren't being served yet.

## Variant lifecycle

| Status | Served? | Editable? |
|---|---|---|
| `DRAFT` | No | Yes — `variant_update` |
| `ACTIVE` | Yes | No — create a new variant instead |
| `PAUSED` | No | No |
| `ARCHIVED` | No | No |

Variants added with `variant_create` start as drafts. Show the user the drafts, then activate the
approved ones with `variant_set_status`. Pause a variant rather than archiving it if the user may
want it back.

## Working with the user

- **"Open it" / "show me the results":** call `surface_get` and open its `dashboard_url`. Results,
  analytics and A/B tests live in the dashboard.
- **Writing variants:** start from the control's copy, change one idea per variant, and keep each
  value close to the original's length so the layout holds.
- **Deletes** aren't available through the tools. Archive instead, or point the user to the
  dashboard.
- **Errors:** relay a tool's error message as it is — it explains the rule that was hit. A plan
  limit error includes a link to the account page; share it.
