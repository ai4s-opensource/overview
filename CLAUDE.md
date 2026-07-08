# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A static Chinese-language landing page showcasing AI for Science (AI4S) annual achievements from four Chinese research institutions (智源研究院, 昌平实验室, 深圳河套学院, 中国科学技术大学). The page is a single HTML file with embedded CSS and JavaScript — no build system, no dependencies, no framework.

## Tech Stack

- **Language:** Vanilla HTML5, CSS3, JavaScript (ES6)
- **Fonts:** Google Fonts (Space Grotesk, Inter) — loaded via `<link>` in the `<head>`
- **No build tools, no package manager, no framework**

## Project Structure

```
AI4S-web/
├── index.html      # Single-page site — all HTML, CSS, JS in one file
├── web.md          # Content source / spec document (markdown)
├── 1-1.png         # Project 1 image assets
├── 1-2.png
├── 1-3.png
├── 2-1.gif         # Project 2 animated comparison
├── 3-1.png         # Project 3 image assets
├── 3-2.png
├── 3-3.png
├── 4-1.jpg         # Project 4 image assets
├── 4-2.png
├── 4-3.jfif
└── CLAUDE.md       # This file
```

## Architecture

The entire page is self-contained in `index.html`:

1. **CSS Design Tokens** — CSS custom properties (`:root` variables) for colors, typography, spacing, layout, transitions, and border radii. Dark theme (deep navy/teal palette).
2. **HTML Sections:**
   - **Nav** — fixed top bar with logo and CTA
   - **Hero** — full-viewport intro with animated entrance
   - **Projects (#projects)** — 4 project articles, each with text and image in a 2-column grid (alternating layout via `direction: rtl` on even children)
   - **Impact (#impact)** — 4-card dashboard with animated number counters
   - **Recruitment (#recruitment)** — hiring section with 3 role cards
   - **Footer**
3. **JavaScript (IIFE at bottom of `<body>`):**
   - Particle network canvas background with mouse interaction
   - `IntersectionObserver`-based scroll reveal animations
   - Counter animation (ease-out cubic) triggered on scroll

## Key Patterns

- **Scroll animations:** Elements with class `.reveal` or attribute `data-reveal` fade up on scroll via `IntersectionObserver`
- **Counter animation:** `.counter` elements inside `.impact-card` animate from 0 to their `data-target` value when scrolled into view
- **Image fallback:** `window.imgError()` replaces broken images with an SVG placeholder
- **Responsive breakpoints:** 1024px, 768px, 480px
- **Accessibility:** `prefers-reduced-motion` support, `focus-visible` styles, `sr-only` utility class, semantic HTML

## Development

Since this is a static site with no build tooling:

- **Preview:** Open `index.html` directly in a browser (file:// or any static server)
- **No tests, no linter, no CI/CD pipeline**
- There is no `web.md` → `index.html` generation pipeline — content changes should be made directly in `index.html`
- Image assets are referenced as relative paths (`./1-3.png`)

## Conventions

- CSS uses custom properties for all design tokens (colors, spacing, type scale)
- Animations use the `--ease-out` cubic-bezier consistently
- All text content is in Simplified Chinese (zh-CN)
- External links open in new tabs (`target="_blank" rel="noopener"`)
- Use `loading="lazy"` on images
