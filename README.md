# AI Mentor Hub

A collection of interactive HTML teaching guides for Hebrew-speaking students in ML/AI, DevOps, and developer tooling. Each guide is a single self-contained `.html` file — all CSS and JS inlined, no build step, no dependencies.

The guide content is bilingual (mostly Hebrew with English technical terms); this README and the rest of the repo plumbing are in English.

## Viewing a guide

Just open any `.html` in a browser — no server, no install:

```bash
open interactive-ml-concepts/confusion-matrix-explorer.html   # macOS
start interactive-ml-concepts/confusion-matrix-explorer.html  # Windows
```

The repo is also published via GitHub Pages: <https://zacharadn.github.io/ai-mentor-hub/>

## Guides

### Interactive ML/AI concepts

| Guide | Topic |
|-------|-------|
| [logistic-regression.html](interactive-ml-concepts/logistic-regression.html) | Logistic regression with live sliders and scatter plots |
| [how-models-learn.html](interactive-ml-concepts/how-models-learn.html) | How models learn, step by step — logistic line nudged per-point, tree built split-by-split, forest voting (real in-browser training) |
| [decision-tree.html](interactive-ml-concepts/decision-tree.html) | Decision trees and overfitting — tree-depth slider |
| [overfitting-explorer.html](interactive-ml-concepts/overfitting-explorer.html) | Overfitting, validation set, leakage & model comparison — real in-browser models, live decision boundary, train/test U-curve |
| [confusion-matrix-explorer.html](interactive-ml-concepts/confusion-matrix-explorer.html) | Confusion matrix, precision, recall — threshold slider |
| [cnn.html](interactive-ml-concepts/cnn.html) | Convolutional neural networks — animated diagrams |
| [llm-guide.html](interactive-ml-concepts/llm-guide.html) | LLM fundamentals |
| [llm-guide-reference.html](interactive-ml-concepts/llm-guide-reference.html) | LLM deep-dive reference (Eli) |
| [omer-concepts-guide.html](interactive-ml-concepts/omer-concepts-guide.html) | VIF, feature engineering, stacking, RAG, QLoRA (Omer) |

### Architecture and production

| Guide | Topic |
|-------|-------|
| [fullstack-data-flow.html](architecture-production/fullstack-data-flow.html) | Data flow in a full-stack architecture |
| [demo-to-production-itay.html](architecture-production/demo-to-production-itay.html) | From demo to production (Itay) |
| [production-readiness-explorer.html](architecture-production/production-readiness-explorer.html) | 7-dimensional production-readiness framework |
| [i24-three-pillars.html](architecture-production/i24-three-pillars.html) | i24 project broken into three pillars |
| [i24-timeseries-deep-dive.html](architecture-production/i24-timeseries-deep-dive.html) | Time-series deep dive for i24 |

### Tooling and setup

| Guide | Topic |
|-------|-------|
| [index.html](index.html) | Claude Code installation — Windows (also serves as the site landing page) |
| [claude-code-installation-guide.html](tooling-setup/claude-code-installation-guide.html) | Claude Code installation — Windows, Mac, VS Code |
| [ai-workspace-setup-gil.html](tooling-setup/ai-workspace-setup-gil.html) | Non-technical beginner setup (Gil) — Stage 1: Claude Desktop + Obsidian; Stage 2 (bonus, later): dev stack via the main guide |
| [git-github-setup.html](tooling-setup/git-github-setup.html) | From zero to first push — GitHub signup, Git install, config, commit/push via the VS Code UI |
| [git-github-uri.html](tooling-setup/git-github-uri.html) | Minimal Windows-only prerequisite for Uri — GitHub signup + Git install/config only, verification steps delegated to Claude instead of a terminal |
| [technion-lbs-setup.html](tooling-setup/technion-lbs-setup.html) | Technion LBS course dev environment setup |
| [geoai-rg-setup.html](tooling-setup/geoai-rg-setup.html) | GeoAI / RG Innovation dev environment setup (Geo-AI-Course org) |
| [whatsapp-setup.html](tooling-setup/whatsapp-setup.html) | WhatsApp Skill installation |
| [hebrew-terminal-fix.html](tooling-setup/hebrew-terminal-fix.html) | Fixing Hebrew display in the Windows terminal |
| [self-improving-skills-hooks.html](tooling-setup/self-improving-skills-hooks.html) | Claude Code Skills and Hooks system |
| [openclaw-guide.html](tooling-setup/openclaw-guide.html) | Pointer to the OpenClaw guide |
| [links.html](tooling-setup/links.html) | Curated external resource links |

## Adding a new guide

Two paths:

1. **Use the `teaching-html` skill** inside Claude Code — it's tuned to this repo's bilingual conventions and visual style.
2. **Copy an existing guide as a template.** Match by interaction style:
   - Interactive ML concept (sliders, canvas plots) → `interactive-ml-concepts/confusion-matrix-explorer.html`, `interactive-ml-concepts/decision-tree.html`
   - Step-by-step setup with screenshots → `tooling-setup/git-github-setup.html`, `tooling-setup/claude-code-installation-guide.html`
   - Concept reference cards → `interactive-ml-concepts/omer-concepts-guide.html`, `interactive-ml-concepts/llm-guide-reference.html`
   - Architecture / system explainer → `architecture-production/fullstack-data-flow.html`, `architecture-production/production-readiness-explorer.html`

Place the new file in the matching folder, add a row to the table above, and (if it references images) reference them as `../gifs/<subfolder>/<file>` so the path works from the nested location.

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
├── index.html                      # Site landing (Claude Code Windows install)
├── interactive-ml-concepts/        # ML/AI concept guides with live interactivity
├── architecture-production/        # System / production / project-architecture guides
├── tooling-setup/                  # Installation, setup, and tooling guides
├── gifs/                           # Screenshots and GIFs (per-guide subfolders)
├── .claude/                        # Claude Code project config + local learn skill
└── .mcp.json                       # Playwright MCP server registration
```

For deeper conventions and authoring notes, see [CLAUDE.md](CLAUDE.md).
