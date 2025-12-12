# Research: succinct CSS authoring options

## Goals
- Reduce repetitive CSS while keeping the code CDN-only and build-free.
- Preserve explicit CSS variable usage so themes remain data-driven.
- Favor techniques LLMs can read and extend without opaque macros.

## Approaches
- **Open Props**: already used in a demo; ships a dense set of variables over CDN. Great for spacing, radii, typography, and color seeds with minimal authoring.
- **Shoelace themes**: pairs CSS variables with web components. You can theme via variables only and skip writing component CSS altogether.
- **Radix Colors tokens**: a CDN JSON or CSS file supplies well-tuned color ramps; authors only map the ramps to semantic variables.
- **Water.css / new.css**: classless CSS frameworks that style raw HTML elements. They shrink the amount of custom CSS needed but are less token-centric.
- **Pico.css**: lightweight semantic class system with CSS variables. Authors can override a handful of root variables to restyle controls.
- **Open Props + PostCSS-less utility extraction**: use the prebuilt utility classes that ship with Open Props via CDN (e.g., `.shadow-3`, `.radius-2`) to avoid restating shadows and radii. No build step required.
- **Capsize.js via esm.sh**: if typography sizing is verbose, Capsize computes cap-height-driven line-heights from CDN without build tooling.
- **Mini CSS-in-HTML snippets**: store reusable rule blocks in `<template>` tags and clone them into a `<style>` element when needed; this keeps repetition down without external tools.

## Patterns to avoid
- **Utility-first build systems**: Tailwind/JIT-style systems require builds and are outside the repo constraints.
- **Preprocessors**: Sass/Less/Stylus would add a build step and are not suitable here.

## Recommendation
Lean on CDN token packs (Open Props, Radix Colors) combined with semantic CSS variables. For brevity, classless frameworks or Pico.css can cut boilerplate, and Capsize can keep font sizing concise—all without bundlers.
