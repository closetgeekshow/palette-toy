# Modularization Blueprint

Module entry (`tokens-runtime.js`): exports base token defaults, required/optional arrays, font imports, and a helper to inject a deduped Google Fonts link. Keep it pure data plus side-effect-free helpers.

UI helpers (`template-factories.js`): expose small functions for pills, tabs, meters, and skeleton rows that accept a token map and return DOM strings/fragments. Include copy/paste utilities to drop rendered HTML into plain pages.

Prompt + instruction module (`prompt-kits.js`): generates schema expectations from the live token list, assembles prompt text, and bundles guidance strings for documentation.

JSON editor host (`json-editor-shell.js`): wraps the existing editor logic, pulling helpers from the above modules while preserving current behaviors. Add light boilerplate to push updates into template code and clipboard-friendly exports.
