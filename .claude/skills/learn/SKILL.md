---
name: learn
description: Generate an interactive visual learning guide for any topic and deploy it to GitHub Pages. Use when user says "learn about", "teach me", "visual guide for", "explain visually", or provides a topic to learn.
argument-hint: topic name (e.g., "transformers", "gradient descent", "backpropagation")
---

# Interactive Visual Learning Guide Generator

Creates a beautiful, interactive single-file HTML visual guide for any given topic, then deploys it to a new public GitHub repo with GitHub Pages.

## Instructions

### Step 1: Parse the topic

Extract the topic from the user's argument. Convert it to:
- `TOPIC_DISPLAY`: Human-readable name (e.g., "Gradient Descent", "Transformers")
- `TOPIC_SLUG`: kebab-case for repo/file naming (e.g., "gradient-descent", "transformers")
- `REPO_NAME`: `{TOPIC_SLUG}-visual-guide`

### Step 2: Research the topic

Before writing any HTML, think deeply about the topic and plan the content:

1. **Core concept** — What is it? One-sentence explanation a beginner can understand.
2. **Analogy** — 4 relatable real-world analogies (like "baby learning to see" for CNN).
3. **Visual hierarchy** — 3-5 stages that build from simple to complex (like "edges -> textures -> parts -> objects" for CNN).
4. **Process/Pipeline** — The full step-by-step flow with 5-7 clickable stages, each with a detailed explanation in both English and Hebrew.
5. **Interactive demo** — Design ONE interactive demo that lets users click through the concept step by step. This is the most important part. Examples:
   - For gradient descent: animate a ball rolling down a curve
   - For backpropagation: step through error flowing backward through layers
   - For transformers: show attention weights highlighting between words
   - For decision trees: build a tree step by step with splits
6. **Real-world applications** — 6 cards showing where this is used.
7. **Key takeaways** — 5-6 bullet points summarizing everything.

### Step 3: Generate the HTML

Create a single `index.html` file following the template structure in `references/html-template-guide.md`.

CRITICAL requirements:
- Full English AND Hebrew translations using the `data-i18n` attribute system
- RTL support when Hebrew is selected (`dir="rtl"`, arrows flip)
- Language toggle button fixed at top-right
- Dark theme: background `#0f172a`, cards `#1e293b`, borders `#334155`
- Gradient accents: purples `#818cf8`, `#c084fc`, pinks `#f472b6`
- All interactive demos must work in both languages
- Single file — no external dependencies (no CDN links, no frameworks)
- Mobile responsive
- Smooth transitions and hover effects on all cards

### Step 4: Create a temporary project directory and initialize git

```bash
# Create temp directory for the new project
WORK_DIR=$(mktemp -d)
# Copy index.html there
# Initialize git repo
cd "$WORK_DIR"
git init
git add index.html
git commit -m "Add {TOPIC_DISPLAY} visual guide with English/Hebrew toggle"
```

### Step 5: Create GitHub repo and deploy

1. **Ensure gh CLI is available:**
   - Check if `gh` is in PATH
   - If not, check `/tmp/gh_install/gh_2.67.0_macOS_arm64/bin/gh`
   - If not found, download it:
     ```bash
     curl -sL https://github.com/cli/cli/releases/download/v2.67.0/gh_2.67.0_macOS_arm64.zip -o /tmp/gh.zip
     unzip -o /tmp/gh.zip -d /tmp/gh_install
     ```
   - Set `GH` variable to the working binary path

2. **Verify authentication:**
   ```bash
   $GH auth status
   ```

3. **Create public repo and push:**
   ```bash
   $GH repo create {REPO_NAME} --public --source=. --push \
     --description "Interactive visual guide to {TOPIC_DISPLAY} with English/Hebrew support"
   ```

4. **Create GitHub Pages workflow:**

   Create `.github/workflows/pages.yml`:
   ```yaml
   name: Deploy to GitHub Pages
   on:
     push:
       branches: [main]
   permissions:
     contents: read
     pages: write
     id-token: write
   concurrency:
     group: pages
     cancel-in-progress: false
   jobs:
     deploy:
       environment:
         name: github-pages
         url: ${{ steps.deployment.outputs.page_url }}
       runs-on: ubuntu-latest
       steps:
         - uses: actions/checkout@v4
         - uses: actions/configure-pages@v5
         - uses: actions/upload-pages-artifact@v3
           with:
             path: .
         - id: deployment
           uses: actions/deploy-pages@v4
   ```

   Commit and push the workflow file.

5. **Enable GitHub Pages via API:**
   ```bash
   $GH api repos/{OWNER}/{REPO_NAME}/pages -X POST \
     --input - <<< '{"build_type":"workflow","source":{"branch":"main","path":"/"}}'
   ```

6. **Get the GitHub username** from `$GH api user --jq .login` for the final URL.

### Step 6: Return results to user

Show the user:
- **Repository URL**: `https://github.com/{OWNER}/{REPO_NAME}`
- **Live site URL**: `https://{OWNER}.github.io/{REPO_NAME}/`
- Note that deployment takes ~1 minute

## Quality Check

CRITICAL: Before deploying, verify:
- [ ] HTML is valid and self-contained (no external deps)
- [ ] Language toggle switches ALL text between English and Hebrew
- [ ] RTL layout works correctly in Hebrew mode (arrows flip, text aligns right)
- [ ] Interactive demo has Step, Auto Play, and Reset buttons (all translated)
- [ ] All 7 sections are present: Hero, Analogies, Visual Hierarchy, Interactive Demo, Pipeline, Applications, Takeaways
- [ ] Pipeline stages are clickable with detailed explanations in both languages
- [ ] Mobile responsive (test mentally: does the grid collapse, are buttons reachable?)
- [ ] Dark theme colors match the spec (#0f172a, #1e293b, purple/pink gradients)

## Examples

### Example 1: /learn gradient descent
- Creates `gradient-descent-visual-guide` repo
- Interactive demo: ball rolling down a loss curve, step by step with learning rate control
- Pipeline: Define Loss -> Calculate Gradient -> Update Weights -> Check Convergence -> Repeat
- Analogies: hiker in fog, rolling a ball downhill, hot/cold game, tuning a radio

### Example 2: /learn transformers
- Creates `transformers-visual-guide` repo
- Interactive demo: self-attention mechanism showing how words attend to each other
- Pipeline: Input Embedding -> Positional Encoding -> Self-Attention -> Feed Forward -> Output
- Analogies: reading a book with context, spotlight on a stage, conversation between words

### Example 3: /learn backpropagation
- Creates `backpropagation-visual-guide` repo
- Interactive demo: error flowing backward through a small network, updating weights
- Pipeline: Forward Pass -> Calculate Loss -> Backward Pass -> Update Weights -> Iterate
- Analogies: teacher correcting homework, chain of whispers, domino effect

## Troubleshooting

### gh CLI not found
Cause: Not installed via brew/conda
Fix: Download binary directly to `/tmp/gh_install/` using curl from GitHub releases

### gh auth not logged in
Cause: User hasn't authenticated
Fix: Run `$GH auth login` and follow the prompts. Needs `repo` scope.

### GitHub Pages shows 404
Cause: The workflow deployment hasn't completed yet
Fix: Wait 1-2 minutes. Check status at `https://github.com/{OWNER}/{REPO_NAME}/actions`

### Repo name already exists
Cause: A repo with the same name already exists for this user
Fix: Append a number suffix (e.g., `transformers-visual-guide-2`) or ask the user what to do
