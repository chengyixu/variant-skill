# Variant.com Interactive Widget Design System -- Deep Analysis

Comprehensive extraction and analysis of 14 interactive homepage widgets from variant.com.
Each widget is embedded as an iframe and represents a distinct design approach.

---

## Table of Contents

1. [CRT Emulator](#1-crt-emulator)
2. [Poetic Weather](#2-poetic-weather)
3. [Bike Battery](#3-bike-battery)
4. [Radio Widget](#4-radio-widget)
5. [Music Player](#5-music-player)
6. [Scribble Pad](#6-scribble-pad)
7. [Stickers](#7-stickers)
8. [Card Widget](#8-card-widget)
9. [Text Editor Widget](#9-text-editor-widget)
10. [Robot Widget](#10-robot-widget)
11. [Movie Rating App](#11-movie-rating-app)
12. [Video Player](#12-video-player)
13. [Voice Recorder](#13-voice-recorder)
14. [Infinite Gallery](#14-infinite-gallery)
15. [Cross-Widget Design Patterns](#15-cross-widget-design-patterns)
16. [Master Color Palette](#16-master-color-palette)
17. [Master Typography System](#17-master-typography-system)
18. [Animation Technique Catalog](#18-animation-technique-catalog)

---

## 1. CRT Emulator

**Style Category:** Retro / Skeuomorphic / Hardware Emulation

### Visual Concept
A physics-based CRT monitor emulator running a DOOM WASM build (PrBoom+). Renders through WebGL with scanline generation, phosphor decay simulation, and beam spread calculations.

### Color Palette
| Token | Value | Usage |
|-------|-------|-------|
| Background | `#000` (pure black) | CRT bezel / page background |
| Text | `#e0e0e0` | UI text, light gray |

### Typography
- **Primary Font:** `JetBrains Mono` (monospace)
- Weight: Regular
- Used for all UI elements -- reinforces terminal/retro aesthetic

### Technical Implementation
- **Canvas Size:** Fixed 640x480 with responsive scaling
- **Scaling Formula:** `Math.max(0.1, Math.min(vw / BASE_W, vh / BASE_H))`
- **Rendering:** WebGL with custom vertex/fragment shaders
- **border-radius:** `0px` (sharp corners, deliberate)
- **overflow:** `hidden`

### WebGL Shader Details
Fragment shader implements "unified beam physics":
- `beamSpread: 2.0` -- Gaussian beam profile width
- `persistence: 1.0` -- phosphor decay time constant
- `phosphorScale: 720` -- phosphor excitation grid resolution
- Calculates phosphor excitation via Gaussian beam profiles
- Applies exponential decay functions for persistence effect

### Audio Processing Chain
Custom Web Audio API pipeline:
1. Biquad highpass filter
2. Biquad lowpass filter
3. Biquad peaking filter
4. Waveshaper distortion node
5. Noise/hum oscillators for CRT ambiance

### Animation Techniques
- WebGL render loop via `requestAnimationFrame`
- Scanline generation per-frame
- Phosphor decay simulation (temporal)
- No CSS animations -- all GPU-driven

---

## 2. Poetic Weather

**Style Category:** Glassmorphic / Editorial / Atmospheric

### Visual Concept
A compact weather card (252x310px) showing San Francisco weather with rain animation, blurred background image, gradient overlays, and SVG stroke-draw animation.

### Color Palette
| Token | Value | Usage |
|-------|-------|-------|
| Page Background | `#111` | Dark backdrop |
| Card Overlay Gradient Top | `rgba(0, 0, 0, 0.2)` | Gradient start |
| Card Overlay Gradient Bottom | `rgba(0, 0, 0, 0.4)` | Gradient end |
| Location Pill BG Top | `rgba(0, 0, 0, 0.1)` | Pill gradient start |
| Location Pill BG Bottom | `rgba(0, 0, 0, 0.25)` | Pill gradient end |
| Text | `white` (#ffffff) | All text elements |
| Text Opacity | `0.75` | Secondary text |
| Raindrop | `white` | Rain particles |

### Typography
- **Display Font:** `"Caveat"`, cursive (Google Fonts)
- **UI Font:** `"Inter"`, sans-serif (Google Fonts)
- Location pill: Inter, 11.5px, weight 400
- Body: Caveat for handwritten feel

### CSS Design Tokens
```css
.weather-card {
    width: 252px;
    height: 310px;
    overflow: hidden;
    z-index: 1;
}
/* Inset shadow for depth: */
box-shadow: inset 0 -4px 8px rgba(0, 0, 0, 0.25),
            inset 0 4px 6px rgba(255, 255, 255, 0.55);
/* Glassmorphism: */
backdrop-filter: blur(8px);
-webkit-backdrop-filter: blur(8px);
/* Location pill blur: */
backdrop-filter: blur(10px);
```

### Gradient Definitions
1. **Content overlay:** `linear-gradient(180deg, rgba(0,0,0,0.2) 0%, rgba(0,0,0,0.4) 100%)`
2. **Location pill:** `linear-gradient(180deg, rgba(0,0,0,0.1) 0%, rgba(0,0,0,0.25) 100%)`

### Animation Techniques
1. **Rain Animation (`@keyframes fall`):**
   - 50 procedurally-generated raindrops
   - Each raindrop: `width: 2px; height: 40px; filter: blur(4px)`
   - Duration: random 0.33s to 1.04s
   - Scale variation: 0.5 to 1.0
   - Negative animation-delay for staggered starts
   - `translateY(-40px)` to `translateY(312px)` with opacity fade

2. **SVG Stroke Draw Animation:**
   - Uses `stroke-dasharray` / `stroke-dashoffset` technique
   - Sequential path animation via `animateSequentially()`
   - Duration calculated: `Math.min(Math.max(length / 200, 0.3), 1.5) / 3`
   - Easing: `ease-out`
   - Web Animations API (`element.animate()`) with `fill: "forwards"`

### Border Radius
- Location pill: `12px`
- Raindrop top: `50% 50% 0 0` (teardrop shape)

---

## 3. Bike Battery

**Style Category:** Dark Dashboard / Data-Driven UI / Futuristic

### Visual Concept
An electric bike battery dashboard with 20 animated bars, percentage/miles display, stat cards, and a charging button with WebGL energy shader effect.

### Color Palette -- CSS Custom Properties
| Token | Variable | Value | Usage |
|-------|----------|-------|-------|
| Page BG | `--page-bg` | `#181b25` | Overall background |
| Panel BG | `--panel-bg` | `#181b25` | Widget background |
| Panel Surface | `--panel-surface` | `#0e121b` | Card/bar inactive bg |
| Panel Border | `--panel-border` | `#2b303b` | Borders, separators |
| Text Primary | `--text` | `#ffffff` | Headings, values |
| Text Muted | `--muted` | `#99a0ae` | Labels, secondary |
| Card Text | `--card-text` | `#f5f7fa` | Card value text |
| Accent Blue A | `--accent-a` | `#2b6cff` | Primary blue |
| Accent Blue B | `--accent-b` | `#00c2ff` | Secondary blue/cyan |
| Accent Border | `--accent-border` | `#2a7bdc` | Button border |
| Bar Border | `--bar-border` | `#9bd9ff` | Active bar border |

**Alternate Accent (Green -- charging complete):**
| Token | Value |
|-------|-------|
| Green A | `#06d689` |
| Green B | `#04dac1` |
| Green Border | `#459382` |
| Green Bar Border | `#85ffe4` |

### Typography
- **Primary Font:** `"Inter"`, `system-ui`, `-apple-system`, `Segoe UI`, `Roboto`, `Helvetica`, `Arial`, sans-serif
- Title: 18px, weight 600, letter-spacing -0.5px, line-height 1.5
- Percent display: 56px, weight 400, letter-spacing -1.1px
- Miles display: 56px, weight 400, letter-spacing -1.1px
- Miles label: 22px, letter-spacing -1.1px, color `--muted`
- Card label: 12px, weight 600, letter-spacing -0.2px, uppercase
- Card value: 16px, weight 500, uppercase
- Button text: 16px, weight 600, letter-spacing -0.2px

### CSS Design Tokens
```css
/* Widget dimensions */
.widget { width: 424px; height: 546px; border-radius: 0px; }

/* Inner shadow system */
.widget__inner {
    box-shadow: inset 0px 4px 11.1px 0px #181b25,
                inset 0px 16px 15.5px 0px rgba(113, 119, 132, 0.34),
                inset 0px 46px 24.4px 0px rgba(0, 0, 0, 0.25);
}

/* Battery bar */
.bar { width: 8px; height: 100px; border-radius: 25px; }
.bar--full {
    background: linear-gradient(to bottom, var(--accent-a), var(--accent-b));
}

/* Stat cards */
.card { border-radius: 16px; padding: 16px; }
.card__icon {
    width: 32px; height: 32px; border-radius: 8px;
    background: #525866;
    box-shadow: inset 0px -6px 9.3px 0px rgba(0, 0, 0, 0.25);
}

/* Charge button */
.charge { height: 52px; border-radius: 20px; }
```

### WebGL Shader -- Energy Wave Effect
```glsl
// Fractional Brownian Motion noise
float fbm(vec2 p) {
    float v = 0.0; float a = 0.5;
    for (int i = 0; i < 4; i++) {
        v += a * smoothNoise(p);
        p *= 2.0; a *= 0.5;
    }
    return v;
}

// Main energy visualization
float wave1 = sin(uv.x * 15.0 - t * 5.0 + fbm(p + t) * 3.0) * 0.5 + 0.5;
float wave2 = sin(uv.x * 10.0 - t * 4.0 + uv.y * 3.0) * 0.5 + 0.5;
float wave3 = fbm(p * 2.0 + vec2(-t * 3.0, 0.0));
float energy = wave1 * 0.45 + wave2 * 0.35 + wave3 * 0.55;
energy = pow(energy, 1.3);
float pulse = sin(t * 3.5) * 0.18 + 0.9;
```
- Blend mode: Additive (`gl.SRC_ALPHA, gl.ONE`)
- SVG mask clips shader to bar shapes
- Color transitions between blue/green via `lerpHex()`

### Animation Techniques
1. **WebGL energy shader** -- continuous render loop
2. **Battery percentage flicker** -- random intervals (1.5-4s), +1% for 200-600ms
3. **Color lerp transition** -- speed 3, smooth blue-to-green
4. **Button gradient** -- radial gradient SVG as background-image
5. **CSS transitions** on hover: `opacity 120ms ease`

---

## 4. Radio Widget

**Style Category:** Retro-Modern / Physical Skeuomorphic / Analog

### Visual Concept
A 500x500px radio with a rotatable dial, frequency display, station tuning with white noise, and Rive-animated speaker icon. Skeuomorphic dial interaction with elastic resistance at boundaries.

### Color Palette
| Token | Value | Usage |
|-------|-------|-------|
| Page BG | `#151619` | Dark background |
| Widget BG | `#ececec` | Radio body (light gray) |
| Dial Ring Fill | `#D9D9D9` | SVG dial ring |
| Dial Ring Track | `#B8B8B8` | Progress track |
| Accent | `#FFB30F` | Golden yellow indicator |
| Display Left BG | `#8a8a8a` | Frequency display |
| Display Right BG | `#ffffff` | Station name display |
| Frequency Text | `#ffffff` | Large frequency numbers |
| Station Name | `rgba(0, 0, 0, 0.5)` | Station name text |
| Station Label | `rgba(0, 0, 0, 0.3)` | "Channel" label |
| Lines Border | `rgba(0, 0, 0, 0.1)` | Display borders |
| Dial Line | `#000` at 0.3 opacity | Tick marks |
| Modulation inactive | `rgba(0,0,0,0.2)` | AM/FM unselected |

### Typography
- **Primary Font:** `'Gilroy'` (custom @font-face, Light weight 300)
  - Source: `./fonts/Gilroy-Light.woff`
- Frequency display: 3.4375rem (55px)
- Station name: 1rem (16px)
- Channel label: 0.75rem (12px)
- Dial tick labels: 0.75rem (12px)
- AM/FM selector: 1rem, weight 300

### CSS Design Tokens
```css
.radio-widget {
    width: 500px; height: 500px;
    background-color: #ececec;
    border-radius: 0px;
}
.display { height: 4.5rem; }
.display-item { width: 8.75rem; }
.dial-svg { border-radius: 9999px; aspect-ratio: 418 / 449; }
.dial-inner { border-radius: 9999px; width: 45.3125rem; }
.modulation-selector-indicator {
    width: 0.1875rem; height: 0.1875rem;
    background-color: #000; border-radius: 999px;
}
```

### Dial Interaction System
- **Elastic resistance** at boundaries: `elasticStrength = 0.15`, `maxOvershoot = 20`
- **Snap-to-station** animation: 200ms, cubic ease-out `(1 - Math.pow(1 - progress, 3))`
- **Line height scaling:** Based on angular distance from center: `Math.max(0.4, 1 - (absAngle / 15) * 0.6)`
- **Touch + Mouse + Keyboard** input handling
- **White noise generator** during tuning (Web Audio API)
  - On-station volume: 0.05
  - Between-stations volume: 0.15

### Stations Data
| Name | Frequency | Stream |
|------|-----------|--------|
| Main FM | 88.3 | Radio Paradise AAC-128 |
| Beyond FM | 91.5 | Radio Paradise Beyond-128 |
| Rock FM | 94.7 | Radio Paradise Rock-128 |
| Serenity FM | 97.9 | Radio Paradise Serenity |
| Mellow FM | 101.1 | Radio Paradise Mellow-128 |

### Animation Techniques
1. **Dial rotation** -- CSS transform with `will-change: transform`, `backface-visibility: hidden`
2. **Snap animation** -- custom `requestAnimationFrame` loop, cubic ease-out
3. **AM/FM selector** -- `transition: transform 0.3s ease-in-out` with scale
4. **Rive animation** -- speaker icon via `.riv` file with state machine
5. **Line scale animation** -- dynamic `--line-scale` CSS variable per tick

---

## 5. Music Player

**Style Category:** Modern / Vinyl Skeuomorphic / Minimal Dark

### Visual Concept
A music player with vinyl record 3D flip animation, progress ring, track info (title, key, BPM), and morphing SVG play/pause button. Built with GSAP animation library.

### Key Technical Details
- **Animation Library:** GSAP 3.14.2
- **Bundled/Minified:** Source is obfuscated, compiled JS bundle
- **SVG morphing** for play/pause state transitions
- **3D vinyl flip** using CSS/GSAP transforms
- **Progress ring** visualization around vinyl

### Identifiable Patterns
- Audio playback via HTML5 `<audio>` API
- GSAP timeline animations for state transitions
- CSS Plugin for GSAP style manipulation
- Previous/Next/Play controls

---

## 6. Scribble Pad

**Style Category:** Minimal / Tool UI / Creative Canvas

### Visual Concept
A 292x320px drawing canvas with color palette, stroke width selector, clear button, and a "turbulence" effect that continuously distorts drawn strokes with sine-wave displacement.

### Color Palette
| Token | Value | Usage |
|-------|-------|-------|
| Page BG | `#111111` | Page background |
| Canvas BG | `#333333` | Drawing surface |
| Stroke Red | `#FF6B6B` | Color option |
| Stroke Orange | `#FFA94D` | Color option |
| Stroke Green | `#69DB7C` | Color option |
| Stroke Blue | `#4DABF7` | Color option |
| Stroke Purple | `#CC5DE8` | Color option (default) |
| Stroke Indicator | `#666` | Inactive dot |
| Clear Button Text | `rgba(255, 255, 255, 0.5)` | Default |
| Clear Button Hover | `rgba(255, 255, 255, 0.9)` | Hover state |
| Button Hover BG | `rgba(255, 255, 255, 0.1)` | Clear button bg |
| Cancel Button BG | `rgba(0, 0, 0, 0.5)` | Cancel overlay |
| Cancel Button Hover | `rgba(0, 0, 0, 0.65)` | Cancel hover |
| Color Swatch Border | `inset 0 0 0 0.5px rgba(0, 0, 0, 0.1)` | Inner border |

### Typography
- **Primary Font:** `"Inter"`, sans-serif
- Clear button: 14px, weight 500
- System font stack for body: sans-serif

### CSS Design Tokens
```css
.widget-container { width: 320px; }
.canvas-container { width: 292px; height: 320px; background-color: #333333; }
canvas { cursor: crosshair; touch-action: none; }
.clear-button { height: 38px; border-radius: 19px; }
.stroke-selector { width: 38px; height: 38px; border-radius: 50%; }
.color-selector { width: 38px; height: 38px; border-radius: 10px; }
.color-indicator { width: 30px; height: 30px; border-radius: 6px; }
.color-option { width: 38px; height: 38px; border-radius: 10px; }
.color-option-inner { width: 30px; height: 30px; border-radius: 6px; }
```

### Canvas Drawing Implementation
- **Rendering:** Canvas 2D context
- **DPR scaling:** `window.devicePixelRatio` for retina displays
- **Line properties:** `lineCap: "round"`, `lineJoin: "round"`
- **Stroke widths:** 8, 10, 12, 14, 16 pixels
- **Pre-loaded strokes:** 3 demo strokes with recorded point data

### Turbulence Effect
```javascript
turbulenceAmount = 0.65;   // displacement magnitude
turbulenceFrequency = 0.5; // spatial frequency
animationSpeed = 2;        // time progression rate
frequencyVariation = 1;    // frequency modulation depth
amountVariation = 1;       // amplitude modulation depth

// Displacement formula:
offsetX = sin(x * freq + t * 0.01) * sin(y * freq * 0.5 + t * 0.02) * amount;
offsetY = sin(y * freq + t * 0.015) * sin(x * freq * 0.5 + t * 0.025) * amount;
```
- Runs at 50fps (20ms interval)
- Frequency modulated by: `baseFrequency + sin(time * 0.8) * baseFrequency`
- Amount modulated by: `baseAmount + sin(time * 0.6) * baseAmount`

### Animation Techniques
1. **Turbulence loop** -- setInterval at 20ms, sine-based displacement
2. **Color panel reveal** -- staggered entry with cubic-bezier bounce: `(0.175, 0.885, 0.32, 1.275)`
3. **Stroke panel reveal** -- identical stagger pattern
4. **Button press** -- `transform: scale(0.9)` on `:active`
5. **Controls depression** -- `scale(0.95)`, `filter: blur(4px)`, `opacity: 0` during panel open
6. **Hover dim overlay** -- `.hover-dim` with `opacity: 0 -> 0.15`
7. **Visibility management** -- Pauses turbulence when widget not visible (postMessage API)

---

## 7. Stickers

**Style Category:** Playful / 3D Interactive / Augmented Reality

### Visual Concept
An interactive MacBook laptop display with draggable stickers that respond to 3D perspective. Features sticker graphics ("Style Shift", "Prism" designs) with tilt sensitivity.

### Key Technical Details
- **Rendering:** Canvas-based with potential WebGL for 3D perspective
- **Interaction:** Drag with tilt sensitivity (`DRAG_TILT_SENSITIVITY = 3`)
- **CSS 3D Transforms:** `perspective`, `preserve-3d`, `perspective-origin`
- **Effects:** Sheen/gloss effects, shadow casting
- **SVG Sticker Graphics** with gradient definitions and color stops
- Source was truncated -- incomplete extraction

### Identifiable Colors
- SVG gradients with multiple color stops (linear gradients)
- 3D shadow/lighting calculations

---

## 8. Card Widget

**Style Category:** Premium Fintech / 3D Interactive / Dark Luxury

### Visual Concept
A credit card widget with 3D mouse-tracking tilt, flip animation, freeze effect (frost overlay), mechanical counter for balance, and "Add Cash" floating amount indicator. Uses squircle (superellipse) border shapes.

### Color Palette
| Token | Value | Usage |
|-------|-------|-------|
| Widget BG Gradient Start | `#0b0b0a` | Dark near-black |
| Widget BG Gradient End | `#242c2f` | Dark blue-gray |
| Card Gradient | `#4a4a4a` to `#3d3d3d` to `#353535` to `#3a3a3a` to `#424242` | Card surface |
| Card Top Highlight | `rgba(255,255,255,0.08)` | Gradient highlight |
| Card Bottom Shadow | `rgba(0,0,0,0.15)` | Gradient shadow |
| Card Inset Top | `#ffffff1a` (white 10%) | Top edge highlight |
| Card Inset Bottom | `#0003` (black 20%) | Bottom edge shadow |
| Text Primary | `#fff` | White |
| Text Secondary | `#fff6` (white 40%) | Muted labels |
| Button BG | `#ffffff1a` (white 10%) | Action button default |
| Button Hover | `#fff3` (white 20%) | Action button hover |
| Button Active BG | `#fff` | Pressed/active state |
| Button Active Icon | `#0d0d0c` | Icon on white |
| Accent Green | `#4ade80` | Floating "+$" amount |
| Card Line | `#737373` to `#d9d9d98c` | Decorative gradient line |
| Frost Border | `white` at 0.5 opacity | Frozen state dashed border |

### Typography
- **Primary Font:** `Inter`, sans-serif (with variable font support via `InterVariable`)
- **Font Features:** `"liga" 1, "calt" 1`
- Card name: 0.875rem (14px), weight 500
- Money display: 0.875rem, weight 500
- Card action label: 0.75rem, weight 500
- SVG card brand text: custom SVG paths

### CSS Design Tokens
```css
.card-widget {
    width: 24.25rem; height: 31.25rem;
    background-image: linear-gradient(153deg, #0b0b0a 0% 40%, #242c2f);
    border-radius: 8px;
    gap: 2.0625rem;
}
.card {
    width: 281px; height: 11.6875rem;
    --squircle-radius: 1.0625rem;
    padding: 0.75rem;
}
.card-action button {
    width: 3.5rem; height: 3.5rem;
    border-radius: 999px;
}
```

### Squircle Implementation (CSS `shape()` with fallback)
```css
@supports (clip-path: shape(from 0 0, close)) {
    .squircle {
        border-radius: 0;
        clip-path: shape(
            from 0px var(--d-tl),
            curve to var(--d-tl) 0px with 0px var(--sm-tl) / var(--sm-tl) 0px,
            hline to calc(100% - var(--d-tr)),
            /* ... continues for all corners */
            close
        );
    }
}
```
- Uses CSS `shape()` function (cutting-edge CSS)
- Fallback to standard `border-radius`
- Variables: `--sm-*` = `radius * 0.375`, `--d-*` = `radius * 1.3`

### 3D Card Interaction
```javascript
// Mouse tracking
const rotateY = (pointerX_percent - 50) / 50 * 15; // max +/-15deg
const rotateX = (50 - pointerY_percent) / 50 * 15; // max +/-15deg

// Glare effect
.card:before {
    background: radial-gradient(
        circle at var(--pointer-x) var(--pointer-y),
        rgba(255,255,255,0.15), transparent 70%
    );
    filter: blur(20px);
}
```

### Animation Techniques
1. **3D tilt** -- CSS `transform: rotateX() rotateY()` via CSS variables, 0.1s ease-out response
2. **Flip animation** -- `rotateX(180deg)`, 0.6s `cubic-bezier(0.76, 0, 0.24, 1)`
3. **Freeze effect** -- scale to 0.9, opacity to 0.2, frost image overlay fades in
4. **Mechanical counter** -- digit rolling via `translateY(calc(var(--digit) * -1.2em))`
   - Roll animation: 0.5s `cubic-bezier(0.22, 1, 0.36, 1)`
   - Mask: `linear-gradient(to bottom, transparent 0%, black 25%, black 75%, transparent 100%)`
5. **Floating amount** -- `floatIn` (translateY + opacity) / `floatOut` animations, 0.3s
6. **Mouse leave spring** -- `cubic-bezier(0.34, 1.56, 0.64, 1)` (overshoot bounce)
7. **Button press** -- active state instantly changes bg to white
8. **Counter shift** -- horizontal translation on width change with smooth transition

---

## 9. Text Editor Widget

**Style Category:** Minimal / Productivity Tool

### Visual Concept
A rich text editor widget built on ProseMirror. Source was fully minified/obfuscated, preventing full design extraction.

### Key Technical Details
- **Framework:** ProseMirror-compatible editor
- **Architecture:** Document fragment model, selection management, transaction handling
- **Features:** Mark/node type system, parsing, serialization
- Source is a compiled JavaScript bundle (not extractable as HTML/CSS)

---

## 10. Robot Widget

**Style Category:** Friendly Tech / Dot-Matrix Display / Conversational UI

### Visual Concept
A tall phone-shaped widget (402x874px) featuring "Jitty" the robot. Top section shows an animated dot-grid face with blinking eyes and moving mouth. Bottom section displays typewriter-animated multilingual text.

### Color Palette
| Token | Value | Usage |
|-------|-------|-------|
| Page BG | `#151619` | Background |
| Widget BG | `#ffffff` | White body |
| Face BG | `#000000` | Face panel |
| Dot Active | `#FF9421` | Orange -- eyes/mouth |
| Dot Inactive | `rgba(255, 148, 33, 0.14)` | Dim orange grid |
| Text Panel BG | `#e2f0f4` | Pale blue |
| Text Color | `#000000` | Display text |
| Label Color | `#70949f` | Language selector |
| Bottom Bar BG | `#000000` | Navigation bar |
| Nav Item BG | `#e2f0f4` | Nav button default |
| Nav Active | `#ff9421` | Active nav button (orange) |
| Nav Icon | `#383838` | Dark gray icons |
| Dropdown BG | `#ffffff` | Language dropdown |
| Dropdown Shadow | `rgba(0, 0, 0, 0.1)` | `0 4px 12px` |
| Selected Item BG | `#e2f0f4` | Selected language |
| Selected Item Text | `#70949f` | Selected language text |
| Hover BG | `#f0f7f9` | Dropdown item hover |
| Badge BG | `#70949f` | "Soon" badge |
| Badge Text | `rgba(255, 255, 255, 0.7)` | Badge text |

### Typography
- **Display Font:** `'PP Mondwest'` (custom @font-face, Regular 400)
  - Source: `./fonts/PPMondwest-Regular.otf`
  - Size: 4.6875rem (75px)
  - Line-height: 1
  - Letter-spacing: -0.0938rem
- **UI Font:** `'Inter'` (custom @font-face, Medium 500)
  - Source: `./fonts/Inter-Medium.woff2`
  - Size: 0.875rem for selectors

### CSS Design Tokens
```css
.robot-widget {
    width: 402px; height: 874px;
    background-color: #ffffff;
    border-radius: 0px;
    padding: 0.3125rem; gap: 0.375rem;
}
.face {
    height: 21.125rem;
    border-radius: 2.1875rem;
}
.text {
    height: 33.5rem;
    border-radius: 2.1875rem;
}
.bottom-bar {
    border-radius: 1.8125rem;
    padding: 0.5rem;
}
.bottom-bar > li {
    border-radius: 1.3125rem;
    aspect-ratio: 1 / 1;
}
```

### Canvas Dot Grid Face
```javascript
dotRadius = 3;
dotSpacing = 8;
dotColor = '#FF9421';      // active
dotColorOff = 'rgba(255, 148, 33, 0.14)'; // inactive

// Eye parameters:
eyeRadiusX = canvas.width * 0.075;
baseEyeRadiusY = canvas.height * 0.15;
eyeSpacing = cols * 0.2 * dotSpacing;
eyeVerticalOffset = canvas.height * 0.09;
maxEyeOffset = 8; // pixels of eye-tracking range

// Mouth parameters:
smileWidth = canvas.width * 0.25;
smileCurve = canvas.height * 0.04;
smileThickness = dotSpacing * 0.8;
smileVerticalPosition = centerY + canvas.height * 0.29;
```

### Animation Techniques
1. **Dot grid rendering** -- Canvas 2D, requestAnimationFrame loop
2. **Blink animation** -- Random intervals 2-6s, progress 0->1->2 cycle, speed 0.15/frame
3. **Mouth animation** -- Random open/close intervals (3-8s open, 1-3s closed), speed 0.08/frame
4. **Eye tracking** -- Follows mouse position with max 8px offset, distance-based falloff (normalized at 300px)
5. **Glow effect** -- `ctx.shadowColor = dotColor; ctx.shadowBlur = 20;` for active dots
6. **Typewriter text** -- 50ms per character, auto-advance every 5000ms
7. **Language dropdown** -- CSS transitions: `opacity 0.3s`, `transform 0.3s` with `cubic-bezier(0.22, 1, 0.36, 1)`
8. **Chevron rotation** -- `transform: rotate(180deg)`, 0.3s

### Multilingual Content
- English, Spanish, French (with Japanese "Soon")
- 8 phrases per language
- Line breaks preserved via `\n` with `white-space: pre-wrap`

---

## 11. Movie Rating App

**Style Category:** Editorial / Entertainment UI

### Visual Concept
Movie rating interface with page peel/turn animation effect. Built with GSAP animation library and a custom "Peel" effect library.

### Key Technical Details
- **Animation Library:** GSAP
- **Custom Library:** Page-peel/turning effect
- **SVG Path Parsing:** Complex drawing command utilities
- Source was fully minified -- limited design extraction
- CSS Plugin for GSAP style manipulation

---

## 12. Video Player

**Style Category:** Minimal / Media Player

### Visual Concept
Video player widget. Page returned only the text "video-player" with no extractable source code. Likely requires JavaScript execution to render.

### Key Technical Details
- Served at `/homepage-widgets/video-player/dist/index.html`
- Built application (dist folder suggests bundled build)
- No static HTML content available for extraction

---

## 13. Voice Recorder

**Style Category:** Brutalist-Minimal / Military-Technical / HUD

### Visual Concept
A "Signal Capture Unit" with radial tick-mark visualizer, central record button, timer display, and status readout. Clean, technical aesthetic with minimal decoration.

### Color Palette -- CSS Custom Properties
| Token | Variable | Value | Usage |
|-------|----------|-------|-------|
| Background | `--bg-color` | `#151619` | Page and card BG |
| Card BG | `--card-bg` | `#151619` | Widget container |
| Text Primary | `--text-primary` | `#FFFFFF` | Main text |
| Text Secondary | `--text-secondary` | `#8E9299` | Labels, muted |
| Record Active | (inline) | `#FF4444` | Recording indicator |
| Record Glow | (inline) | `rgba(255, 68, 68, 0.4)` | Record button glow |
| Idle Ticks | (inline) | `#8E9299` | Non-recording ticks |
| Active Ticks | (inline) | `rgba(255,255,255,0.85)` | Recording ticks |
| Pulse Ring | (inline) | `rgba(255,255,255,0.3)` | Pulse border |
| Divider | (inline) | `rgba(255,255,255,0.1)` | Footer border |

### Typography
- **UI Font:** `'Inter'`, `-apple-system`, `BlinkMacSystemFont`, `"Segoe UI"`, `Roboto`, `Helvetica`, `Arial`, sans-serif
- **Mono Font:** `'JetBrains Mono'`, `'Roboto Mono'`, monospace
- Reference label: 10px mono, letter-spacing 1px, opacity 0.7
- Status label: 10px mono, uppercase, letter-spacing 1px
- Main readout: 14px, line-height 1.4
- Timer: 11px mono, letter-spacing 1px

### CSS Design Tokens
```css
.widget-container {
    width: 380px; height: 520px;
    border-radius: 0px; /* var(--border-radius) */
    box-shadow: 0 20px 40px rgba(0,0,0,0.15);
}
.radial-hud { width: 280px; height: 280px; }
.radial-track {
    width: 176px; height: 176px;
    border: 1px dashed var(--text-secondary);
    border-radius: 50%;
}
.record-trigger {
    width: 60px; height: 60px;
    border-radius: 50%;
    border: 1px solid var(--text-secondary);
    transition: all 0.3s cubic-bezier(0.2, 0.8, 0.2, 1);
}
.trigger-icon {
    width: 8px; height: 8px;
    border-radius: 1px;
}
.is-recording .trigger-icon {
    width: 12px; height: 12px;
    border-radius: 2px;
    background-color: #FF4444;
    box-shadow: 0 0 10px rgba(255, 68, 68, 0.4);
}
.timer-display {
    border-top: 1px solid rgba(255,255,255,0.1);
}
```

### Canvas Radial Visualizer
```javascript
tickCount = 120;
baseRadius = 105;
baseTickLength = 4;

// Recording mode noise:
noise = sin(i * 0.2 + time) * cos(i * 0.1 - time * 2) * 32;
noise += random() * 10;

// Idle mode:
noise = sin(i * 0.1 + time) * 5;

// Rendering:
ctx.lineWidth = 1.5;
```

### Animation Techniques
1. **Radial ticks** -- Canvas 2D, requestAnimationFrame, 120 ticks with noise displacement
2. **Radial track spin** -- `@keyframes spin { 0% rotate(0deg) -> 100% rotate(360deg) }`, 60s linear infinite
3. **Pulse ring** -- `@keyframes pulse-ring`, scale 0.8->1.5 with opacity fade, 2s infinite
4. **Record button hover** -- scale(1.05), border color lighten
5. **Record button press** -- scale(0.95)
6. **Timer update** -- setInterval at 10ms for centisecond precision
7. **Icon morph** -- trigger-icon transitions width/height/border-radius/color on recording state

---

## 14. Infinite Gallery

**Style Category:** Minimal / Image Grid / Infinite Scroll

### Visual Concept
An infinite-scrolling photo gallery with a quincunx (honeycomb offset) grid layout. Cards snap to center, non-centered cards dim to 15% opacity. Drag/flick physics with velocity-based momentum.

### Color Palette
| Token | Value | Usage |
|-------|-------|-------|
| Gallery BG | `#1c1c1c` | Container background |
| Handle BG | `#262626` | Username pill |
| Text | `#fff` | Usernames |
| Card Active Opacity | `1` | Centered card |
| Card Inactive Opacity | `0.15` | Non-centered cards |

### Typography
- **Primary Font:** `Inter`, sans-serif (with `InterVariable` support)
- **Font Features:** `"liga" 1, "calt" 1`
- Handle text: 1rem, weight 600
- Handle pill: 0.625rem horizontal padding, 1.125rem vertical

### CSS Design Tokens
```css
.gallery-container {
    width: 25.125rem; height: 54.625rem;
    background-color: #1c1c1c;
    border-radius: 8px;
    touch-action: none;
}
.gallery {
    cursor: grab;
    will-change: transform;
}
.gallery:active { cursor: grabbing; }
.gallery-card {
    width: 15.625rem; height: 15.625rem; /* 250x250px */
    border-radius: 2.5rem; /* 40px */
    transition: opacity 0.3s ease-out;
}
.gallery-card img { border-radius: 2.5rem; }
.card-handle {
    background-color: #262626;
    border-radius: 999px;
    padding: 0.625rem 1.125rem;
    transition: all 0.2s ease-out;
}
```

### Grid Layout System
```javascript
cols = 3;
rows = 5;
cardWidth = 250;   // px
cardHeight = 250;  // px
gap = 8;           // px
quincunxOffset = 258 / 2; // 129px offset for odd rows
```

### Physics System
```javascript
// Velocity tracking
velocityX = (currentOffset - lastOffset) / deltaTime * 16;

// Momentum decay
this.velocityX *= 0.95;  // friction coefficient
this.velocityY *= 0.95;

// Magnetic snap threshold
if (velocity < 3) {
    attraction = 0.05 * (1 - velocity / 3);
    offsetX += (targetX - offsetX) * attraction;
}

// Snap animation
duration = 300; // ms
easing = (t) => 1 - Math.pow(1 - t, 3); // cubic ease-out
```

### Animation Techniques
1. **Drag physics** -- pointer events with velocity tracking, momentum decay (0.95 friction)
2. **Snap-to-center** -- 300ms cubic ease-out animation to nearest card center
3. **Magnetic attraction** -- When velocity < 3, soft pull toward nearest card
4. **Infinite wrap** -- Cards repositioned when exiting viewport bounds (tile wrapping)
5. **Opacity transitions** -- 0.3s ease-out between active (1) and inactive (0.15)
6. **Handle reveal** -- opacity + scale transition only when card centered and motion stopped

---

## 15. Cross-Widget Design Patterns

### Common Layout Patterns

1. **Centering Strategy:** All widgets use `display: flex; justify-content: center; align-items: center; height: 100vh;`
2. **User Selection Prevention:** `user-select: none; -webkit-user-select: none; -webkit-touch-callout: none;`
3. **Border Radius:** Most widgets use `border-radius: 0px` for the outer container (deliberate sharp edges for iframe embedding)
4. **Overflow Control:** `overflow: hidden` on all widget containers
5. **Box Sizing:** `box-sizing: border-box` universally applied

### Common Interaction Patterns

1. **Debug Logging System:** Every widget checks `localStorage.getItem('vg-debug-widgets') === '1'` for debug mode
2. **Visibility Management:** Widgets listen for `window.message` events with `{type: 'widget-state', visible: bool}` to pause/resume animations
3. **Touch Support:** All interactive widgets handle both mouse and touch events
4. **Performance Monitoring:** Debug mode logs render times > 24ms (16ms for timers)

### Common Animation Easings
| Name | Value | Usage |
|------|-------|-------|
| Smooth decelerate | `cubic-bezier(0.22, 1, 0.36, 1)` | Most UI transitions |
| Spring bounce | `cubic-bezier(0.34, 1.56, 0.64, 1)` | Overshoot effects |
| Sharp ease | `cubic-bezier(0.76, 0, 0.24, 1)` | Card flip |
| Record button | `cubic-bezier(0.2, 0.8, 0.2, 1)` | Voice recorder |
| Panel bounce | `cubic-bezier(0.175, 0.885, 0.32, 1.275)` | Scribble pad panels |

### Shared Shadow Patterns
1. **Inset depth:** `inset 0 1px 1px rgba(255,255,255,0.1), inset 0 -1px 1px rgba(0,0,0,0.2)`
2. **Card elevation:** `0 20px 40px rgba(0,0,0,0.15)`
3. **Inner icon depth:** `inset 0px -6px 9.3px 0px rgba(0,0,0,0.25)`
4. **Dropdown shadow:** `0 4px 12px rgba(0,0,0,0.1)`

---

## 16. Master Color Palette

### Background Colors (Dark)
| Color | Hex | Widgets |
|-------|-----|---------|
| Pure Black | `#000` / `#000000` | CRT, Robot face |
| Near Black 1 | `#0b0b0a` | Card widget gradient |
| Near Black 2 | `#0e121b` | Bike battery surfaces |
| Dark Gray 1 | `#111` / `#111111` | Weather, Scribble bg |
| Dark Gray 2 | `#151619` | Radio, Robot, Voice Recorder |
| Dark Gray 3 | `#181b25` | Bike Battery |
| Dark Gray 4 | `#1c1c1c` | Infinite Gallery |
| Medium Dark | `#242c2f` | Card gradient end |

### Background Colors (Light)
| Color | Hex | Widgets |
|-------|-----|---------|
| White | `#ffffff` | Robot body, dropdown |
| Off-white | `#ececec` | Radio body |
| Pale Blue | `#e2f0f4` | Robot text panel |
| Hover Blue | `#f0f7f9` | Dropdown hover |
| Canvas Gray | `#333333` | Scribble canvas |

### Accent Colors
| Color | Hex | Widgets |
|-------|-----|---------|
| Electric Blue | `#2b6cff` | Bike battery |
| Cyan | `#00c2ff` | Bike battery |
| Teal Green | `#06d689` | Bike battery (charged) |
| Mint | `#04dac1` | Bike battery (charged) |
| Golden Yellow | `#FFB30F` | Radio dial accent |
| Orange | `#FF9421` / `#ff9421` | Robot active elements |
| Red | `#FF4444` | Voice recorder record |
| Red Soft | `#FF6B6B` | Scribble color |
| Orange Soft | `#FFA94D` | Scribble color |
| Green Soft | `#69DB7C` | Scribble color |
| Blue Soft | `#4DABF7` | Scribble color |
| Purple Soft | `#CC5DE8` | Scribble color |
| Success Green | `#4ade80` | Card floating amount |

### Text Colors
| Color | Hex/Value | Widgets |
|-------|-----------|---------|
| White | `#ffffff` | Most widgets |
| Light Gray | `#e0e0e0` | CRT text |
| Muted Gray | `#99a0ae` | Bike battery labels |
| Steel Gray | `#8E9299` | Voice recorder labels |
| Teal Gray | `#70949f` | Robot labels |
| Dark Gray | `#383838` | Robot nav icons |
| Half White | `rgba(255,255,255,0.5)` | Multiple widgets |
| Quarter White | `rgba(255,255,255,0.4)` | Card secondary |

---

## 17. Master Typography System

### Font Families Used

| Font | Weight | Format | Widget |
|------|--------|--------|--------|
| **JetBrains Mono** | Regular | System | CRT, Voice Recorder |
| **Inter** | 500 (Medium) | woff2 (custom) | Robot, multiple |
| **Inter** | 400-600 | System | Bike Battery, Scribble, Card, Gallery |
| **InterVariable** | Variable | System | Card, Gallery |
| **Gilroy** | 300 (Light) | woff | Radio |
| **PP Mondwest** | 400 (Regular) | otf | Robot display text |
| **Caveat** | Regular | Google Fonts | Weather card |

### Type Scale Patterns

**Dashboard/Data (Bike Battery):**
- Hero number: 56px, weight 400, spacing -1.1px
- Title: 18px, weight 600, spacing -0.5px
- Label: 12px, weight 600, spacing -0.2px, uppercase
- Value: 16px, weight 500, uppercase

**Display (Robot):**
- Hero text: 75px, weight 400, spacing -1.5px, PP Mondwest
- UI label: 14px, weight 500, Inter

**Technical (Voice Recorder):**
- Reference code: 10px mono, spacing 1px
- Status text: 14px, line-height 1.4
- Timer: 11px mono, spacing 1px

**Financial (Card):**
- Balance: 14px, weight 500
- Action labels: 12px, weight 500

---

## 18. Animation Technique Catalog

### WebGL/Shader Effects
1. **CRT phosphor simulation** -- beam physics with Gaussian profiles and exponential decay
2. **Bike battery energy waves** -- FBM noise, sine wave composition, additive blending
3. **Stickers 3D perspective** -- Canvas/WebGL with perspective transforms

### Canvas 2D Rendering
1. **Robot dot grid** -- Ellipse-based eye detection, smile curve math, glow via shadowBlur
2. **Voice recorder radial ticks** -- 120 ticks with sine/cosine noise displacement
3. **Scribble pad drawing** -- Retina-aware, turbulence displacement, stroke replay

### CSS Animation Patterns
1. **Rain particles** -- N elements with random duration/delay/scale
2. **SVG stroke draw** -- dasharray/dashoffset sequential reveal
3. **3D card tilt** -- CSS custom properties driven by mouse position
4. **Mechanical counter** -- translateY digit rolling with mask gradient
5. **Elastic dial snap** -- requestAnimationFrame with cubic ease-out
6. **Pulse rings** -- scale + opacity keyframes, infinite loop
7. **Typewriter text** -- setTimeout character-by-character reveal

### Physics Simulations
1. **Dial elastic resistance** -- Overshoot clamping with springy snap-back
2. **Gallery momentum** -- Velocity tracking, 0.95 friction decay, magnetic snap
3. **Turbulence field** -- Sine-based displacement with frequency/amplitude modulation

### State Machine Animations
1. **Radio tuning** -- play/pause/tune states with white noise crossfade
2. **Card freeze** -- scale + opacity + frost overlay state
3. **Voice recorder** -- idle/recording states with icon morph
4. **Battery charging** -- color lerp between blue/green palettes

### Easing Functions Summary
```
Smooth decelerate:  cubic-bezier(0.22, 1, 0.36, 1)    -- most common
Spring overshoot:   cubic-bezier(0.34, 1.56, 0.64, 1)  -- playful bounces
Sharp symmetric:    cubic-bezier(0.76, 0, 0.24, 1)      -- dramatic moves
Panel bounce:       cubic-bezier(0.175, 0.885, 0.32, 1.275) -- UI reveals
Cubic ease-out:     (t) => 1 - Math.pow(1 - t, 3)       -- JS animations
```

---

## Design Philosophy Summary

Variant's widget collection demonstrates several overarching principles:

1. **Tactile Realism** -- Physical metaphors (radio dials, battery bars, CRT screens) with authentic interaction models including elastic resistance, momentum, and snap-to behavior.

2. **Dark-First Design** -- Nearly every widget uses a dark background (#111-#1c1c1c range) with carefully calibrated text opacity levels for hierarchy.

3. **Performance-Conscious Animation** -- Debug logging for frame drops, visibility-based pause/resume, `will-change` hints, and `backface-visibility: hidden` optimizations.

4. **Progressive Enhancement** -- CSS `@supports` for squircle clip-paths, WebGL fallbacks, Rive animation with graceful degradation.

5. **Micro-interaction Rich** -- Every interactive element has hover, active, and transition states. No bare interactions.

6. **Zero Border Radius on Containers** -- All outer widget containers use `border-radius: 0px`, creating a deliberate, modular tile aesthetic when arranged in the homepage grid. Inner elements use generous radius (16px-40px).

7. **Unified Infrastructure** -- Common debug system (`vg-debug-widgets`), visibility management via postMessage, and consistent CSS reset patterns across all widgets.
