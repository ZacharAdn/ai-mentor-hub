# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A collection of standalone, interactive HTML teaching guides built for a Hebrew-speaking student cohort (ML/AI, DevOps, Claude Code tooling). Each guide is a single self-contained `.html` file — all CSS and JS inlined, no build step, no shared assets. Pure static; viewed by opening the file in a browser or via GitHub Pages.

Guides are categorized into three folders: `interactive-ml-concepts/`, `architecture-production/`, `tooling-setup/`. The root `index.html` is the Windows Claude Code install guide and doubles as the GitHub Pages landing page — it stays at root, not in `tooling-setup/`. Some guides are course-wide (e.g. `i24-*`, `cnn.html`, `confusion-matrix-explorer.html`); others are addressed to a named student (`omer-concepts-guide.html`, `demo-to-production-itay.html`, `llm-guide-reference.html` for Eli). When editing a per-student guide, keep its tone and depth aligned with that student's level — don't generalize it.

## No build / no tests

There is nothing to install, build, lint, or test. Don't add a `package.json`, bundler, or CI pipeline unless the user explicitly asks. To view a guide locally: `open <file>.html` (macOS) or just double-click it.

## Authoring a new guide

Two paths:

1. **Use the `teaching-html` skill** (preferred for new topics) — it's tuned for this repo's style and bilingual conventions.
2. **Copy an existing guide as a template.** Good templates by category:
   - Interactive ML concept (sliders, canvas plots): `interactive-ml-concepts/confusion-matrix-explorer.html`, `interactive-ml-concepts/decision-tree.html`, `interactive-ml-concepts/logistic-regression.html`
   - Step-by-step install with GIFs: `tooling-setup/claude-code-installation-guide.html` (GIFs live in `gifs/`, referenced as `../gifs/...` from the subfolder)
   - Concept reference cards: `interactive-ml-concepts/omer-concepts-guide.html`, `interactive-ml-concepts/llm-guide-reference.html`
   - Architecture / system explainer: `architecture-production/fullstack-data-flow.html`, `architecture-production/production-readiness-explorer.html`

Place the new guide in the matching folder and add a row to the README table. If it references images, use `../gifs/<subfolder>/<file>` paths so they resolve from the nested location. If it links back to the landing page, use `href="../index.html"`.

## Style conventions (followed by all guides — match these)

- **Language toggle**: fixed top-right (or in `.top-nav`) with HE/EN buttons. Hebrew uses `<html lang="he" dir="rtl">`; English flips to `lang="en" dir="ltr"`. Most guides toggle via `data-i18n` attributes on translatable nodes, with a JS dictionary at the bottom of the file.
- **Typography**: Heebo from Google Fonts (`https://fonts.googleapis.com/css2?family=Heebo:wght@300;400;500;600;700&display=swap`) — it handles Hebrew + Latin cleanly.
- **Palette**: dark navy backgrounds (`#0f172a`, `#1a1a2e`), purple/indigo/pink gradients (`#667eea → #764ba2`, `#6366f1 → #c084fc → #f472b6`). Cards have subtle borders + glassmorphism (`backdrop-filter: blur`).
- **Theme toggle (MANDATORY for every guide — Zac's standing request, 2026-06-10)**: each guide ships both themes. All colors behind CSS variables: `:root` holds the dark palette, `html[data-theme="light"]` overrides it (light bg `#f4f6fa`, white cards, borders `#d9e0ea`, accents darkened for contrast on white: `#4f46e5`, `#7c3aed`, `#db2777`). A ☀️/🌙 button sits inside the `.lang-toggle` bar, persists via localStorage (`guideTheme`), and honors a `?theme=light|dark` URL param. **Default is light.** JS-generated SVG must use CSS classes (`.svg-panel`, `.svg-axis`, `.svg-lbl`, `.svg-lbl-strong`) instead of inline fills so it re-themes live. Reference implementation: `recsys-three-models.html`. Older dark-only guides get the toggle when next touched.
- **Interactivity**: vanilla JS only. Canvas for plots, SVG for diagrams, native `<input type="range">` for sliders. No React, no frameworks, no CDN libs beyond Google Fonts.
- **Self-contained**: don't extract shared CSS or JS into separate files. Each guide must be openable as a single file with no network calls except Google Fonts and (for some) inline images.

## Bilingual content guidance

When writing or editing guide content: Hebrew is the default for student-facing prose; technical terms (Python, gradient, overfitting, regression, GitHub, RAG, QLoRA, etc.) stay in English even inside Hebrew sentences. Avoid translating code identifiers, library names, or CLI flags.

## Tooling available

- **Playwright MCP** (`.mcp.json`) — enabled for headless browser validation. Use it to verify interactive guides render correctly and language toggles work, especially after style changes. Cached artifacts land in `.playwright-mcp/` (gitignored).
- **`.claude/skills/learn/`** — a project-local skill for generating new guide drafts.

## What lives where

- `index.html` — Claude Code Windows install guide; doubles as the GitHub Pages landing page (kept at root).
- `interactive-ml-concepts/` — ML/AI concept guides with live sliders/canvas (logistic regression, decision tree, confusion matrix, CNN, LLM, etc.).
- `architecture-production/` — system-architecture, production-readiness, and i24 project guides.
- `tooling-setup/` — installation, setup, and tooling guides (Claude Code, Git/GitHub, Technion LBS, WhatsApp, OpenClaw, links hub, etc.).
- `gifs/` — screenshots and GIFs, organized in per-guide subfolders (e.g. `gifs/git-github/`). Referenced from guides in subfolders as `../gifs/<subfolder>/<file>`.
- `.claude/` — project Claude Code config + the local `learn` skill.
- `.mcp.json` — Playwright MCP server registration.

## When making changes

- Edits to one HTML file never affect another — there are no shared dependencies. Don't refactor "for consistency" across files unless the user asks; the per-file independence is intentional.
- Don't strip the language toggle, the Heebo font load, or the RTL handling when editing — these are load-bearing for the student audience.
- If you move a guide between folders, update its `src="../gifs/..."` and `href="../index.html"` paths to match the new depth, and update the table in `README.md`.
