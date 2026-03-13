# Variant.com — Complete Design Reference

## Source

- URL: https://variant.com/
- Captured: 2026-03-13
- Method: chrome-devtools DOM inspection + computed style extraction + visual screenshot analysis

## Product Context

Variant is an AI design tool. Users type an idea and get endless generated design options by scrolling. The tagline: "Endless designs for your ideas, just scroll." The site itself is a showcase of the tool's capabilities — interactive widget demos in a masonry grid.

## Page Structure (DOM)

```
RootWebArea "Variant – Endless designs for your ideas, just scroll"
├── main
│   ├── .HomepageV3_root (CSS Grid: 408px | 708px, height: 100vh)
│   │   ├── Left Panel (hero)
│   │   │   ├── Logo (SVG, 88x20px at x:24 y:24)
│   │   │   ├── h1 "Endless designs for your ideas, just scroll."
│   │   │   │   └── "just scroll." is italic
│   │   │   ├── p "Most tools make you explain what you want. Variant just shows you."
│   │   │   │   └── "Variant just shows you." is emphasized (brighter color)
│   │   │   ├── p "It's like working with a creative director that never runs out of options."
│   │   │   ├── Suggested prompts group
│   │   │   │   ├── button "Sign up / Sign in"
│   │   │   │   └── button "Surprise me"
│   │   │   └── (spacer to push input bar down)
│   │   │
│   │   └── Right Panel (widget showcase, overflow: hidden)
│   │       └── Widget grid (masonry-like layout)
│   │           ├── Card: CRT screen (iframe → Dwasm 2.1.1, Canvas-based)
│   │           ├── Card: Poetic Weather (iframe → Golden Gate Bridge photo + rain overlay)
│   │           ├── Card: Bike Battery (iframe → gauge at 67%, 40 miles left)
│   │           ├── Card: Radio Widget (iframe → FM 88.3, frequency dial, AM/FM toggle)
│   │           ├── Card: Music Player (album art + AMOUR - AVA2 + playback controls)
│   │           ├── Multiple empty/placeholder cards (dashed borders)
│   │           └── More cards extending beyond viewport (clipped)
│   │
│   └── Floating Input Bar (bottom-left)
│       ├── Toolbar: [+ Add image] [@ Select style]
│       ├── Editable area: placeholder "See endless designs for..."
│       └── Submit button (arrow icon, disabled when empty)
│
└── Alert region (for notifications)
```

## Extracted Computed Styles

### Body
```
background-color: rgb(34, 34, 34)    →  #222222
color: rgb(255, 255, 255)
font-family: Inter, "Inter Fallback", system-ui, sans-serif
```

### Heading (h1)
```
font-family: "Variant Neue Display", "Variant Neue Text", Inter, "Inter Fallback", system-ui, sans-serif
font-size: 32px
font-weight: 400
line-height: 36px
letter-spacing: 0.32px
color: (inherits --text-primary)
```

### Body Paragraphs (p)
```
font-size: 14px
line-height: 24px
color: rgba(240, 237, 229, 0.65)
```

### Pill Buttons
```
background: rgb(7, 7, 6)           →  #070706
color: rgb(240, 237, 229)          →  #f0ede5
border: 0.5px solid rgba(255, 255, 255, 0.1)
border-radius: 6px
padding: 0px 8px 0px 7px
font-size: 11px
```

### Main Grid Layout
```css
.HomepageV3_root {
  display: grid;
  grid-template-columns: 408px 708px;
  grid-template-rows: 884px;   /* = 100vh */
  width: 1116px;
}
```

### Widget Cards
```
border-radius: 8px
background: transparent (empty) or rgba(0,0,0,0) with content
```

Card dimension variants observed:
- 315 × 236 px
- 375 × 236 px
- 513 × 384 px
- 177 × 384 px
- 345 × 259 px
- 513 × 385 px
- 177 × 385 px

### Full Color Palette (extracted)
```
Backgrounds:
  #222222    rgb(34, 34, 34)         — body
  #1e1e1c    rgb(30, 30, 28)         — surface/panels
  #070706    rgb(7, 7, 6)            — deep/buttons

Text:
  #f0ede5    rgb(240, 237, 229)       — primary (headings)
  —          rgba(240, 237, 229, 0.9) — strong emphasis
  —          rgba(240, 237, 229, 0.65)— body copy
  —          rgba(240, 237, 229, 0.5) — captions
  —          rgba(255, 255, 255, 0.85)— input text
  —          rgba(255, 255, 255, 0.5) — disabled icons
  —          rgba(255, 255, 255, 0.4) — subtle icons

Borders:
  —          rgba(255, 255, 255, 0.1) at 0.5px — button/card borders
  —          rgba(255, 255, 255, 0.08) dashed  — placeholder cards (estimated)

Internal (iframe widgets may use their own palettes):
  #000000    rgb(0, 0, 0)            — inside widget iframes
```

### Custom Fonts
```
Font files loaded:
  /static/media/618b869efe759565-s.p.otf     (OTF, likely "Variant Neue Display")
  /static/media/c4b700dcb2187787-s.p.woff2   (WOFF2)
  /static/media/e4af272ccee01ff0-s.p.woff2   (WOFF2)
```
Fallback chain: "Variant Neue Display" → "Variant Neue Text" → Inter → "Inter Fallback" → system-ui → sans-serif

### Interactive Widget Details

**CRT Screen Widget**
- URL: /homepage-widgets/crt/crt.html
- Title: "Dwasm 2.1.1"
- Uses HTML5 Canvas for retro CRT effect
- Content appears to show weather/time text in monospace

**Poetic Weather Widget**
- URL: /homepage-widgets/poetic-weather/index.html
- Background: Golden Gate Bridge photograph in fog
- Overlay: Rain drop animations (50+ div elements)
- Bottom: "San Francisco" label with icon
- Moody, atmospheric aesthetic

**Bike Battery Widget**
- URL: /homepage-widgets/bike-battery/bike-battery.html
- Displays: 67% charge, 40 MILES LEFT
- Stats: LAST CHARGE TODAY 8:30 AM, TOTAL RANGE 60 MILES
- Battery bar visualization with vertical segments
- Action button: "Stop Charging" (pressed state)
- Dark UI with cyan/teal accent on battery indicator

**Radio Widget**
- URL: /homepage-widgets/radio-widget/index.html
- Frequency: 88.3 FM, CHANNEL: MAIN FM
- Frequency dial with markers (83.5 through 105.9)
- Canvas element for waveform visualization
- Toggle: AM / FM buttons
- Retro-modern radio interface design

**Music Player Widget**
- Visible in scrolled view
- Track: "AMOUR - AVA2"
- "CMINOR - 140 BPM" tag
- Circular album art with magenta/pink gradient glow
- Playback controls: prev, play, next

## Design Principles (Inferred)

1. **Warm darks over pure blacks** — #222 body, #070706 surfaces, never #000
2. **Warm off-whites over pure whites** — #f0ede5 text, never #fff
3. **Ultra-subtle borders** — 0.5px at 10% opacity, barely perceptible
4. **Light-weight headlines** — 400 weight, not bold; italic for emphasis
5. **Interactive > static** — Live Canvas/iframe widgets, not screenshots
6. **Asymmetric grid** — Mixed card sizes create visual rhythm
7. **Viewport-contained** — Full 100vh, no traditional page scrolling
8. **Ambient animation** — Rain drops, waveforms, gauges; subtle continuous motion
9. **Minimal chrome** — No navigation bar, no footer, no decorative elements
10. **Single focal point** — Hero text left, showcase right, input bar anchored

## Technical Stack (Observed)

- Framework: Next.js (React Server Components, RSC payload)
- Styling: CSS Modules (`.HomepageV3_root__3pGZA` naming)
- Fonts: Custom "Variant Neue" + Inter
- Widgets: Self-contained HTML/CSS/JS in iframes
- Canvas: Used for CRT effects, radio waveforms
- Rich text input: TipTap editor for the prompt input
