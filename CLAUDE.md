# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A single-file static landing page (`index.html`) for **Career Ops** — an AI job-search toolkit targeting professional immigrants in the Australian market. There is no build system, bundler, framework, or package manager. The entire site is one self-contained HTML file.

## How to preview

Open `index.html` directly in a browser, or serve it with any static file server:

```bash
npx serve .
# or
python -m http.server 8080
```

## Architecture

Everything lives in `index.html`:

- **`<head>`** — meta/OG tags, Google Fonts (`Playfair Display`, `DM Mono`, `Syne`), inline `<style>` block, emoji favicon via SVG data URI.
- **CSS** — all styles are inline in the `<style>` block. Design tokens live in `:root` CSS variables (`--bg`, `--teal`, `--amber`, etc.). Layout uses CSS Grid throughout.
- **HTML sections** (in order): Nav → Hero → Origin → Problem → Tools → How It Works → Differentiators → Pricing → CTA → Footer.
- **JS** — a single `IntersectionObserver` at the bottom of `<body>` drives the `.reveal` scroll-animation system. No other JavaScript.

## Key design conventions

- `.z` class sets `position: relative; z-index: 1` to layer content above the CSS `body::before` grid texture and `body::after` noise overlay.
- `.reveal` + `.reveal-d1/d2/d3/d4` handle staggered scroll-in animations — add these classes to any new content that should animate in on scroll.
- Primary colour is `--teal` (`#0AA898`). Use it for accents, highlights, and CTAs. `--amber` is reserved for the "External / full price" pricing tier.
- Buttons: `.btn-os` for OS download buttons, `.btn-primary` for main CTAs, `.btn-secondary` for ghost/outline.

## External dependencies

- **Google Fonts** (CDN) — loaded in `<head>`.
- **Stripe** — payment links point to `buy.stripe.com` (currently test-mode URLs).
- **GitHub Releases** — installer download links point to `github.com/Mr-JotA-94/career-ops/releases/latest/download/`.

## Responsive breakpoints

- `≤900px` — single-column grids, hide `.hero-bg-word`, stack `.asymmetry-block`.
- `≤600px` — further collapse tools/flow grids, hide `.nav-tag`.
