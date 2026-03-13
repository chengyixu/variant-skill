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
  --bg-body: #222222;           /* rgb(34, 34, 34) — outer body background */
  --bg-page: #070706;          /* rgb(7, 7, 6) — main page/panel background */
  --bg-surface: #1e1e1c;       /* rgb(30, 30, 28) — input bar, elevated panels */
  --bg-deep: #070706;          /* rgb(7, 7, 6) — buttons, cards with content */

  /* Text — warm off-whites, never pure white */
  --text-primary: #f0ede5;          /* rgb(240, 237, 229) — headings, bold text */
  --text-secondary: rgba(240, 237, 229, 0.65);  /* body copy */
  --text-tertiary: rgba(240, 237, 229, 0.5);    /* captions, hints */
  --text-input: rgba(255, 255, 255, 0.85);       /* input fields */

  /* Borders — ultra-subtle */
  --border-subtle: rgba(255, 255, 255, 0.1);    /* 0.5px borders on buttons/cards */
  --border-card-outline: rgba(255, 255, 255, 0.08); /* dashed placeholder cards */

  /* Accents — from CSS variables, use sparingly in widget interiors */
  --accent-blue: #2688f9;       /* --color-primary-blue */
  --accent-blue-alt: #3a86ff;   /* --color-secondary-blue */
  --accent-coral: rgb(248, 113, 113); /* --color-accent-coral */
  --accent-purple: rgba(107, 173, 255, 1); /* --color-accent-purple */
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
- **Widget grid**: Masonry-style mixed card sizes with 10px gap, absolutely positioned via CSS transforms (virtual scrolling)
- **Floating input**: Pinned to bottom of left panel (not viewport-fixed), with `rgb(30, 30, 28)` background and `box-shadow: rgba(255,255,255,0.1) 0 0 0 0.5px` ring

### Card Sizes (Widget Grid)

Cards use varied sizes for visual rhythm:
```
Small:   315 x 236px  (border-radius: 8px)
Medium:  375 x 236px  (border-radius: 8px)
Wide:    513 x 384px  (border-radius: 8px)
Narrow:  177 x 384px  (border-radius: 8px)
Feature: 345 x 259px  (border-radius: 8px)
```

Empty/placeholder cards use a **shimmer dashed border** effect:
```css
.card::after {
  content: '';
  position: absolute;
  inset: 0;
  border-radius: 8px;
  pointer-events: none;
  /* Shimmer gradient that sweeps across the border */
  background-image: linear-gradient(135deg,
    rgba(255,255,255,0.22) 48%,
    rgba(255,255,255,0.55) 50%,
    rgba(255,255,255,0.22) 52%);
  background-size: 6700px 6700px;
  /* Masked to a dashed rounded-rectangle via SVG */
  -webkit-mask-image: url("data:image/svg+xml,...");
  /* SVG uses: stroke-dasharray='2 3' stroke-linecap='round' stroke-width='1' rx='8' ry='8' */
}
```
Active cards: contain interactive iframes or rich content, solid subtle border.

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

Variant showcases 15+ interactive widget demos inside cards. Each is self-contained (iframe with `sandbox="allow-scripts allow-same-origin"`, lazy-loaded). Examples:

- **Poetic Weather**: Photo background (Golden Gate Bridge) + temperature overlay + animated rain drops + city label
- **Music Player**: Circular album art with glow + track info + playback controls + genre/BPM tag
- **Bike Battery**: Vertical bar gauge + percentage + miles left + charge stats + action button
- **Radio Tuner**: Frequency dial (83.5–105.9) + AM/FM toggle + Canvas waveform
- **CRT Display**: Retro scanline monitor with "Loading DOOM..." text, Canvas-based
- **Scribble Pad**: Drawing canvas with colorful strokes + clear button + tool toggles
- **Stickers**: Collection of retro/funky sticker designs with typography badges
- **Card Widget**: Credit/debit card with flip, freeze, add cash actions
- **Robot Widget**: Animated LED-style robot face with emoji reaction buttons
- **Messaging**: Notification list with tabs and message previews
- **Text Editor**: Rich text with B/I/U/List toolbar
- **Video Player**: Media playback widget
- **Voice Recorder**: Audio recording interface

Widget states: shimmer placeholder (loading) → loaded → hidden (offscreen, recycled).

### Animation & Interaction Principles

1. **Infinite virtual scroll**: Right panel uses transform-based positioning with ~60,000px scroll height; tiles are recycled as user scrolls (not traditional DOM flow)
2. **Shimmer borders**: Card outlines use a 135deg gradient (`rgba(255,255,255,0.22)` → `0.55` → `0.22`) masked to a dashed SVG rect, creating a slow-moving light sweep effect
3. **Micro-interactions**: Subtle hover states on buttons (opacity change, not color change)
4. **Canvas animations**: Use HTML5 Canvas for CRT effects, radio waveforms, particle systems
5. **No jarring transitions**: Everything eases smoothly (300-500ms, ease-out)
6. **Ambient motion**: Continuous animations in widgets (rain drops, waveforms, gauges) add life without distraction
7. **Sound design**: Interaction sounds for generate, explore, and error states (`.wav` files preloaded)

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
