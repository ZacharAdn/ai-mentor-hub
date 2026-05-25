# Student Guides

A collection of interactive HTML teaching guides for Hebrew-speaking students in ML/AI, DevOps, and developer tooling. Each guide is a single self-contained `.html` file — all CSS and JS inlined, no build step, no dependencies.

The guide content is bilingual (mostly Hebrew with English technical terms); this README and the rest of the repo plumbing are in English.

## Viewing a guide

Just open any `.html` in a browser — no server, no install:

```bash
open confusion-matrix-explorer.html   # macOS
start confusion-matrix-explorer.html  # Windows
```

The repo is also published via GitHub Pages: <https://zacharadn.github.io/student-guides/>

## Guides

### Interactive ML/AI concepts

| Guide | Topic |
|-------|-------|
| [logistic-regression.html](logistic-regression.html) | Logistic regression with live sliders and scatter plots |
| [decision-tree.html](decision-tree.html) | Decision trees and overfitting — tree-depth slider |
| [confusion-matrix-explorer.html](confusion-matrix-explorer.html) | Confusion matrix, precision, recall — threshold slider |
| [cnn.html](cnn.html) | Convolutional neural networks — animated diagrams |
| [llm-guide.html](llm-guide.html) | LLM fundamentals |
| [llm-guide-reference.html](llm-guide-reference.html) | LLM deep-dive reference (Eli) |
| [omer-concepts-guide.html](omer-concepts-guide.html) | VIF, feature engineering, stacking, RAG, QLoRA (Omer) |

### Architecture and production

| Guide | Topic |
|-------|-------|
| [fullstack-data-flow.html](fullstack-data-flow.html) | Data flow in a full-stack architecture |
| [demo-to-production-itay.html](demo-to-production-itay.html) | From demo to production (Itay) |
| [production-readiness-explorer.html](production-readiness-explorer.html) | 7-dimensional production-readiness framework |
| [i24-three-pillars.html](i24-three-pillars.html) | i24 project broken into three pillars |
| [i24-timeseries-deep-dive.html](i24-timeseries-deep-dive.html) | Time-series deep dive for i24 |

### Tooling and setup

| Guide | Topic |
|-------|-------|
| [index.html](index.html) | Claude Code installation — Windows |
| [claude-code-installation-guide.html](claude-code-installation-guide.html) | Claude Code installation — Windows, Mac, VS Code |
| [git-github-setup.html](git-github-setup.html) | From zero to first push — GitHub signup, Git install, config, commit/push via the VS Code UI |
| [technion-lbs-setup.html](technion-lbs-setup.html) | Technion LBS course dev environment setup |
| [whatsapp-setup.html](whatsapp-setup.html) | WhatsApp Skill installation |
| [hebrew-terminal-fix.html](hebrew-terminal-fix.html) | Fixing Hebrew display in the Windows terminal |
| [self-improving-skills-hooks.html](self-improving-skills-hooks.html) | Claude Code Skills and Hooks system |
| [openclaw-guide.html](openclaw-guide.html) | Pointer to the OpenClaw guide |
| [links.html](links.html) | Curated external resource links |

## Adding a new guide

Two paths:

1. **Use the `teaching-html` skill** inside Claude Code — it's tuned to this repo's bilingual conventions and visual style.
2. **Copy an existing guide as a template.** Match by interaction style:
   - Interactive ML concept (sliders, canvas plots) → `confusion-matrix-explorer.html`, `decision-tree.html`
   - Step-by-step setup with screenshots → `git-github-setup.html`, `claude-code-installation-guide.html`
   - Concept reference cards → `omer-concepts-guide.html`, `llm-guide-reference.html`
   - Architecture / system explainer → `fullstack-data-flow.html`, `production-readiness-explorer.html`

After adding, link the new guide from `index.html` (main hub) or `links.html` (resource pointer), and add a row to the table above.

## Style conventions

All guides follow the same conventions — match them when authoring or editing:

- **Language**: Hebrew is the default for student-facing prose; technical terms (Python, gradient, overfitting, RAG, etc.) stay in English even inside Hebrew sentences. RTL layout via `<html lang="he" dir="rtl">`. Some guides include an HE/EN toggle.
- **Typography**: Heebo from Google Fonts (handles Hebrew + Latin cleanly).
- **Palette**: dark navy backgrounds (`#0f172a`, `#1a1a2e`), purple/indigo/pink gradients.
- **Interactivity**: vanilla JS only — Canvas for plots, SVG for diagrams, native `<input type="range">` sliders. No frameworks, no CDN libs beyond Google Fonts.
- **Self-contained**: each guide must open as a single file. Don't extract shared CSS or JS.

## Repo layout

```
.
├── *.html              # The guides — each one fully self-contained
├── gifs/               # Screenshots and GIFs (per-guide subfolders)
├── .claude/            # Claude Code project config + local learn skill
└── .mcp.json           # Playwright MCP server registration (browser validation)
```

For deeper conventions and authoring notes, see [CLAUDE.md](CLAUDE.md).
