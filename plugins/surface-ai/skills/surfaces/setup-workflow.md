Set up a Surface on a page of this codebase: Surface serves a different version of chosen content
to each visitor and learns which one gets more visitors to the page's goal.

Work through these steps in order. Ask the user at each checkpoint marked **Ask** and wait for the
answer — nothing is created until step 5.

1. **Find the page.** Ask the user which page, if they haven't said. Get its live URL (the deployed page, not localhost). Find the
   source file(s) that render it and identify the framework (Next.js, Astro, Rails, plain HTML…).

2. **Propose what to test.** Read the page and propose:
   - 2–4 content elements worth varying: the headline, the subheadline, the primary call-to-action
     label, a hero image. Skip elements that wrap other markup — swapping their text would wipe it.
   - 1–2 goals: the primary call-to-action click, a signup or lead form submit.

   **Ask** the user which elements and goals to use.

3. **Draft the variants.** The control is the page's current copy, taken from the source. Write 2–3
   challengers that change one idea each (outcome-led headline, urgency, social proof…), keeping
   each value close to the original's length.

   **Ask** the user to approve or edit the variants.

4. **Mark the elements.** Add `data-surface-field="<key>"` to each chosen element and
   `data-surface-goal="<goal key>"` to each goal element. Keys are lowercase with underscores, e.g.
   `headline`, `cta_label`. Change no copy and no other markup.

   An element that is both — a call-to-action whose label you vary and whose click is the goal —
   gets only `data-surface-field`. Its goal reuses that field's selector, so one click is one
   event rather than two.

5. **Create the surface.** Call `surface_setup` with the page URL, the fields (selector
   `[data-surface-field="<key>"]`), the goals (selector `[data-surface-goal="<goal key>"]`, or the
   field's exact selector for an element that is both; `dom_event` `submit` for a form, otherwise
   `click`; the primary goal first) and the variants (`is_control: true` on the current copy, which
   must set every field).

6. **Install the snippet.** Follow the returned `install_guide` exactly — it is the source of truth.
   In short: this one page only, never site-wide; in `<head>`; keep `defer`; the anti-flicker style
   must be in the server-sent HTML, before the script; add the script's origin to the site's CSP if
   it has one.

7. **Review and preview.** Show the user the full diff. Then start the dev server and give them one
   link per variant — the page's local URL plus `?surface_variant=<id>`, with each id from the
   `variants` that `surface_setup` returned, the control first. Opening each shows that variant
   swapped in within a second. Local traffic is served but never recorded, so previewing is safe.
   Without the parameter, a browser session keeps whichever variant it was first served.

8. **Go live.** Visitors see variants once the user deploys. After they do, call `surface_get` and
   confirm `live_state` is `LIVE`; share the `dashboard_url`, where results appear.
