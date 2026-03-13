---
name: variant-website
description: Build websites in the visual style of variant.com — ultra-dark, warm minimal, interactive widget showcases with refined typography and subtle borders. Use when the user wants a dark landing page, AI tool homepage, infinite scroll showcase, or any site inspired by variant.com's design language.
---

# Variant Website Design System

Build production-grade websites that capture variant.com's distinctive design language: a warm-dark, ultra-refined aesthetic with interactive widget showcases, subtle borders, and clean typography.

## When to Use

- User asks to build a website "like variant.com" or references the Variant design style
- Dark-mode landing pages for AI tools, creative tools, or SaaS products
- Showcase/portfolio pages with interactive widget grids
- Any request for a warm-dark minimal aesthetic with high production polish

## Design System

### Color Palette

```css
:root {
  /* Backgrounds — warm darks, never pure black */
  --bg-body: #222222;           /* rgb(34, 34, 34) — main background */
  --bg-surface: #1e1e1c;       /* rgb(30, 30, 28) — cards, panels */
  --bg-deep: #070706;          /* rgb(7, 7, 6) — buttons, elevated surfaces */

  /* Text — warm off-whites, never pure white */
  --text-primary: #f0ede5;          /* rgb(240, 237, 229) — headings, bold text */
  --text-secondary: rgba(240, 237, 229, 0.65);  /* body copy */
  --text-tertiary: rgba(240, 237, 229, 0.5);    /* captions, hints */
  --text-input: rgba(255, 255, 255, 0.85);       /* input fields */

  /* Borders — ultra-subtle */
  --border-subtle: rgba(255, 255, 255, 0.1);    /* 0.5px borders on buttons/cards */
  --border-card-outline: rgba(255, 255, 255, 0.08); /* dashed placeholder cards */

  /* Accents — use sparingly, only in widget interiors */
  --accent-blue: #4a9eff;
  --accent-pink: #ff6b9d;
  --accent-green: #4aff8a;
}
```

**Critical rules:**
- NEVER use pure `#000000` or `#ffffff` — always use the warm variants above
- Background colors should feel like "charcoal" not "black"
- Text should feel like "warm cream" not "white"
- Borders at 0.5px width with very low opacity — barely visible

### Typography

```css
/* Primary: system sans-serif stack inspired by Variant's custom fonts */
--font-display: 'Inter', system-ui, -apple-system, sans-serif;
--font-body: 'Inter', system-ui, -apple-system, sans-serif;

/* Headline */
h1 {
  font-size: 32px;
  font-weight: 400;        /* Light weight — NOT bold */
  line-height: 36px;
  letter-spacing: 0.32px;
  color: var(--text-primary);
}

/* Emphasis word in headline: italic */
h1 em, h1 i {
  font-style: italic;
  font-weight: 400;
}

/* Body text */
p {
  font-size: 14px;
  line-height: 24px;
  color: var(--text-secondary);
}

/* Buttons / labels */
.btn-label {
  font-size: 11px;
  color: var(--text-primary);
}
```

**Critical rules:**
- Headlines are light weight (400), never bold
- Use italic for emphasis words within headlines
- Body text is 14px, comfortable line-height
- Small UI elements (buttons, labels) at 11px

### Layout

```
+------------------------------------------------------+
|  logo (SVG, 88x20px, top-left, 24px padding)         |
+-------------------+----------------------------------+
|                   |                                  |
|  HERO TEXT        |  WIDGET GRID                     |
|  (408px)          |  (708px, overflow hidden)        |
|                   |                                  |
|  h1 headline      |  [card] [card] [card]            |
|  p description     |  [card] [wide-card   ]           |
|  p tagline        |  [tall ] [card] [card]           |
|                   |  [card ] [card] [card]           |
|  [btn] [btn]      |                                  |
|                   |                                  |
+-------------------+----------------------------------+
|  [floating input bar, bottom-left, 200px wide]       |
+------------------------------------------------------+
```

- **Two-column CSS Grid**: `grid-template-columns: 408px 1fr` (responsive: stack on mobile)
- **Full viewport height**: `height: 100vh`
- **Widget grid**: Masonry-style mixed card sizes with 6px gap
- **Floating input**: Fixed position, bottom-left, with glassmorphism

### Card Sizes (Widget Grid)

Cards use varied sizes for visual rhythm:
```
Small:   315 x 236px  (border-radius: 8px)
Medium:  375 x 236px  (border-radius: 8px)
Wide:    513 x 384px  (border-radius: 8px)
Narrow:  177 x 384px  (border-radius: 8px)
Feature: 345 x 259px  (border-radius: 8px)
```

Empty/placeholder cards: dashed 0.5px border, no fill.
Active cards: contain interactive iframes or rich content.

### UI Components

**Pill Buttons:**
```css
.btn-pill {
  background: var(--bg-deep);
  color: var(--text-primary);
  border: 0.5px solid var(--border-subtle);
  border-radius: 6px;
  padding: 0 8px;
  font-size: 11px;
  cursor: pointer;
  display: inline-flex;
  align-items: center;
  gap: 6px;
}
```

**Floating Input Bar:**
```css
.input-bar {
  position: fixed;
  bottom: 24px;
  left: 24px;
  width: 200px;
  background: var(--bg-surface);
  border: 0.5px solid var(--border-subtle);
  border-radius: 12px;
  padding: 12px 16px;
  display: flex;
  align-items: center;
  gap: 8px;
}
.input-bar input,
.input-bar [contenteditable] {
  background: transparent;
  border: none;
  color: var(--text-input);
  font-size: 14px;
  flex: 1;
  outline: none;
}
.input-bar .icon-btn {
  color: rgba(255, 255, 255, 0.4);
  cursor: pointer;
  background: none;
  border: none;
  padding: 0;
}
```

**Widget Cards (with interactive content):**
```css
.widget-card {
  background: var(--bg-deep);
  border-radius: 8px;
  overflow: hidden;
  position: relative;
}
.widget-card-empty {
  border: 0.5px dashed var(--border-card-outline);
  border-radius: 8px;
  background: transparent;
}
```

### Interactive Widgets

Variant showcases interactive widget demos inside cards. Typical widget types:
- **Weather widget**: Photo background + temperature overlay + rain drops animation
- **Music player**: Album art + playback controls + waveform
- **Battery/status**: Gauge display + stats + action button
- **Radio tuner**: Frequency dial + AM/FM toggle + waveform canvas
- **CRT display**: Retro monitor with text content + scanlines

Each widget is self-contained (iframe or shadow DOM) with its own internal styling.

### Animation & Interaction Principles

1. **Scroll-driven**: Content reveals on scroll, widgets animate as they enter viewport
2. **Micro-interactions**: Subtle hover states on buttons (opacity change, not color change)
3. **Canvas animations**: Use HTML5 Canvas for waveforms, gauges, particle effects
4. **No jarring transitions**: Everything eases smoothly (300-500ms, ease-out)
5. **Ambient motion**: Subtle continuous animations in widgets (rain, waveforms) add life

### Responsive Behavior

```css
@media (max-width: 1024px) {
  .layout {
    grid-template-columns: 1fr;
    grid-template-rows: auto 1fr;
  }
  .hero { padding: 24px; }
  .widget-grid { height: 60vh; }
}
@media (max-width: 640px) {
  h1 { font-size: 24px; line-height: 28px; }
  .input-bar { width: calc(100% - 48px); }
}
```

## Implementation Checklist

When building a variant.com-style website:

1. [ ] Set `background: #222222` on body — warm charcoal, not pure black
2. [ ] Use `color: #f0ede5` for text — warm off-white, not pure white
3. [ ] Headlines at 400 weight with italic emphasis words
4. [ ] 0.5px borders with `rgba(255,255,255,0.1)` — barely visible
5. [ ] Two-column grid: hero left, showcase right
6. [ ] Mixed-size cards in the showcase grid (not uniform)
7. [ ] Interactive widget content in cards (not just static images)
8. [ ] Floating input bar fixed at bottom-left
9. [ ] SVG logo top-left, minimal
10. [ ] Full viewport height, no traditional scrolling on hero

## Quick Start Template

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Your Product — Tagline</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=Inter:ital,wght@0,400;0,500;1,400&display=swap" rel="stylesheet">
  <style>
    *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

    :root {
      --bg-body: #222222;
      --bg-surface: #1e1e1c;
      --bg-deep: #070706;
      --text-primary: #f0ede5;
      --text-secondary: rgba(240, 237, 229, 0.65);
      --text-tertiary: rgba(240, 237, 229, 0.5);
      --border-subtle: rgba(255, 255, 255, 0.1);
    }

    body {
      font-family: 'Inter', system-ui, sans-serif;
      background: var(--bg-body);
      color: var(--text-primary);
      height: 100vh;
      overflow: hidden;
    }

    .layout {
      display: grid;
      grid-template-columns: 408px 1fr;
      height: 100vh;
    }

    .hero {
      padding: 24px;
      display: flex;
      flex-direction: column;
      justify-content: flex-start;
      gap: 16px;
    }

    .logo svg { width: 88px; height: 20px; fill: var(--text-primary); }

    h1 {
      font-size: 32px;
      font-weight: 400;
      line-height: 36px;
      letter-spacing: 0.32px;
      margin-top: 24px;
    }
    h1 em { font-style: italic; }

    .description {
      font-size: 14px;
      line-height: 24px;
      color: var(--text-secondary);
    }
    .description strong {
      color: var(--text-primary);
      font-weight: 500;
    }

    .actions {
      display: flex;
      gap: 8px;
      margin-top: 8px;
    }
    .btn-pill {
      background: var(--bg-deep);
      color: var(--text-primary);
      border: 0.5px solid var(--border-subtle);
      border-radius: 6px;
      padding: 4px 8px;
      font-size: 11px;
      cursor: pointer;
      display: inline-flex;
      align-items: center;
      gap: 4px;
    }

    .showcase {
      overflow: hidden;
      padding: 6px;
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(170px, 1fr));
      grid-auto-rows: 120px;
      gap: 6px;
    }

    .card {
      border: 0.5px dashed rgba(255, 255, 255, 0.08);
      border-radius: 8px;
      overflow: hidden;
    }
    .card.active {
      background: var(--bg-deep);
      border-style: solid;
      border-color: var(--border-subtle);
    }
    .card.span-2 { grid-column: span 2; }
    .card.tall { grid-row: span 2; }

    .input-bar {
      position: fixed;
      bottom: 24px;
      left: 24px;
      width: 200px;
      background: var(--bg-surface);
      border: 0.5px solid var(--border-subtle);
      border-radius: 12px;
      padding: 10px 14px;
      display: flex;
      align-items: center;
      gap: 8px;
    }
    .input-bar input {
      background: transparent;
      border: none;
      color: rgba(255, 255, 255, 0.85);
      font-size: 14px;
      flex: 1;
      outline: none;
      font-family: inherit;
    }
    .input-bar input::placeholder { color: var(--text-tertiary); }
    .input-bar button {
      background: none;
      border: none;
      color: rgba(255, 255, 255, 0.4);
      cursor: pointer;
      font-size: 16px;
      padding: 0;
    }

    @media (max-width: 1024px) {
      .layout { grid-template-columns: 1fr; }
      .showcase { max-height: 50vh; }
      .input-bar { width: calc(100% - 48px); }
    }
  </style>
</head>
<body>
  <div class="layout">
    <div class="hero">
      <div class="logo">
        <!-- Replace with your SVG logo -->
        <svg viewBox="0 0 88 20"><text x="0" y="16" font-size="16" fill="currentColor" font-family="Inter">your logo</text></svg>
      </div>
      <h1>Your headline here,<br><em>with emphasis.</em></h1>
      <p class="description">Supporting text goes here. <strong>Brand name does this.</strong></p>
      <p class="description">A compelling one-liner about the product experience.</p>
      <div class="actions">
        <button class="btn-pill">Get started</button>
        <button class="btn-pill">Try it</button>
      </div>
    </div>
    <div class="showcase">
      <div class="card active span-2"><!-- Widget content --></div>
      <div class="card"></div>
      <div class="card active tall"><!-- Widget content --></div>
      <div class="card span-2"></div>
      <div class="card"></div>
      <div class="card active span-2"><!-- Widget content --></div>
      <div class="card tall"></div>
      <div class="card"></div>
      <div class="card"></div>
    </div>
  </div>
  <div class="input-bar">
    <button>+</button>
    <input type="text" placeholder="See endless designs for...">
    <button>&#x21B5;</button>
  </div>
</body>
</html>
```

## References

Load the detailed design reference when you need deeper detail:
- [REFERENCE.md](references/REFERENCE.md) — Full extracted design tokens, layout measurements, and component specs

## Source

- Design reference: https://variant.com/
- Extraction method: webskills CLI (html_fallback) + chrome-devtools visual analysis
- Skill methodology: browser-use skills pattern (capture once, reproduce deterministically)
