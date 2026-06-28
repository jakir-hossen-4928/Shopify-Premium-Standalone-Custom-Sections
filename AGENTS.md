# AGENTS.md — Shopify Premium Standalone Custom Sections

## Repository structure

This repo is a flat collection of **standalone Shopify section files**. There is no build system, package manager, tests, CI, or bundler. Each `.liquid` file is a complete, self-contained Shopify section.

```
├── *.liquid              # 30+ standalone sections
├── images/               # README screenshots (not used by code)
├── README.md             # Visual catalog + installation guide
└── AGENTS.md             # This file
```

## Key architecture facts

- **All-in-one files**: Liquid markup, CSS (`<style>`), and JavaScript (`<script>`) are inlined within a single `.liquid` file. No external assets, no dependency on theme `assets/` folder.
- **Schema block**: Every section ends with `{% schema %}...{% endschema %}` defining theme editor settings (colors, sizes, toggles, content blocks). These settings are accessed via `{{ section.settings.xxx }}`.
- **Section-scoped CSS**: CSS rules are prefixed with a unique ID selector (`#hero-banner-{{ section.id }}`) to avoid style conflicts with other sections.
- **Zero theme pollution**: Sections do not modify `theme.liquid`, `theme.js`, or `theme.css`. They are drag-and-drop additions.

## Installation workflow

1. In Shopify Admin → Online Store → Themes → Edit Code → Sections → Add a new section
2. Paste the entire `.liquid` file contents
3. Customize via Theme Editor (the schema drives the editor UI)

No build, no deploy, no npm commands.

## Notable sections

| File | Notes |
|---|---|
| `custom-navbar-with-drawer.liquid` | Full navigation + cart drawer + predictive search. Dispatches/ listens for `cart:update`, `cart:open`, `ajaxProduct:added` events. Use variant ID (not product ID) with `/cart/add.js`. |
| `full-custom-header-with-sidebar-cart.liquid` | Alternative header with sidebar cart |
| `hero-banner.liquid` | ~940 lines, largest section — parallax, stats grid, dual CTAs, decorative blobs |

## Section conventions

- Section ID pattern: `#<section-name>-{{ section.id }}`
- Custom CSS properties (variables) are set on the section wrapper using `{{ section.settings.xxx }}` Liquid interpolation
- Responsive breakpoints: generally `@media (max-width: 768px)` and `(max-width: 480px)`
- All sections pin CSS via `<style>` tags inside the section HTML (no `{% style %}` tag)
- JavaScript is vanilla — no jQuery, no external libraries

## What is NOT in this repo

- No `theme.liquid`, `theme.js`, `theme.css`, or any Shopify theme wrapper files
- No `package.json`, lockfiles, or dependency manifests
- No build, lint, typecheck, or test commands
- No CI/CD configuration
- No Shopify CLI, Hydrogen, or app code
