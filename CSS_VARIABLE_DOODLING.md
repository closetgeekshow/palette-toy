# Designing a CSS-Variables-First "Doodling" System for LLM-Friendly Theming

## Goals
- **Flexible**: Encourage freeform exploration of tokens (colors, radii, typography) without locking users into strict schemas.
- **Easy to write**: Plain HTML/JS with CSS variables front-and-center; no build tooling or JSX required.
- **LLM-friendly**: Clear naming, inline comments, and predictable structures that models can infer, extend, and refactor safely.

## Core Principles
1. **Single source of truth in CSS variables**: Define every adjustable value as a `--token` on `:root` or scoped containers. Avoid magic numbers in markup/JS.
2. **Semantic token naming**: Use readable patterns like `--surface-base`, `--accent-strong`, `--radius-sharp`, `--font-body`. Prefer `-xs/-s/-m/-l` scales over ad-hoc values.
3. **Composable layers**: Group tokens by concern (surfaces, text, accents, radii, shadows, spacing, motion) with light comments so LLMs can identify related families.
4. **Explicit fallbacks**: Provide fallbacks for fonts and colors (e.g., `var(--font-body, system-ui)`) so partial themes still render and stay legible.
5. **Inline previews**: Pair each token with a mini preview swatch or control (slider for radii, color input for accents). Keep previews small and colocated with token declarations in the DOM.
6. **Schema hints in data attributes**: Use `data-token="surface.base"` or `data-role="radius/sharp"` to help LLMs map DOM nodes to token meanings.
7. **Textual prompt scaffolds**: Keep a short, updatable prompt template in the page that explains required vs optional tokens, font fallback rules, and accessibility constraints. LLMs can rewrite or extend it.
8. **No build step, CDN-only**: Load helpers (color pickers, drag-to-tweak controls) via CDN. Keep everything runnable from `index*.html` for quick iterations.

## Suggested Structure
```html
<style>
  :root {
    /* surfaces */
    --surface-base: #0d1117;
    --surface-raised: #161b22;
    /* accent & contrast */
    --accent-primary: #7c3aed;
    --text-primary: #f8fafc;
    --text-muted: #cbd5e1;
    /* radii */
    --radius-sharp: 2px;
    --radius-soft: 12px;
    /* fonts */
    --font-body: system-ui, sans-serif;
    --font-heading: var(--font-body);
    --font-logo: var(--font-heading);
    --font-code: ui-monospace, SFMono-Regular, Menlo, monospace;
  }
</style>
<div class="token-row" data-token="accent.primary">
  <label>Accent Primary</label>
  <input type="color" value="#7c3aed" data-bind="--accent-primary" />
  <span class="swatch" style="background: var(--accent-primary)"></span>
</div>
```
- Keep **one visual and one textual hint** per token row so LLMs see intent and humans can tweak quickly.

## Interaction Ideas
- **Drag-to-doodle radii**: A slider bound to `--radius-sharp` and `--radius-soft` updates corners live; use small preview boxes to show sharp vs. pill.
- **Visibility guardrails**: Compute contrast for text vs. surfaces; auto-warn when `contrast < 4.5` to keep “objects on surfaces visible.”
- **Variant buttons**: Tabs or toggles to flip between "sharp", "medium", and "pill" radius presets by updating related variables.
- **Font sandbox**: Dropdown for body font plus optional inputs for heading/logo/code. Missing values fall back automatically.
- **Snapshot + share**: Serialize the current `:root` variable set to JSON and the page URL hash for quick sharing, keeping the schema LLM-readable.

## Authoring Conventions for LLM Understanding
- **Consistent prefixes**: `surface.*`, `text.*`, `accent.*`, `radius.*`, `font.*`, `shadow.*`, `space.*`.
- **Inline guidance**: Short comments like `/* objects on surfaces must stay visible: keep contrast > 4.5 */` adjacent to token blocks.
- **Minimal nesting**: Favor flat structures in the DOM and data (no deep object trees). LLMs handle shallow, well-labeled maps more reliably.
- **Explicit optionality**: Mark optional tokens (e.g., `data-optional="true"`) and list defaults near the controls so generated themes include fallbacks without verbose prose.
- **Tiny examples**: Keep a few prefilled tokens with distinct values to show intent; avoid long sample datasets that obscure the schema.

## Implementation Tips
- Use a single `refresh()` function that re-reads inputs and applies CSS variables to `:root`, plus a `MutationObserver` to keep live previews in sync.
- Keep accessibility helpers inline: a `checkContrast(bg, text)` function and `aria-live` region for warnings.
- Store prompts and token manifests as small JSON blocks in `<script type="application/json">` tags for straightforward parsing by humans and LLMs alike.
- Prefer `dataset` lookups over class name parsing to keep the DOM clean and predictable.
- Avoid complex class systems; rely on the CSS variables themselves to express style changes.

By leaning on clear token names, inline previews, and shallow data, you get a doodling experience that is fun for humans and legible to LLMs—without introducing tooling or verbose markup.
