# TODO

## Outstanding Requests

- [ ] Mirror the required/optional token sets across **all** demos.
  - [ ] Extract the definitive required/optional token list from `index.html`.
  - [ ] Apply the same list to every variant HTML file, ensuring fallbacks match.
  - [ ] Spot-check a few demos in the browser to confirm consistent behavior.

- [ ] Audit font imports across themes.
  - [ ] Enumerate `fonts.imports` segments in every demo and deduplicate.
  - [ ] Verify each demo sets `--font-body`, `--font-heading`, `--font-logo`, and `--font-code` with correct fallbacks.
  - [ ] Ensure the Google Fonts URL assembly logic stays centralized and consistent.

- [ ] Add keyboard accessibility for the skeleton “fidget” controls in `index.html`.
  - [ ] Wire keyboard toggles for tabs, switches, and radio controls.
  - [ ] Keep the interactive elements integrated into the dashboard layout (not bolted on separately).
  - [ ] Regression-test existing pointer interactions after keyboard support.

- [ ] Integrate interactive fidget elements into the dashboard sketch.
  - [ ] Identify dashboard panels to host the toggles, tabs, and radios.
  - [ ] Embed controls within existing blocks instead of appending a new section.
  - [ ] Align spacing/radius tokens so the tactile feel remains consistent.

- [ ] Create additional demos.
  - [ ] Hyperscript version (CDN-only, no build).
  - [ ] uhtml version.
  - [ ] hyperHTML version.
  - [ ] nanohtml version.
  - [ ] Open Props + Radix Colors hybrid with tokens serialized to DTCG JSON.
  - [ ] Slot-friendly, templating-helper demo without frameworks, based on the original layout.
  - [ ] Add each new page to `menu.html` with updated line-count stats per agent rules.

- [ ] Documentation updates.
  - [x] Write a document on how `@layer` and other modern CSS features can keep variables flexible, clear, and DRY.
  - [x] Add guidance prioritizing Open Props, layering Radix Colors, and emitting DTCG JSON for interoperability.
  - [x] Recommend modularizing the JSON editor, helper factories, prompt generator, instructions, base token defaults, and schema generation into a separate file with boilerplate for template updates, copying/pasting, and a template prompt generator.
  - [x] Create a short (≤100 words) document proposing any additional rules to add to `AGENTS.md`.
- [x] Update existing docs to trim completed items, leaving only their names with a ✅ marker.
  - ✅ CSS_LAYERING_GUIDE.md
  - ✅ TOKEN_STACKING_STRATEGY.md
  - ✅ MODULARIZATION_PLAN.md
  - ✅ AGENTS_RULES_PROPOSAL.md

- [ ] Menu hygiene.
  - [ ] After adding demos or docs, refresh `menu.html` to include links and stats for every page.
  - [ ] Recalculate baseline comparisons against `index.html`.
