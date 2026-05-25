# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A collection of standalone, interactive HTML teaching guides built for a Hebrew-speaking student cohort (ML/AI, DevOps, Claude Code tooling). Each guide is a single self-contained `.html` file — all CSS and JS inlined, no build step, no shared assets. Pure static; viewed by opening the file in a browser or via GitHub Pages.

Some guides are course-wide (e.g. `i24-*`, `cnn.html`, `confusion-matrix-explorer.html`); others are addressed to a named student (`omer-concepts-guide.html`, `demo-to-production-itay.html`, `llm-guide-reference.html` for Eli). When editing a per-student guide, keep its tone and depth aligned with that student's level — don't generalize it.

## No build / no tests

There is nothing to install, build, lint, or test. Don't add a `package.json`, bundler, or CI pipeline unless the user explicitly asks. To view a guide locally: `open <file>.html` (macOS) or just double-click it.

## Authoring a new guide

Two paths:

1. **Use the `teaching-html` skill** (preferred for new topics) — it's tuned for this repo's style and bilingual conventions.
2. **Copy an existing guide as a template.** Good templates by category:
   - Interactive ML concept (sliders, canvas plots): `confusion-matrix-explorer.html`, `decision-tree.html`, `logistic-regression.html`
   - Step-by-step install with GIFs: `claude-code-installation-guide.html` (GIFs live in `gifs/`)
   - Concept reference cards: `omer-concepts-guide.html`, `llm-guide-reference.html`
   - Architecture / system explainer: `fullstack-data-flow.html`, `production-readiness-explorer.html`

After adding a guide, link it from `index.html` if it belongs in the main hub, or from `links.html` if it's a resource pointer.

## Style conventions (followed by all guides — match these)

- **Language toggle**: fixed top-right (or in `.top-nav`) with HE/EN buttons. Hebrew uses `<html lang="he" dir="rtl">`; English flips to `lang="en" dir="ltr"`. Most guides toggle via `data-i18n` attributes on translatable nodes, with a JS dictionary at the bottom of the file.
- **Typography**: Heebo from Google Fonts (`https://fonts.googleapis.com/css2?family=Heebo:wght@300;400;500;600;700&display=swap`) — it handles Hebrew + Latin cleanly.
- **Palette**: dark navy backgrounds (`#0f172a`, `#1a1a2e`), purple/indigo/pink gradients (`#667eea → #764ba2`, `#6366f1 → #c084fc → #f472b6`). Cards have subtle borders + glassmorphism (`backdrop-filter: blur`).
- **Interactivity**: vanilla JS only. Canvas for plots, SVG for diagrams, native `<input type="range">` for sliders. No React, no frameworks, no CDN libs beyond Google Fonts.
- **Self-contained**: don't extract shared CSS or JS into separate files. Each guide must be openable as a single file with no network calls except Google Fonts and (for some) inline images.

## Bilingual content guidance

When writing or editing guide content: Hebrew is the default for student-facing prose; technical terms (Python, gradient, overfitting, regression, GitHub, RAG, QLoRA, etc.) stay in English even inside Hebrew sentences. Avoid translating code identifiers, library names, or CLI flags.

## Tooling available

- **Playwright MCP** (`.mcp.json`) — enabled for headless browser validation. Use it to verify interactive guides render correctly and language toggles work, especially after style changes. Cached artifacts land in `.playwright-mcp/` (gitignored).
- **`.claude/skills/learn/`** — a project-local skill for generating new guide drafts.

## What lives where

- `*.html` at the root — the guides themselves (one per topic).
- `index.html` — Claude Code Windows install hub (also serves as a landing page).
- `links.html` — curated external resource links.
- `gifs/` — screen-recording GIFs referenced only by `claude-code-installation-guide.html`.
- `.claude/` — project Claude Code config + the `learn` skill.
- `.mcp.json` — Playwright MCP server registration.

## When making changes

- Edits to one HTML file never affect another — there are no shared dependencies. Don't refactor "for consistency" across files unless the user asks; the per-file independence is intentional.
- Don't strip the language toggle, the Heebo font load, or the RTL handling when editing — these are load-bearing for the student audience.
- GIFs in `gifs/` are referenced by filename from the install guide; if you rename one, update the `<img src="gifs/...">` references.
