# Proposed Agent Rules (≤100 words)

1. Mirror required/optional token metadata across every demo before adding new UI changes.
2. Keep functional code in existing HTML pages; only add files when explicitly requested.
3. Use CDN-only dependencies and avoid build steps.
4. Update `menu.html` whenever demos change, including refreshed line counts.
5. Ensure font imports dedupe into one Google Fonts link per page with `--font-body` as the only required stack.
6. Ship keyboard access for tabs, toggles, radios, and checks in every interaction surface.
