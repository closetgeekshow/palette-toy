# Follow-up Improvements and QA Ideas

These suggestions focus on keeping the CDN-only, no-build demos lean while tightening quality and maintainability.

## Cross-demo consistency
- **Align token defaults**: Mirror the same required/optional token set across every demo (VanJS, Mithril, HTM/Preact, lit-html, Open Props, Shoelace, Radix Colors, doodling lab) so prompt wording and variable fallbacks stay identical.
- **Shared accessibility checklist**: Create a short ARIA/color-contrast checklist and keep it in `index.html` comments so every variant inherits the same guardrails.
- **Font import audits**: Add a small script block in `index.html` that logs deduped Google Font imports and warns if any demo omits the required body stack.

## Menu and metrics hygiene
- **Auto size table**: Generate the menu line-count table at load time by reading `data-lines` attributes on the links; add a lint check that fails if a file is missing or the numbers drift.
- **Link health check**: Include a tiny link-verifier snippet in `menu.html` to highlight missing demo files or typos without a build step.

## Interaction polish
- **Skeleton “fidget” improvements**: Add keyboard toggles for the tab, switches, and radio controls in `index.html` to keep the tactile feel accessible.
- **Visibility guardrails**: Extend the contrast checker from the doodling lab into the core demo so tokens that would hide objects on surfaces get flagged inline.

## Documentation & onboarding
- **Mini runbook**: Document how to add a new CDN-only variant (file naming, menu update, line-count entry, font imports). Place it near the top of `index.html` as a comment block.
- **Prompt regression notes**: Keep a short changelog of prompt schema changes inside `STYLE_REDUCTION_NOTES.md` so future tweaks stay deliberate.

## Optional monitoring (still build-free)
- **Perf sanity check**: Add a lightweight `performance.mark()` + `console.table` in `index.html` to spot expensive layout shifts across variants without introducing tooling.
