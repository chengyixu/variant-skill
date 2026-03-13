# Variant.com Widget Source Reference

Extracted via Jina r.reader API with `X-Engine: browser` and `X-Return-Format: html`.

## Widget Index

| Widget | URL | Theme | Key Font | Key Colors |
|--------|-----|-------|----------|------------|
| Bike Battery | `/homepage-widgets/bike-battery/bike-battery.html` | Dark (#181b25) | Inter 400-700 | Blue #2b6cff → Cyan #00c2ff |
| Poetic Weather | `/homepage-widgets/poetic-weather/index.html` | Dark (#111) | Caveat cursive | White on photo |
| CRT/DOOM | `/homepage-widgets/crt/crt.html` | Black (#000) | JetBrains Mono | Green phosphor |
| Radio | `/homepage-widgets/radio-widget/index.html` | Light (#ececec) | Gilroy 300 | Gold #FFB30F |
| Card | `/homepage-widgets/card/card.html` | Dark gradient | Inter variable | Gray #4a4a4a, Green #4ade80 |
| Scribble Pad | `/homepage-widgets/scribble-pad/index.html` | Dark (#111111) | sans-serif | Canvas #333333 |
| Stickers | `/homepage-widgets/stickers/stickers.html` | Black (#000) | Courier New | MacBook gray gradient |
| Robot | `/homepage-widgets/robot-widget/index.html` | White (#ffffff) | PP Mondwest | Orange #ff9421, Teal #e2f0f4 |
| Music Player | `/homepage-widgets/music-player/dist/index.html` | Black | — (Vite bundle) | Magenta/pink glow |
| Video Player | `/homepage-widgets/video-player/dist/index.html` | — | — (Vite bundle) | — |

## Complete CSS Variables Per Widget

### Bike Battery
```css
:root {
  --page-bg: #181b25;
  --panel-bg: #181b25;
  --panel-surface: #0e121b;
  --panel-border: #2b303b;
  --text: #ffffff;
  --muted: #99a0ae;
  --card-text: #f5f7fa;
  --accent-a: #2b6cff;
  --accent-b: #00c2ff;
  --accent-border: #2a7bdc;
  --bar-border: #9bd9ff;
}
/* Green charging variant: */
/* --accent-a: #06d689; --accent-b: #04dac1; --accent-border: #459382; --bar-border: #85ffe4; */
```

### Radio Widget
```css
:root {
  font-family: 'Gilroy', system-ui, sans-serif;
  font-weight: 300;
  background-color: #151619;
}
/* Widget bg: #ececec */
/* Display left bg: #8a8a8a */
/* Display right bg: #ffffff */
/* Dial lines: #000 opacity 0.3 */
/* Active frequency accent: #FFB30F */
/* AM/FM inactive: opacity 0.2, scale(0.8) */
```

### Robot Widget
```css
:root {
  background-color: #151619;
  color: rgba(255, 255, 255, 0.87);
}
/* Widget: #ffffff */
/* Face: #000000 */
/* Text area: #e2f0f4 */
/* Language selector: #70949f */
/* Dropdown bg: #ffffff */
/* Dropdown hover: #f0f7f9 */
/* Selected: #e2f0f4 with #70949f text */
/* "Soon" badge: #70949f bg, white text */
/* Bottom bar: #000000 bg */
/* Button base: #e2f0f4 */
/* Active button: #ff9421 */
/* Text: #000000, PP Mondwest 75px */
/* Dot grid: #FF9421 active, rgba(255,148,33,0.14) off */
```

### Card Widget
```css
:root {
  font-family: Inter, sans-serif;
  --frost-image: url("./assets/img_7d5d3328.webp");
}
/* Widget gradient: linear-gradient(153deg, #0b0b0a 0% 40%, #242c2f) */
/* Card surface: linear-gradient(to bottom, #4a4a4a, #3d3d3d, #353535, #3a3a3a, #424242) */
/* Card highlight: linear-gradient(145deg, rgba(255,255,255,0.08), transparent, rgba(0,0,0,0.15)) */
/* Card inner shadows: inset 0 1px 1px rgba(255,255,255,0.1), inset 0 -1px 1px rgba(0,0,0,0.2) */
/* Action button: rgba(255,255,255,0.1) bg, 999px radius */
/* Action hover: rgba(255,255,255,0.2) */
/* Action active: #fff bg, #0d0d0c text */
/* Money text: #fff */
/* Card name: rgba(255,255,255,0.4) */
/* Float amount: #4ade80 (green) */
/* Border SVG: stroke-dasharray="1 4" stroke-opacity="0.5" */
```

### Stickers Widget
```css
/* Body: #000, perspective: 1200px */
/* MacBook container: 840x528px */
/* Lid: linear-gradient(180deg, #333335, #1e1e1f) */
/* Lid overlay: mix-blend-mode: overlay, linear-gradient(230deg, rgba(190,191,196,0.7) 17%, rgba(127,128,131,0.7) 81%) */
/* Lid shadow: inset 0px -4.539px 22.695px rgba(0,0,0,0.2) */
/* Sticker shadow: drop-shadow(0px var(--sh-y) var(--sh-blur) rgba(0,0,0,0.30)) */
/* Render scale: 4x for retina */
/* Drag tilt max: 14.4deg, smoothing: 0.1 */
/* Sheen strength: 0.6, tilt shift: 0.05 */
```

### Poetic Weather
```css
/* Body: #111 */
/* Card: 252x310px */
/* Card glass: inset 0 -4px 8px rgba(0,0,0,0.25), inset 0 4px 6px rgba(255,255,255,0.55) */
/* Blur: backdrop-filter blur(8px) */
/* Gradient: linear-gradient(180deg, rgba(0,0,0,0.2), rgba(0,0,0,0.4)) */
/* Raindrop: 2px wide, 40px tall, white, blur(4px) */
/* Fall animation: 0.33-1.04s, random delay */
/* Location pill: blur(10px), gradient bg, 12px radius, 24px height */
/* SVG text: stroke-dasharray animation, 1.75px white stroke */
```

## Advanced Techniques

### WebGL Battery Shader (Bike Battery)
The battery bars use a WebGL fragment shader for energy pulse animation:
- Fractal Brownian Motion (fbm) for organic movement
- Wave patterns at 3 frequencies: 15x, 10x, and fbm*2
- Pulse effect: sin(t*3.5) * 0.18 + 0.9
- Additive blending (gl.SRC_ALPHA, gl.ONE)
- SVG mask for bar shapes (objectBoundingBox coordinates)

### Squircle Clip-Path (Card Widget)
Uses CSS `shape()` function for iOS-like superellipse corners:
```css
@supports (clip-path: shape(from 0 0, close)) {
  .squircle {
    clip-path: shape(
      from 0px var(--d-tl),
      curve to var(--d-tl) 0px with 0px var(--sm-tl) / var(--sm-tl) 0px,
      hline to calc(100% - var(--d-tr)),
      curve to 100% var(--d-tr) with calc(100% - var(--sm-tr)) 0px / 100% var(--sm-tr),
      vline to calc(100% - var(--d-br)),
      curve to calc(100% - var(--d-br)) 100% with 100% calc(100% - var(--sm-br)) / calc(100% - var(--sm-br)) 100%,
      hline to var(--d-bl),
      curve to 0px calc(100% - var(--d-bl)) with var(--sm-bl) 100% / 0px calc(100% - var(--sm-bl)),
      close
    );
  }
}
/* Radius formula: sm = radius * 0.375, d = radius * 1.3 */
```

### LED Dot Grid (Robot Widget)
Canvas-based animated face with:
- Dot spacing: 8px, dot radius: 3px
- Eye tracking: follows mouse position, max 8px offset
- Blink: random 2-6s delay, 0.15 progress per frame
- Mouth: alternates open/closed every 3-8s
- Ellipse eye shapes with blink squash
- Active dots: #FF9421 with 20px shadowBlur glow
- Inactive dots: rgba(255,148,33,0.14)
- Visibility optimization: pauses when widget is offscreen

### Holographic Sticker Sheen (Stickers Widget)
WebGL-rendered stickers with:
- 4x render scale for retina
- Perspective-based tilt on drag (max 14.4deg)
- Holographic rainbow sheen on tilt
- Physics: drag tilt sensitivity 3, smoothing 0.1
- Drop shadow varies with CSS variables (--sh-y, --sh-blur)
- Alpha hit-test for click detection on irregular shapes
