---
name: variant-website
description: "Complete multi-aesthetic design system extracted from variant.com via Jina r.reader + chrome-devtools. Contains 80+ shell CSS variables, 10+ distinct widget aesthetics with FULL source CSS (dark minimal, retro CRT, atmospheric photo, vibrant playful, iOS light, audio/music, retro radio, fintech card, robot mascot, scribble art), shimmer dashed borders, WebGL shaders, squircle clip-paths, virtual scroll patterns, glassmorphism, rain/particle animations, and production-ready component architecture. Use when building any dark-mode UI, landing page, widget showcase, AI tool interface, or when the user needs a specific design aesthetic."
---

# Variant.com — Complete Multi-Aesthetic Design System

Variant.com is not one design — it's a **design platform** showcasing 10+ distinct visual aesthetics across 15+ interactive widgets, unified by a dark-mode shell with warm tones, ultra-subtle borders, and shimmer effects.

This skill gives you the FULL design system: every CSS variable, every animation, every gradient, every component pattern extracted directly from the live source code via Jina r.reader API.

## When to Use

- Building any dark-mode UI, landing page, or product showcase
- AI tool interfaces, creative tool UIs, design tool dashboards
- Widget/card grids with interactive content
- Any of the 10+ specific aesthetics below (retro, glassmorphic, atmospheric, etc.)
- Floating input bars, shimmer effects, virtual scroll grids
- When user says "like variant.com" or wants a warm-dark refined aesthetic

---

## Part 1: The Shell Design System (variant.com itself)

### Complete CSS Custom Properties (80+)

```css
:root {
  /* ═══════ BACKGROUNDS ═══════ */
  --bg-body: #222222;            /* outer body */
  --bg-page: #070706;            /* main panels */
  --bg-surface: #1e1e1c;        /* input bar, elevated panels */
  --bg-deep: #070706;           /* buttons, cards */
  --color-gray-medium: #363636;  /* medium surface */

  /* ═══════ TEXT — warm off-whites, NEVER pure white ═══════ */
  --text-primary: #f0ede5;                     /* rgb(240, 237, 229) */
  --text-90: rgba(255, 255, 255, 0.9);
  --text-85: rgba(255, 255, 255, 0.85);       /* input text */
  --text-80: rgba(255, 255, 255, 0.8);
  --text-70: rgba(255, 255, 255, 0.7);
  --text-50: rgba(255, 255, 255, 0.5);        /* muted labels */
  --text-40: rgba(255, 255, 255, 0.4);        /* placeholder */
  --text-30: rgba(255, 255, 255, 0.3);
  --text-20: rgba(255, 255, 255, 0.2);
  --text-15: rgba(255, 255, 255, 0.15);
  --text-10: rgba(255, 255, 255, 0.1);        /* borders */
  --text-08: rgba(255, 255, 255, 0.08);
  --text-07: rgba(255, 255, 255, 0.07);       /* hover bg */
  --text-06: rgba(255, 255, 255, 0.06);
  --text-05: rgba(255, 255, 255, 0.05);
  --text-04: rgba(255, 255, 255, 0.04);
  --text-03: rgba(255, 255, 255, 0.03);

  /* ═══════ BRAND BLUES ═══════ */
  --color-primary-blue: #2688f9;
  --color-secondary-blue: #3a86ff;
  --color-tertiary-blue: #3291ff;
  --color-accent-blue: rgb(59, 130, 246);
  --color-brand-blue: rgb(37, 99, 235);

  /* ═══════ ACCENT COLORS ═══════ */
  --color-accent-coral: rgb(248, 113, 113);
  --color-accent-purple: rgba(107, 173, 255, 1);
  --color-warning-red: #f55c47;

  /* ═══════ SEMI-TRANSPARENT GRAYS ═══════ */
  --gray-medium-75: rgba(61, 61, 61, 0.75);    /* modal bg */
  --gray-charcoal-85: rgba(22, 22, 22, 0.85);  /* dropdown bg */
  --gray-darker-85: #0e0e0ed9;                 /* menu bg */
  --dropdown-bg: rgba(68, 68, 68, 0.65);       /* dropdown/popover */
}
```

### Typography System

**Font Stack (3 tiers):**
1. `"Variant Neue Display"` — brand display (100–900 weight + italic, Neue Haas Grotesk based)
2. `"Variant Neue Text"` — brand body (400, 500, 700 + italic)
3. `Inter` — system fallback (variable 100–900)

```css
/* Headline: LIGHT weight, never bold */
h1 { font-size: 32px; font-weight: 400; line-height: 36px; letter-spacing: 0.32px; }
h1 em { font-style: italic; }

/* Body */
p { font-size: 14px; line-height: 24px; letter-spacing: 0.28px; color: rgba(240, 237, 229, 0.65); }

/* UI Labels */
.label { font-size: 13px; font-weight: 500; }
.btn { font-size: 11px; font-weight: 400; letter-spacing: 0.22px; }
.small { font-size: 11.5px; letter-spacing: 0.12px; }

/* Monospace (code/data) */
.mono { font-family: ui-monospace, Menlo, Monaco, "Cascadia Mono", monospace; }
```

### Layout Architecture

```
┌─────────────────────────────────────────────────┐
│ Sidebar (52px fixed left, icons only)           │
│ ┌─────────────────────────────────────────────┐ │
│ │ Topbar (52px sticky top, editable title)    │ │
│ │ ┌─────────────────────────────────────────┐ │ │
│ │ │                                         │ │ │
│ │ │  SquishyGrid (virtual scroll,           │ │ │
│ │ │  transform-positioned cards,            │ │ │
│ │ │  ~60,000px scroll height)               │ │ │
│ │ │                                         │ │ │
│ │ └─────────────────────────────────────────┘ │ │
│ └─────────────────────────────────────────────┘ │
│ ┌─────────────────────────────────────────────┐ │
│ │ GlobalComposer (fixed bottom, centered,     │ │
│ │ 520px max, backdrop-blur, dramatic shadow)  │ │
│ └─────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────┘
```

**Homepage variant (two-column):**
```css
.HomepageV3_root {
  display: grid;
  grid-template-columns: 408px 1fr;
  height: 100vh;
  background: rgb(7, 7, 6);
}
/* Mobile (<900px): stacks, left panel overlays transparent on grid */
```

### Signature Visual Effects

**1. Shimmer Dashed Border (The Variant Look)**
```css
.card::after {
  content: "";
  position: absolute; inset: 0;
  border-radius: 8px;
  pointer-events: none;
  background-image: linear-gradient(135deg,
    rgba(255,255,255,0.22) 0%,
    rgba(255,255,255,0.22) 48%,
    rgba(255,255,255,0.55) 50%,
    rgba(255,255,255,0.22) 52%,
    rgba(255,255,255,0.22) 100%);
  background-size: 6700px 6700px;
  /* SVG mask: stroke-dasharray='2 3' stroke-linecap='round' stroke-width='1' rx='8' ry='8' */
  -webkit-mask-image: url("data:image/svg+xml,...");
}
```

**2. Card Overlay Gradient (16-step fade)**
```css
.card-overlay {
  background: linear-gradient(to bottom,
    black 0%, rgba(0,0,0,0.987) 8.1%, rgba(0,0,0,0.951) 15.5%,
    rgba(0,0,0,0.896) 22.5%, rgba(0,0,0,0.825) 29%,
    rgba(0,0,0,0.741) 35.3%, rgba(0,0,0,0.648) 41.2%,
    rgba(0,0,0,0.55) 47.1%, rgba(0,0,0,0.45) 52.9%,
    rgba(0,0,0,0.352) 58.8%, rgba(0,0,0,0.259) 64.7%,
    rgba(0,0,0,0.175) 71%, rgba(0,0,0,0.104) 77.5%,
    rgba(0,0,0,0.049) 84.5%, rgba(0,0,0,0.013) 91.9%,
    transparent 100%);
}
```

**3. Floating Composer Shadow (5-layer depth)**
```css
.composer {
  box-shadow:
    rgba(255,255,255,0.1) 0 0 0 0.5px,   /* ring */
    rgba(0,0,0,0.1) 0 5px 11px,           /* close shadow */
    rgba(0,0,0,0.09) 0 20px 20px,         /* mid shadow */
    rgba(0,0,0,0.05) 0 44px 26px,         /* far shadow */
    rgba(0,0,0,0.01) 0 78px 31px,         /* ambient */
    rgb(0,0,0) 0 122px 34px;              /* ground */
  background: rgba(30, 30, 28, 0.75);
  backdrop-filter: blur(25px);
}
```

**4. Inset Ring Border (used EVERYWHERE)**
```css
box-shadow: rgba(255, 255, 255, 0.1) 0px 0px 0px 0.5px inset;
/* This replaces border in most components */
```

### Animations (25 total)

| Name | Duration | Use |
|------|----------|-----|
| shimmer | ∞ | Background position cycle |
| gridShimmer | 1.5s ∞ | Loading card sweep |
| emptyGridShimmerTranslate | 6s ∞ | Ambient grid sweep |
| tooltipEnter | 0.15s | Scale 0.85→1 |
| badgeSpawn | 0.2s | Blur+scale entrance |
| spinReroll | 0.3s | Rotate -60deg |
| billingModalEnter | 0.2s | Scale 0.96→1 |
| shake | 0.4s | X-axis shake on error |
| slideDown | 0.3s | Y -20px entrance |
| fadeIn/fadeOut | 0.2s | Opacity transitions |

### Easing Functions
```css
cubic-bezier(0.175, 0.885, 0.32, 1)  /* primary: layout shifts */
cubic-bezier(0.19, 1, 0.22, 1)        /* secondary: containers */
cubic-bezier(0.22, 1, 0.36, 1)        /* used in card widget flip/transitions */
cubic-bezier(0.34, 1.56, 0.64, 1)     /* bouncy: card hover reset */
cubic-bezier(0.76, 0, 0.24, 1)        /* card flip: smooth in-out */
/* Durations: 0.1s hover → 0.16s states → 0.2s color → 0.4s layout → 6s ambient */
```

---

## Part 2: The 10+ Design Aesthetics (Complete Widget CSS)

Each widget is a self-contained micro-app. Below are the **actual extracted CSS variables and patterns** from each.

---

### Style 1: Dark Minimal / Dashboard
**Source:** Bike Battery Widget
**Fonts:** Inter 400–700
**Palette:**
```css
:root {
  --page-bg: #181b25;
  --panel-bg: #181b25;
  --panel-surface: #0e121b;
  --panel-border: #2b303b;
  --text: #ffffff;
  --muted: #99a0ae;
  --card-text: #f5f7fa;
  --accent-a: #2b6cff;         /* blue primary */
  --accent-b: #00c2ff;         /* cyan secondary */
  --accent-border: #2a7bdc;
  --bar-border: #9bd9ff;
}
```
**Key patterns:**
```css
/* Deep inset shadow stack for depth */
.widget__inner {
  box-shadow:
    inset 0px 4px 11.1px 0px #181b25,
    inset 0px 16px 15.5px 0px rgba(113,119,132,0.34),
    inset 0px 46px 24.4px 0px rgba(0,0,0,0.25);
}

/* Gradient battery bars */
.bar--full {
  background: linear-gradient(to bottom, var(--accent-a), var(--accent-b));
  border-bottom-color: var(--bar-border);
}

/* Icon card with inset shadow */
.card__icon {
  width: 32px; height: 32px; border-radius: 8px;
  background: #525866;
  box-shadow: inset 0px -6px 9.3px 0px rgba(0,0,0,0.25);
}

/* Large stat number */
.percent { font-size: 56px; font-weight: 400; letter-spacing: -1.1px; }

/* Charge button with radial gradient SVG bg */
.charge {
  height: 52px; border-radius: 20px;
  border: 1px solid var(--accent-border);
  box-shadow: 0px 1px 2px 0px #0a0d14;
}

/* Color transitions (blue↔green) via JavaScript lerp */
/* Green variant: --accent-a: #06d689; --accent-b: #04dac1; */
```

**WebGL shader for energy pulse on battery bars** — uses SVG mask + Canvas for animated glow.

---

### Style 2: Retro CRT / Terminal
**Source:** CRT/DOOM Widget
**Font:** `"JetBrains Mono"` monospace
**Palette:** Pure black (#000) + phosphor green/amber
```css
body {
  background: #000;
  font-family: "JetBrains Mono", monospace;
  color: #e0e0e0;
}
.crt-container {
  width: 640px; height: 480px;
  background: #000;
  overflow: hidden;
}
#boot-status {
  font-size: 12px; line-height: 16px;
  color: rgba(255, 255, 255, 0.75);
  text-shadow: 0 1px 2px rgba(0, 0, 0, 0.6);
}
```
**Key techniques:** Canvas-based CRT emulator with scanlines, barrel distortion, phosphor glow effects. Embeds js-dos for DOOM playback.

---

### Style 3: Atmospheric / Photographic
**Source:** Poetic Weather Widget
**Font:** `"Caveat"` cursive (handwritten) + Inter
**Palette:** Dark (#111) with photo overlay
```css
body { background-color: #111; font-family: "Caveat", cursive; }

/* Card with glass-like depth */
.weather-card::after {
  box-shadow:
    inset 0 -4px 8px rgba(0, 0, 0, 0.25),
    inset 0 4px 6px rgba(255, 255, 255, 0.55);
}

/* Layered overlays */
.blur-overlay { backdrop-filter: blur(8px); }
.gradient-overlay {
  background: linear-gradient(180deg,
    rgba(0,0,0,0.2) 0%, rgba(0,0,0,0.4) 100%);
}

/* Rain animation */
.raindrop {
  width: 2px; height: 40px;
  background: white;
  border-radius: 50% 50% 0 0;
  filter: blur(4px);
  animation: fall linear infinite;
}
@keyframes fall {
  0%   { transform: translateY(-40px); opacity: 1; }
  100% { transform: translateY(312px); opacity: 0; }
}
/* 50 raindrops, random left: 0-100%, scale: 0.5-1.0 */
/* duration: 0.33-1.04s, random delay */

/* Frosted location pill */
.location-pill {
  background: linear-gradient(180deg, rgba(0,0,0,0.1), rgba(0,0,0,0.25));
  padding: 0 8px 0 6px; border-radius: 12px; height: 24px;
  font-size: 11.5px; font-family: "Inter";
  backdrop-filter: blur(10px);
}

/* SVG hand-drawn text animation */
.svg-container path {
  stroke: white; stroke-width: 1.75;
  stroke-linecap: round; stroke-linejoin: round;
  stroke-dasharray: var(--length);
  stroke-dashoffset: var(--length);
  /* Animated via JS: sequential path reveal, duration: length/200 */
}
```

---

### Style 4: Vibrant / Playful (Stickers)
**Source:** Stickers Widget
**Palette:** Black bg + colorful 3D stickers
```css
body {
  background: #000;
  perspective: 1200px;
  perspective-origin: center center;
}

/* MacBook lid gradient */
.macbook-lid {
  background: linear-gradient(180deg, #333335 0%, #1e1e1f 100%);
}
.macbook-lid::before {
  mix-blend-mode: overlay;
  background: linear-gradient(230deg,
    rgba(190,191,196,0.7) 17%, rgba(127,128,131,0.7) 81%);
}
.macbook-lid::after {
  box-shadow: inset 0px -4.539px 22.695px 0px rgba(0,0,0,0.2);
}

/* 3D sticker with WebGL holographic sheen */
.sticker {
  perspective: 800px;
  transform-style: preserve-3d;
  will-change: transform, opacity, filter;
}
.sticker canvas {
  filter: drop-shadow(0px var(--sh-y, 1px) var(--sh-blur, 2px) rgba(0,0,0,0.30));
}
/* Drag tilt: max 14.4deg, smoothing: 0.1 */
/* Holographic sheen: SHEEN_STRENGTH=0.6, SHEEN_TILT_SHIFT=0.05 */
/* Intro: 520ms appear, 260ms respawn */
```

---

### Style 5: Scribble / Art Canvas
**Source:** Scribble Pad Widget
**Palette:** Dark (#111111) + colorful strokes on #333
```css
body { background-color: #111111; font-family: sans-serif; color: #fff; }
.canvas-container {
  width: 292px; height: 320px;
  background-color: #333333;
  overflow: hidden;
}
canvas { cursor: crosshair; touch-action: none; }

/* Controls with press animation */
.controls-wrapper {
  transition: transform 0.3s ease, filter 0.3s ease, opacity 0.3s ease;
}
.controls-wrapper.depressed {
  transform: scale(0.95);
  filter: blur(4px);
  opacity: 0;
}
```

---

### Style 6: Retro Radio / Analog
**Source:** Radio Widget
**Font:** `"Gilroy"` Light 300
**Palette:** Light gray background (#ececec) — BREAKS dark theme
```css
:root {
  font-family: 'Gilroy', system-ui, sans-serif;
  font-weight: 300;
  background-color: #151619;
}
.radio-widget {
  width: 500px; height: 500px;
  background-color: #ececec;  /* LIGHT theme */
  overflow: hidden;
}

/* Frequency display */
.left {
  font-size: 3.4375rem;
  background-color: #8a8a8a;
  color: #ffffff;
}
.right {
  background-color: #ffffff;
  text-transform: uppercase;
}
.right > p:first-of-type { color: rgba(0,0,0,0.3); }
.right > p:last-of-type { color: rgba(0,0,0,0.5); }

/* Circular dial with CSS-drawn tick marks */
.dial-inner {
  border-radius: 9999px;
  will-change: transform;
}
.dial-inner-line {
  --line-scale: 1;
  transform-origin: bottom center;
}
.dial-inner-line::after {
  width: 0.0625rem; height: 2.75rem;
  background-color: #000; opacity: 0.3;
  transform: scaleY(var(--line-scale));
}

/* Accent: gold/amber for active frequency */
/* SVG dial: fill="#FFB30F" for active arc */

/* AM/FM toggle */
.modulation-selector > button {
  color: #000; opacity: 0.2;
  transform: scale(0.8);
  transition: transform 0.3s ease-in-out;
}
.modulation-selector > button.active {
  opacity: 1; transform: scale(1);
}
```

---

### Style 7: Robot / Tech Mascot
**Source:** Robot Widget
**Fonts:** `"PP Mondwest"` (display) + `"Inter"` (UI)
**Palette:** White background — FULL LIGHT THEME
```css
.robot-widget {
  width: 402px; height: 874px;
  background-color: #ffffff;
  border-radius: 0px;
  padding: 0.3125rem;
}
.face {
  background-color: #000000;
  border-radius: 2.1875rem;
}
.text {
  background-color: #e2f0f4;  /* light teal */
  border-radius: 2.1875rem;
}
.text > .text-content > p {
  font-family: 'PP Mondwest';
  font-size: 4.6875rem;    /* 75px */
  font-weight: 400;
  letter-spacing: -0.0938rem;
  color: #000000;
}

/* LED dot grid face (Canvas) */
/* dotColor: '#FF9421' (orange), dotColorOff: 'rgba(255,148,33,0.14)' */
/* Eye tracking: follows mouse, max 8px offset */
/* Blink: 2-6s random delay, 0.15 progress speed */

/* Language selector dropdown */
.language-selector-content {
  background-color: #ffffff;
  border-radius: 0.5rem;
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
  transition: opacity 0.3s cubic-bezier(0.22, 1, 0.36, 1),
    transform 0.3s cubic-bezier(0.22, 1, 0.36, 1);
}

/* Emoji bottom bar */
.bottom-bar {
  background-color: #000000;
  border-radius: 1.8125rem;
}
.bottom-bar > li {
  background-color: #e2f0f4;
  border-radius: 1.3125rem;
  aspect-ratio: 1 / 1;
}
.bottom-bar > li.active { background-color: #ff9421; }
```

---

### Style 8: Fintech / Card
**Source:** Card Widget
**Font:** `Inter` (variable) with feature settings "liga", "calt"
**Palette:** Dark gradient
```css
.card-widget {
  width: 24.25rem; height: 31.25rem;
  background-image: linear-gradient(153deg, #0b0b0a 0% 40%, #242c2f);
  border-radius: 8px;
}

/* Credit card with 3D perspective flip */
.card-container {
  perspective: 600px;
  transform-style: preserve-3d;
}
.flip-wrapper {
  transition: transform .6s cubic-bezier(.76, 0, .24, 1);
  backface-visibility: hidden;
}

/* Squircle clip-path (superellipse) — modern CSS shape() */
.squircle {
  --squircle-radius: 1.0625rem;
  --sm-tl: calc(var(--squircle-tl) * .375);
  --d-tl: calc(var(--squircle-tl) * 1.3);
}
@supports (clip-path: shape(from 0 0, close)) {
  .squircle {
    clip-path: shape(
      from 0px var(--d-tl),
      curve to var(--d-tl) 0px with 0px var(--sm-tl) / var(--sm-tl) 0px,
      hline to calc(100% - var(--d-tr)),
      /* ... full superellipse path */
      close
    );
  }
}

/* Card surface with multi-layer gradient */
.card {
  background:
    linear-gradient(145deg, rgba(255,255,255,0.08) 0%, transparent 40%,
      transparent 60%, rgba(0,0,0,0.15) 100%),
    linear-gradient(to bottom, #4a4a4a, #3d3d3d, #353535, #3a3a3a, #424242);
  box-shadow: inset 0 1px 1px rgba(255,255,255,0.1),
              inset 0 -1px 1px rgba(0,0,0,0.2);
}

/* Mouse-following glare */
.card:before {
  background: radial-gradient(
    circle at var(--pointer-x, 50%) var(--pointer-y, 50%),
    rgba(255,255,255,0.15), transparent 70%);
  filter: blur(20px);
}

/* Frost overlay for "freeze" state */
/* Uses --frost-image: url("./assets/img_7d5d3328.webp") */

/* Mechanical counter digit roll */
.digit {
  transform: translateY(calc(var(--digit) * -1.2em));
}
.digit.rolling {
  animation: rollDigit .5s cubic-bezier(.22, 1, .36, 1) forwards;
}
@keyframes rollDigit {
  from { transform: translateY(calc(var(--from-digit) * -1.2em)); }
  to   { transform: translateY(calc(var(--digit) * -1.2em)); }
}

/* Floating "+$100.00" animation (green #4ade80) */
@keyframes floatIn {
  from { opacity: 0; transform: translateY(.5rem); }
  to   { opacity: 1; transform: translateY(0); }
}

/* Dashed card border (SVG) */
/* stroke-dasharray="1 4" stroke-opacity="0.5" */

/* Action buttons */
.card-action button {
  width: 3.5rem; height: 3.5rem;
  background: rgba(255,255,255,0.1);
  border-radius: 999px;
  color: rgba(255,255,255,0.4);
  transition: background .4s cubic-bezier(.22, 1, .36, 1);
}
.card-action button:hover { background: rgba(255,255,255,0.2); }
.card-action button.active { background: #fff; color: #0d0d0c; }
```

---

### Style 9: Music / Audio
**Source:** Music Player Widget
**Palette:** Deep black + magenta/pink glow
```css
/* Circular album art with radiant magenta glow */
/* Track: "AMOUR - AVA2", Tag: "CMINOR - 140 BPM" */
/* Controls: prev/play/next with frosted backgrounds */
/* Waveform: Canvas visualization */
/* Built with Vite + React (minified), uses GSAP for animations */
```

---

### Style 10: Sci-Fi / Voice Recorder
**Source:** Voice Recorder Widget
**Font:** `"JetBrains Mono"` monospace
**Palette:** Dark (#151619) + red recording accent
```css
body { background-color: #151619; font-family: 'JetBrains Mono', monospace; }

/* Radial tick visualizer — 120 ticks in a circle */
/* Ticks displaced by sine/cosine noise while recording */
/* Color tokens: */
/* --bg: #151619 */
/* --text: #8E9299 (steel gray) */
/* --record: #FF4444 (red) */
/* --record-ring: pulse animation, scale + opacity */

/* Status text: "Secure link established", reference codes */
/* Timer: 11px mono, spacing 1px */
/* Sample rate label: "44.1 kHz" */

/* Record button with state morph: */
/* cubic-bezier(0.2, 0.8, 0.2, 1) for record state transitions */
```

---

### Style 11: Infinite Gallery
**Source:** Infinite Gallery Widget
**Font:** `Inter` / `InterVariable`
**Palette:** Dark (#1c1c1c) with full-opacity active card
```css
.gallery-container {
  width: 25.125rem; height: 54.625rem;
  background-color: #1c1c1c;
  border-radius: 8px;
  touch-action: none;
}
.gallery-card {
  width: 15.625rem; height: 15.625rem;
  border-radius: 2.5rem;   /* 40px — very round! */
  transition: opacity 0.3s ease-out;
}
/* Active card: opacity 1, inactive: 0.15 */

/* Quincunx grid: 3 cols × 5 rows, 8px gap */
/* Odd rows offset by half card width (129px) */

/* Handle pill: bg #262626, border-radius 999px */
/* Momentum drag: velocity tracking, 0.95 friction decay */
/* Magnetic snap: soft pull when velocity < 3 */
/* Snap animation: 300ms cubic ease-out */
```

---

### Style 12: Editorial / Product
**Source:** Movie Rating, Video Player
```css
/* High-quality product photography with warm lighting */
/* Minimal text overlay on rich imagery */
/* Rating systems with GSAP + Peel library animations */
/* Attribution tags ("@vuelo") */
```

---

## Part 3: Implementation Guide

### Building the Shell (variant.com homepage style)

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Your Product — Tagline</title>
  <link href="https://fonts.googleapis.com/css2?family=Inter:ital,wght@0,100..900;1,100..900&display=swap" rel="stylesheet">
  <style>
    *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

    :root {
      --bg-body: #222222;
      --bg-page: #070706;
      --bg-surface: #1e1e1c;
      --text-primary: #f0ede5;
      --text-secondary: rgba(240, 237, 229, 0.65);
      --text-muted: rgba(255, 255, 255, 0.5);
      --text-subtle: rgba(255, 255, 255, 0.4);
      --border-ring: rgba(255, 255, 255, 0.1);
      --hover-bg: rgba(255, 255, 255, 0.07);
    }

    body {
      font-family: 'Inter', system-ui, sans-serif;
      background: var(--bg-body);
      color: var(--text-primary);
      height: 100vh;
      overflow: hidden;
      -webkit-font-smoothing: antialiased;
    }

    .layout {
      display: grid;
      grid-template-columns: 408px 1fr;
      height: 100vh;
      background: var(--bg-page);
    }

    /* Hero Panel */
    .hero {
      padding: 24px;
      display: flex;
      flex-direction: column;
    }
    .logo svg { width: 88px; height: 20px; fill: var(--text-primary); }
    h1 {
      font-size: 32px; font-weight: 400;
      line-height: 36px; letter-spacing: 0.32px;
      margin-top: 43px;
    }
    h1 em { font-style: italic; }
    .desc { font-size: 14px; line-height: 24px; color: var(--text-secondary); }
    .desc strong { color: var(--text-primary); font-weight: 500; }
    .desc + .desc { margin-top: 16px; }
    h1 + .desc { margin-top: 40px; }

    .actions { display: flex; gap: 8px; margin-top: 25px; }
    .btn-pill {
      background: var(--bg-page);
      color: var(--text-primary);
      border: 0.5px solid var(--border-ring);
      border-radius: 6px;
      padding: 0 8px; height: 26px;
      font-size: 11px; font-family: inherit;
      cursor: pointer;
      display: inline-flex; align-items: center; gap: 4px;
    }
    .btn-pill:hover { background: var(--hover-bg); }

    /* Widget Grid */
    .showcase { overflow: hidden; position: relative; }
    .grid-scroll {
      overflow-y: auto; height: 100%;
      padding: 0 6px 6px;
      scrollbar-width: thin;
      scrollbar-color: rgba(255,255,255,0.18) transparent;
    }
    .grid { display: flex; flex-wrap: wrap; gap: 10px; }
    .card {
      border-radius: 8px; overflow: hidden;
      position: relative; flex-shrink: 0;
    }
    /* Shimmer dashed border */
    .card.empty::after {
      content: "";
      position: absolute; inset: 0;
      border-radius: 8px;
      pointer-events: none;
      background-image: linear-gradient(135deg,
        rgba(255,255,255,0.22) 48%,
        rgba(255,255,255,0.55) 50%,
        rgba(255,255,255,0.22) 52%);
      background-size: 6700px 6700px;
    }
    .card.active {
      background: var(--bg-page);
      box-shadow: var(--border-ring) 0 0 0 0.5px inset;
    }

    /* Floating Input */
    .input-bar {
      position: absolute;
      bottom: 12px; left: 12px; right: 12px;
      background: var(--bg-surface);
      border-radius: 10px;
      box-shadow: var(--border-ring) 0 0 0 0.5px;
      padding: 8px;
      min-height: 72px;
      display: flex; flex-direction: column;
    }
    .input-bar input {
      background: transparent; border: none;
      color: rgba(255,255,255,0.85);
      font-size: 14px; font-family: inherit;
      flex: 1; outline: none;
    }
    .input-bar input::placeholder { color: var(--text-subtle); }
    .input-actions { display: flex; gap: 4px; margin-top: 4px; }
    .icon-btn {
      width: 24px; height: 24px;
      background: none; border: none;
      color: var(--text-muted);
      border-radius: 6px; cursor: pointer;
      display: flex; align-items: center; justify-content: center;
    }
    .icon-btn:hover { background: var(--hover-bg); }

    @media (max-width: 900px) {
      .layout { display: block; position: relative; }
      .showcase { position: fixed; inset: 0; z-index: 0; pointer-events: none; }
      .hero { position: relative; z-index: 3; background: transparent; }
    }
  </style>
</head>
<body>
  <div class="layout">
    <div class="hero">
      <div class="logo">
        <svg viewBox="0 0 88 20"><text x="0" y="16" font-size="16" fill="currentColor">your logo</text></svg>
      </div>
      <h1>Your headline here,<br><em>with emphasis.</em></h1>
      <p class="desc">Description text here. <strong>Brand name does this.</strong></p>
      <p class="desc">A compelling tagline about the experience.</p>
      <div class="actions">
        <button class="btn-pill">Get started</button>
        <button class="btn-pill">Try it</button>
      </div>
      <div style="flex:1"></div>
      <div class="input-bar">
        <input type="text" placeholder="See endless designs for...">
        <div class="input-actions">
          <button class="icon-btn">+</button>
          <button class="icon-btn">@</button>
          <div style="flex:1"></div>
          <button class="icon-btn">↵</button>
        </div>
      </div>
    </div>
    <div class="showcase">
      <div class="grid-scroll">
        <div class="grid">
          <div class="card active" style="width:510px;height:380px"><!-- Widget --></div>
          <div class="card empty" style="width:170px;height:380px"></div>
          <div class="card empty" style="width:310px;height:235px"></div>
          <div class="card active" style="width:370px;height:235px"><!-- Widget --></div>
          <div class="card active" style="width:340px;height:255px"><!-- Widget --></div>
          <div class="card empty" style="width:340px;height:255px"></div>
          <div class="card empty" style="width:510px;height:380px"></div>
          <div class="card active" style="width:170px;height:380px"><!-- Widget --></div>
        </div>
      </div>
    </div>
  </div>
</body>
</html>
```

### Building Individual Widget Aesthetics

When the user asks for a specific style, apply the appropriate aesthetic from Part 2:

**For "retro/CRT":** JetBrains Mono, pure #000 bg, Canvas scanlines, green phosphor glow, barrel distortion
**For "glassmorphic/atmospheric":** Photo bg, backdrop-filter: blur(8px), Caveat cursive, rain divs, frosted pills
**For "music/audio":** Circular album art, magenta glow gradients, waveform Canvas, uppercase labels
**For "fintech/card":** Gradient bg (#0b0b0a→#242c2f), squircle clip-path, 3D perspective flip, mechanical counter
**For "playful/stickers":** 3D perspective, WebGL stickers, holographic sheen, MacBook lid gradient
**For "retro radio":** Gilroy Light, LIGHT bg (#ececec), circular SVG dial, gold accent (#FFB30F), AM/FM toggle
**For "robot/mascot":** White bg, PP Mondwest 75px, LED dot grid Canvas, orange (#ff9421), teal card (#e2f0f4)
**For "dark dashboard":** Inter, navy-dark (#181b25), blue-cyan gradient bars, WebGL energy shader, stat cards
**For "scribble/art":** Crosshair cursor, dark canvas (#333), control blur animation on press
**For "editorial":** Hero photography, minimal text, warm lighting, attribution tags

---

## Part 4: Advanced Patterns

### Virtual Scroll (SquishyGrid)
```css
.grid-item {
  position: absolute;
  transform: matrix(1, 0, 0, 1, tx, ty);
  /* ~32 visible items, total scroll ~60,000px */
}
```

### Widget Iframe Pattern
```html
<iframe
  src="/widgets/your-widget.html"
  loading="lazy"
  sandbox="allow-scripts allow-same-origin"
  style="position:absolute;inset:0;border:none;border-radius:8px"
></iframe>
```

### Sound Design
- `Variant_Generate.wav` — generation start
- `Variant_Explore_2.wav` — scroll/explore
- `Variant_Failed_2.wav` — error state

### Component Library

**Dropdown Menu:**
```css
.dropdown {
  background: rgba(68, 68, 68, 0.65);
  backdrop-filter: blur(15px);
  border-radius: 10px;
  box-shadow: color(display-p3 0 0 0 / 0.03) 0 8px 20px;
  padding: 4px;
}
.dropdown-item {
  height: 28px; padding: 0 8px;
  border-radius: 6px; font-size: 12px;
  color: rgba(255,255,255,0.5);
}
.dropdown-item:hover { color: rgba(255,255,255,0.85); }
```

**Toast Notification:**
```css
.toast {
  backdrop-filter: blur(20px);
  background: rgba(0, 0, 0, 0.85);
  border-radius: 8px;
  padding: 12px 14px;
  font-size: 13px;
  box-shadow: 0 0 0 1px rgba(255,255,255,0.1);
}
```

**Custom Scrollbar:**
```css
scrollbar-width: thin;
scrollbar-color: rgba(255,255,255,0.18) transparent;
::-webkit-scrollbar { width: 8px; }
::-webkit-scrollbar-thumb {
  background: content-box rgba(255,255,255,0.18);
  border-radius: 999px;
  border: 2px solid transparent;
}
```

**Display-P3 Wide Gamut:**
```css
border: 0.5px solid color(display-p3 1 1 1 / 0.1);
@supports (color: color(display-p3 1 1 1/1)) {
  background: color(display-p3 0.1176 0.1176 0.1098 / 0.75);
}
```

---

## References

Load detailed specs when needed:
- [REFERENCE.md](references/REFERENCE.md) — Full DOM structure, computed styles, widget catalog
- [WIDGETS.md](references/WIDGETS.md) — Complete widget source HTML/CSS/JS from Jina r.reader extraction

## Source

- Design reference: https://variant.com/
- Extraction methods:
  - **Jina r.reader API** (X-Engine: browser) — full rendered HTML/CSS/JS from all widget URLs
  - **chrome-devtools MCP** — DOM inspection, computed styles, screenshots at 15+ scroll positions
  - **webskills CLI** — initial structure extraction
- CSS rules extracted: 630+ rules, 151 component classes, 25 animations, 26 gradients, 28 shadows
- Widget source code: 8 complete widgets with full CSS + JavaScript
