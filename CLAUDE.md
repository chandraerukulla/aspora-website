# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Aspora is a fintech SPA (single-page application) for diaspora banking, remittances, and investments. The entire application lives in a single file: `aspora-website.html`.

## Development

No build tools, no package manager. Open `aspora-website.html` directly in a browser or serve it with any static file server:

```bash
python3 -m http.server 8080
# or
npx serve .
```

## Architecture

**Single-file SPA** — all HTML, CSS (~750 lines), and JavaScript are embedded in `aspora-website.html`.

### Routing

Client-side routing via the `nav(page)` function: shows the matching `#page-{name}` element and hides all others (`.page.active`). Pages are navigated with `onclick="nav('page-name')"` inline handlers.

Active pages: `home`, `products`, `remittance`, `banking`, `investments`, `support`, `learn`, `asset`, `option-chain`, `transaction`, `bank-account`.

### State

Single global: `let currentCountry = 'IN'` — drives which products render. Changed via `homeCountry()` / `prodCountry()` / `updateNavFlag()`.

### Data

`const PRODUCTS` object keyed by country code (`IN`, `US`, `UK`, `OTHER`). Each product entry has: `cls`, `icon`, `stag`, `title`, `page`, `desc`. `renderGrid(gridId, country)` builds the product card HTML from this data.

### Design System

CSS custom properties in `:root` define the full token set:
- Brand colors: `--crimson` (remittance), `--teal` (banking), `--gold` (investments)
- Page-scoped color overrides use `#page-{name} .selector` patterns

### CSS Organization (in order)

TOKENS → RESET → PAGE ROUTER → NAVIGATION → HERO → MANIFESTO → SECTION SCAFFOLD → COUNTRY TABS → PRODUCT CARDS → HOW IT WORKS → TRUST → CTA BAND → FOOTER → PRODUCT HERO → ASSET DETAIL → OPTION CHAIN → TRANSACTION PAGE → BANK ACCOUNT → PRODUCT PAGE COLOR THEMING
