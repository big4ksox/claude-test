# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static website for **피네스테틱 (Fi_ne.sthetic)**, a Korean aesthetic clinic in Incheon. Deployed to GitHub Pages automatically on every push to `main`.

There is no build step — all files are served directly as-is.

## Deployment

Push to `main` triggers `.github/workflows/static.yml`, which deploys the entire repository root to GitHub Pages. No build tool, no bundler, no package manager.

## File Structure

- `index.html` — Single-page main site (all CSS and JS are inline/embedded)
- `blog_p2.html` – `blog_p5.html`, `blog_raw.html` — Exported Naver blog pages (legacy, not linked from main site)
- `images/instagram/` — Before/After photos and video files referenced directly in `index.html`
- `images/director.jpg` — Director portrait used in the About section

## Architecture of `index.html`

All styles are in a single `<style>` block in `<head>`. All JavaScript is in a single `<script>` block at end of `<body>`. There are no external dependencies or CDN links.

**CSS variables** (defined in `:root`): `--white`, `--off-white`, `--light-gray`, `--mid-gray`, `--dark`, `--accent`, `--gold`, `--gold-light`, `--radius`, `--radius-sm`.

**Sections** (in DOM order, each with a matching `id` for nav anchor links):
`#home` → `#services` → `#results` → `#about` → `#products` → `#process` → `#reviews` → `#location` → `footer`

**Key JavaScript patterns:**
- **Scroll reveal**: Elements with class `.reveal` become visible (`.reveal.visible`) via `IntersectionObserver` with a staggered `setTimeout` delay.
- **Before/After filter**: `.ba-tab[data-filter]` buttons show/hide `.ba-card[data-category]` elements. The tab value `"all"` shows everything; other values match `data-category` exactly.
- **Active nav highlighting**: A second `IntersectionObserver` (threshold 0.5) updates opacity/fontWeight on `.nav-links a` elements based on which `section[id]` is in view.

## Content Language

All user-facing text is in Korean. Keep it Korean when editing content. Section eyebrows and some badges use English labels (e.g., "Services", "Before", "After").
