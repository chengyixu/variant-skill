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

## Shimmer Dashed Border Effect (Signature Visual)

The grid tiles use a distinctive dashed-border shimmer effect created via:

```css
/* Each grid tile has an ::after pseudo-element */
.grid-item::after {
  position: absolute;
  inset: 0;
  border-radius: 8px;
  pointer-events: none;
  z-index: 1;
  /* Diagonal shimmer gradient */
  background-image: linear-gradient(135deg,
    rgba(255,255,255,0.22) 48%,
    rgba(255,255,255,0.55) 50%,
    rgba(255,255,255,0.22) 52%);
  background-size: 6700px 6700px;
  /* SVG mask creates the dashed rounded-rectangle */
  -webkit-mask-image: url("data:image/svg+xml,<svg>
    <rect stroke-dasharray='2 3' stroke-linecap='round'
          stroke-width='1' rx='8' ry='8' fill='none' stroke='white'/>
  </svg>");
}
```

The large `background-size: 6700px` means the shimmer gradient moves very slowly as the user scrolls, creating an elegant, understated light sweep across the grid.

## Virtual Scrolling System ("SquishyGrid")

- CSS class: `HomepageWidgetGrid_scrollHost__BG8W6`
- `overflow: hidden auto` on the scroll container
- Total scroll height: ~59,000–63,000px (effectively infinite)
- Grid items are **absolutely positioned via CSS `transform: matrix(1,0,0,1,tx,ty)`** — not CSS Grid/Flexbox
- Tiles are lazily loaded, recycled as user scrolls (virtual scrolling)
- ~32 tiles visible at any time; rows of 2–3 tiles
- Horizontal/vertical gap: 10px
- Total grid width per row: ~1020px at 1440px viewport

## Widget Loading States

```
shimmer (HomepageWidgetGrid_widgetShimmer__5Hs_Q) → blur placeholder
loaded  (HomepageWidgetGrid_widgetContentLoaded__62tva) → visible
hidden  (HomepageWidgetGrid_widgetContentHidden__1YFj8) → offscreen, recycled
```

Iframes use: `loading="lazy" sandbox="allow-scripts allow-same-origin"`

## Full Widget Catalog

| Widget | URL Path | Description |
|--------|----------|-------------|
| CRT/DOOM | `/homepage-widgets/crt/crt.html` | Physics-based CRT emulator, "Loading DOOM..." |
| Poetic Weather | `/homepage-widgets/poetic-weather/index.html` | Golden Gate Bridge + rain + "52 degrees" |
| Bike Battery | `/homepage-widgets/bike-battery/bike-battery.html` | 68% gauge, 40 miles left, charging controls |
| Radio | `/homepage-widgets/radio-widget/index.html` | FM 88.3, frequency dial, waveform canvas |
| Music Player | `/homepage-widgets/music-player/dist/index.html` | AMOUR - AVA2, circular album art, playback |
| Scribble Pad | `/homepage-widgets/scribble-pad/index.html` | Drawing canvas with colorful strokes |
| Stickers | `/homepage-widgets/stickers/stickers.html` | Retro/funky sticker collection |
| Card | `/homepage-widgets/card/card.html` | Credit card with flip/freeze/add cash |
| Text Editor | `/homepage-widgets/text-editor-widget/...` | Rich text with B/I/U/List toolbar |
| Robot | `/homepage-widgets/robot-widget/index.html` | LED robot face with emoji reactions |
| Movie Rating | `/homepage-widgets/movie-rating-app/...` | Film rating interface |
| Video Player | `/homepage-widgets/video-player/dist/index.html` | Media playback |
| Voice Recorder | `/homepage-widgets/voice-recorder-variant/...` | Audio recording interface |
| Infinite Gallery | `/homepage-widgets/infinite-gallery/...` | Background grid rendering |
| Messaging | (inline) | Notification tabs: Variant(25), Family(12), Friends(99) |

## Sound Design

Preloaded audio files for interaction feedback:
- `Variant_Generate.wav` — played when generating designs
- `Variant_Explore_2.wav` — played when exploring/scrolling
- `Variant_Failed_2.wav` — played on errors

## SVG Animation Assets

Preloaded SVG sequences:
- `design-loader.svg`, `edit-loader.svg` — loading states
- `make.svg`, `inspiration.svg`, `inspecting.svg` — action states
- `make-button.svg` — submit button animation

## Input Bar Details

- CSS class: `HomepageInput_inputContainer__bsWQA`
- Background: `rgb(30, 30, 28)` (#1E1E1C)
- Border: `box-shadow: rgba(255,255,255,0.1) 0px 0px 0px 0.5px` (ring, not border)
- Border-radius: 10px
- Padding: `8px 8px 0px`
- Height: ~72px
- Rich text input: TipTap contenteditable
- Placeholder: "See endless designs for..." in `rgba(255,255,255,0.4)`
- Action row: [+ Add image] [@ Select style] [→ Submit (disabled when empty)]
- Hidden file input for image upload

## CSS Variables (from source)

```css
--color-primary-blue: #2688f9;
--color-secondary-blue: #3a86ff;
--color-accent-coral: rgb(248, 113, 113);
--color-accent-purple: rgba(107, 173, 255, 1);
```

## Design Principles (Inferred)

1. **Warm darks over pure blacks** — #070706 page bg, #222 outer body, never raw #000
2. **Warm off-whites over pure whites** — #f0ede5 text, never #fff
3. **Ultra-subtle borders** — 0.5px at 10% opacity via box-shadow rings, barely perceptible
4. **Shimmer dashed outlines** — SVG-masked gradient borders on empty tiles, signature visual
5. **Light-weight headlines** — 400 weight, not bold; italic for emphasis
6. **Interactive > static** — Live Canvas/iframe widgets, not screenshots
7. **Asymmetric grid** — Mixed card sizes create visual rhythm
8. **Viewport-contained** — Full 100vh, no traditional page scrolling
9. **Ambient animation** — Rain drops, waveforms, gauges; subtle continuous motion
10. **Minimal chrome** — No navigation bar, no footer, no decorative elements
11. **Single focal point** — Hero text left, showcase right, input bar anchored
12. **Sound design** — Audio feedback for key interactions

## Technical Stack (Observed)

- Framework: Next.js (React Server Components, RSC payload)
- Styling: CSS Modules (`.HomepageV3_root__3pGZA`, `.HomepageWidgetGrid_scrollHost__BG8W6`)
- Fonts: Custom "Variant Neue Display" + "Variant Neue Text" + Inter fallback
- Widgets: Self-contained HTML/CSS/JS in sandboxed iframes (`allow-scripts allow-same-origin`)
- Canvas: Used for CRT effects, radio waveforms, drawing pad
- Rich text input: TipTap editor for the prompt input
- Virtual scroll: Transform-based tile positioning with recycling
- Audio: Preloaded WAV files for interaction sounds
