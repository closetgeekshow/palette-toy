# Structuring the Palette Toy templating system

## Goals
- Keep every HTML demo build-free and CDN-only.
- Let LLMs and humans swap UI renderers without touching the shared token manifest.
- Reduce duplication of repeated panels or controls while keeping the markup legible.

## Slot-friendly layout ideas
- **Named slots on reusable shells**: wrap the shared chrome (header, token controls, preview grid) in a template literal with named slots like `slot:header`, `slot:controls`, `slot:preview`. Each framework variant can drop in its own DOM for those slots while inheriting the same styles and data attributes.
- **Data-role anchoring**: mark slot anchors with `data-slot="header"` and hydrate them with `innerHTML` snippets. This keeps the DOM shallow and predictable for LLMs.
- **Lightweight partials**: store small HTML strings (e.g., `window.partials = { card, badge, controlRow }`) that every variant reuses. Because they are plain strings, they require no build tooling and are easy to tweak globally.
- **Token-aware fragments**: keep fragments free of inline colors and radii; everything should rely on CSS variables. Slots should reference `data-token` hints so generators can reason about intent.

## How slots reduce redundancy
- **Shared scaffolding**: the chrome (global styles, CSS variables, prompt helper) only lives once; variants swap slot content instead of forking whole documents.
- **Composable previews**: previews become arrays of fragments (cards, stat tiles, toggles). Add/remove fragments without rewriting the container grid.
- **Safer refactors**: slot names and `data-role` markers give LLMs a stable map to edit without misplacing framework-specific syntax.

## Example slot map
- `slot:header` → logo/title + pill controls
- `slot:controls` → token pickers, doodle pad, preset buttons
- `slot:preview` → card grid demonstrating surfaces, text, and radius application
- `slot:prompt` → THEME IDEAS scaffold and visibility rules

## Templating helpers to keep
- **String-based micro-templates**: small tagged template helpers (e.g., `html` from lit-html or htm) keep the markup terse without a build step.
- **Slot renderers**: `renderSlot(name, targetId, templateFn)` applies a fragment string to any target; the function stays framework-agnostic.
- **Schema metadata**: keep the token manifest and prompt text in `<script type="application/json">` so slots can read shared rules.

By treating the layout as a handful of named slots and keeping fragments token-driven, the demos stay DRY and the markup remains approachable for both humans and LLMs.
