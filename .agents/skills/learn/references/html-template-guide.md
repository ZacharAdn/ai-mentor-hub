# HTML Template Structure Guide

This document describes the exact structure and patterns to follow when generating visual learning guides. Use the CNN visual guide as the canonical reference.

## Overall HTML Structure

```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>{TOPIC} Visual Guide</title>
  <style>/* All CSS inline */</style>
</head>
<body>
  <!-- Language Toggle (fixed top-right) -->
  <!-- Hero Section -->
  <!-- Section 1: What is {TOPIC}? + Analogies -->
  <!-- Section 2: Visual Hierarchy (layered understanding) -->
  <!-- Section 3: Interactive Demo (THE CORE) -->
  <!-- Section 4: Process Detail (e.g., Pooling for CNN) -->
  <!-- Section 5: Full Pipeline (clickable stages) -->
  <!-- Section 6: Real-World Applications -->
  <!-- Section 7: Key Takeaways -->
  <!-- Footer -->
  <script>/* All JS inline */</script>
</body>
</html>
```

## Language Toggle System

### HTML Pattern
Every translatable element gets a `data-i18n` attribute:
```html
<h2 data-i18n="section_title">English Title</h2>
<p data-i18n="section_desc">English description with <strong>HTML</strong> allowed.</p>
```

Arrows that need to flip in RTL get `data-i18n-arrow`:
```html
<div class="hier-arrow" data-i18n-arrow>-></div>
```

### Toggle Button HTML
```html
<div class="lang-toggle">
  <button class="lang-btn active" id="btn-en" onclick="setLang('en')">EN English</button>
  <button class="lang-btn" id="btn-he" onclick="setLang('he')">HE Hebrew</button>
</div>
```

### Translation Object Structure
```javascript
const T = {
  en: {
    hero_title: 'Topic Visual Guide',
    hero_subtitle: 'Description...',
    // ... all keys
    stages: [
      { title: 'Stage Title', html: '<p>Detailed HTML content</p>' },
      // ...
    ]
  },
  he: {
    hero_title: 'Hebrew title',
    hero_subtitle: 'Hebrew description...',
    // ... all keys matching en
    stages: [
      { title: 'Hebrew stage title', html: '<p>Hebrew HTML content</p>' },
      // ...
    ]
  }
};
```

### setLang Function
```javascript
let currentLang = 'en';

function setLang(lang) {
  currentLang = lang;
  const html = document.documentElement;
  html.lang = lang;
  html.dir = lang === 'he' ? 'rtl' : 'ltr';

  document.getElementById('btn-en').classList.toggle('active', lang === 'en');
  document.getElementById('btn-he').classList.toggle('active', lang === 'he');

  document.querySelectorAll('[data-i18n]').forEach(el => {
    const key = el.getAttribute('data-i18n');
    if (T[lang][key]) el.innerHTML = T[lang][key];
  });

  document.querySelectorAll('[data-i18n-arrow]').forEach(el => {
    el.textContent = lang === 'he' ? '<-' : '->';
  });

  // Reset any dynamic text (step info, stage details)
  // to match the current language
}
```

## Design System (MUST follow exactly)

### Colors
```css
--bg-primary: #0f172a;      /* Page background */
--bg-card: #1e293b;         /* Card backgrounds */
--border: #334155;          /* Borders */
--border-hover: #475569;    /* Border hover state */
--text-primary: #e2e8f0;    /* Main text */
--text-secondary: #cbd5e1;  /* Body text */
--text-muted: #94a3b8;      /* Muted/hint text */
--accent-purple: #818cf8;   /* Primary accent */
--accent-violet: #c084fc;   /* Section titles */
--accent-pink: #f472b6;     /* Card titles, highlights */
--accent-indigo: #6366f1;   /* Buttons, active states */
--accent-deep: #4f46e5;     /* Highlights */
--accent-vivid: #7c3aed;    /* Kernel/filter cells */
--accent-bright: #8b5cf6;   /* Button gradients */
--success: #22c55e;         /* Positive indicators */
--error: #ef4444;           /* Error/red indicators */
--info: #3b82f6;            /* Blue indicators */
```

### Button Styles
```css
.btn-primary {
  background: linear-gradient(135deg, #6366f1, #8b5cf6);
  color: #fff;
  padding: 0.7rem 1.5rem;
  border-radius: 10px;
  border: none;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
}
.btn-primary:hover {
  transform: scale(1.05);
  box-shadow: 0 0 20px rgba(99,102,241,0.4);
}
```

### Card Style
```css
.card {
  background: #1e293b;
  border-radius: 16px;
  padding: 2rem;
  margin: 1.5rem 0;
  border: 1px solid #334155;
  box-shadow: 0 4px 24px rgba(0,0,0,0.3);
}
```

### Language Toggle Style
```css
.lang-toggle {
  position: fixed;
  top: 1.2rem;
  right: 1.5rem;
  z-index: 1000;
  display: flex;
  background: rgba(30,41,59,0.9);
  backdrop-filter: blur(12px);
  border-radius: 12px;
  border: 1px solid #334155;
  overflow: hidden;
  box-shadow: 0 4px 20px rgba(0,0,0,0.4);
}
```

## Interactive Demo Guidelines

The interactive demo is the MOST IMPORTANT part of the guide. It should:

1. **Be visual** — Show grids, charts, animations, or step-by-step progressions
2. **Have controls** — Step, Auto Play, Reset buttons (all translated)
3. **Show state changes** — Highlight active elements, show computed values
4. **Be self-explanatory** — A step-info text area explains what's happening at each step

### Demo Pattern
```html
<div class="card">
  <div class="demo" id="demoArea">
    <!-- Visual elements (grids, canvases, SVGs) -->
    <div class="step-info" id="stepInfo" data-i18n="demo_hint">
      Click "Step" to begin!
    </div>
    <div class="conv-controls">
      <button class="btn-primary" onclick="step()" data-i18n="btn_step">Step</button>
      <button class="btn-primary" onclick="autoPlay()" data-i18n="btn_auto">Auto Play</button>
      <button class="btn-secondary" onclick="reset()" data-i18n="btn_reset">Reset</button>
    </div>
  </div>
</div>
```

### Demo State Management
```javascript
let currentStep = 0;
let totalSteps = N;
let isDone = false;
let isAutoPlaying = false;

function step() {
  if (isDone) return;
  // Update visuals for currentStep
  // Update step-info text using T[currentLang]
  currentStep++;
  if (currentStep >= totalSteps) {
    isDone = true;
    document.getElementById('stepInfo').textContent = T[currentLang].demo_done;
  }
}

function autoPlay() {
  if (isAutoPlaying || isDone) return;
  isAutoPlaying = true;
  const interval = setInterval(() => {
    if (isDone) { clearInterval(interval); isAutoPlaying = false; return; }
    step();
  }, 600);
}

function reset() {
  currentStep = 0;
  isDone = false;
  isAutoPlaying = false;
  // Reset all visual elements
  document.getElementById('stepInfo').textContent = T[currentLang].demo_hint;
}
```

## Responsive Breakpoints

```css
@media (max-width: 768px) {
  .hero h1 { font-size: 2.2rem; }
  .analogy-grid { grid-template-columns: 1fr; }
  .demo-row { flex-direction: column; }
  section { padding: 2.5rem 1rem; }
  .lang-toggle { top: 0.8rem; right: 0.8rem; }
  .lang-btn { padding: 0.5rem 0.8rem; font-size: 0.85rem; }
}
```

## Hebrew Translation Quality

When translating to Hebrew:
- Use natural, conversational Hebrew (not formal/academic)
- Technical terms can stay in English (e.g., "ReLU", "Softmax", "CNN")
- Ensure all HTML tags inside translations are preserved
- Arrows flip: English uses `->`, Hebrew uses `<-`
- `pool_arrow`: English "-> MAX ->", Hebrew "<- MAX <-"
- Button text should be concise in both languages
