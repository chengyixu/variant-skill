# Variant.com — Complete CSS Design System (Extracted)

## CSS Custom Properties (Complete)

```css
:root {
  /* Layout */
  --max-width: 1100px;
  --border-radius: 12px;

  /* Typography */
  --font-mono: ui-monospace, Menlo, Monaco, "Cascadia Mono", "Segoe UI Mono", "Roboto Mono", "Oxygen Mono", "Ubuntu Monospace", "Source Code Pro", "Fira Mono", "Droid Sans Mono", "Courier New", monospace;

  /* Core Colors */
  --color-transparent: transparent;
  --color-white: white;
  --color-black: black;
  --color-gray-dark: #222222;
  --color-gray-medium: #363636;
  --color-gray-light: #dadada;
  --color-gray-lighter: #ccc;

  /* Brand Blues */
  --color-primary-blue: #2688f9;
  --color-secondary-blue: #3a86ff;
  --color-tertiary-blue: #3291ff;
  --color-accent-blue: rgb(59, 130, 246);
  --color-brand-blue: rgb(37, 99, 235);

  /* Status Colors */
  --color-success-green: green;
  --color-error-red: red;
  --color-warning-red: #f55c47;
  --color-warning-yellow: yellow;
  --color-info-blue: blue;

  /* Accent Colors */
  --color-accent-coral: rgb(248, 113, 113);
  --color-accent-purple: rgba(107, 173, 255, 1);

  /* Billing-specific */
  --color-billing-past-due-text: rgba(223, 99, 78, 1);
  --color-billing-past-due-bg: rgba(223, 99, 78, 0.18);
  --color-billing-past-due-border: rgba(223, 99, 78, 0.2);
  --color-billing-past-due-hover-bg: rgba(223, 99, 78, 0.12);
  --color-billing-modal-bg: rgba(167, 52, 32, 0.2);

  /* White Opacity Scale (16 steps!) */
  --color-white-90: rgba(255, 255, 255, 0.9);
  --color-white-85: rgba(255, 255, 255, 0.85);
  --color-white-80: rgba(255, 255, 255, 0.8);
  --color-white-70: rgba(255, 255, 255, 0.7);
  --color-white-50: rgba(255, 255, 255, 0.5);
  --color-white-40: rgba(255, 255, 255, 0.4);
  --color-white-30: rgba(255, 255, 255, 0.3);
  --color-white-20: rgba(255, 255, 255, 0.2);
  --color-white-15: rgba(255, 255, 255, 0.15);
  --color-white-10: rgba(255, 255, 255, 0.1);
  --color-white-08: rgba(255, 255, 255, 0.08);
  --color-white-07: rgba(255, 255, 255, 0.07);
  --color-white-06: rgba(255, 255, 255, 0.06);
  --color-white-05: rgba(255, 255, 255, 0.05);
  --color-white-04: rgba(255, 255, 255, 0.04);
  --color-white-03: rgba(255, 255, 255, 0.03);
  --color-white-full: rgba(255, 255, 255, 1);
  --color-white-none: rgba(255, 255, 255, 0);

  /* Black Opacity Scale (18 steps!) */
  --color-black-90: rgba(0, 0, 0, 0.9);
  --color-black-45: rgba(0, 0, 0, 0.45);
  --color-black-35: rgba(0, 0, 0, 0.35);
  --color-black-25: rgba(0, 0, 0, 0.25);
  --color-black-24: rgba(0, 0, 0, 0.24);
  --color-black-20: rgba(0, 0, 0, 0.2);
  --color-black-15: rgba(0, 0, 0, 0.15);
  --color-black-987: rgba(0, 0, 0, 0.987);
  --color-black-951: rgba(0, 0, 0, 0.951);
  --color-black-896: rgba(0, 0, 0, 0.896);
  --color-black-825: rgba(0, 0, 0, 0.825);
  --color-black-741: rgba(0, 0, 0, 0.741);
  --color-black-648: rgba(0, 0, 0, 0.648);
  --color-black-55: rgba(0, 0, 0, 0.55);
  --color-black-352: rgba(0, 0, 0, 0.352);
  --color-black-259: rgba(0, 0, 0, 0.259);
  --color-black-175: rgba(0, 0, 0, 0.175);
  --color-black-104: rgba(0, 0, 0, 0.104);
  --color-black-049: rgba(0, 0, 0, 0.049);
  --color-black-013: rgba(0, 0, 0, 0.013);
  --color-black-none: rgba(0, 0, 0, 0);

  /* Gray Variants */
  --color-gray-dark-80: rgba(34, 34, 34, 0.8);
  --color-gray-dark-full: rgba(34, 34, 34, 1);
  --color-gray-dark-none: rgba(34, 34, 34, 0);
  --color-gray-medium-75: rgba(61, 61, 61, 0.75);
  --color-gray-medium-90: rgba(33, 33, 33, 0.9);
  --color-gray-charcoal-95: rgba(48, 48, 48, 0.95);
  --color-gray-charcoal-85: rgba(22, 22, 22, 0.85);
  --color-gray-charcoal-50: rgba(8, 8, 8, 0.5);
  --color-gray-charcoal-90: rgba(8, 8, 8, 0.9);
  --color-gray-charcoal-none: rgba(8, 8, 8, 0);
  --color-gray-medium-40: rgba(80, 80, 80, 0.4);

  /* Hex variants with alpha */
  --color-gray-dark-hex-55: #22222288;
  --color-gray-dark-hex-65: #222222a6;
  --color-gray-medium-hex-65: #3a3a3aa6;
  --color-gray-medium-dark-65: #4e4e4ea6;
  --color-gray-darker-85: #0e0e0ed9;
  --color-gray-darkest-65: #131313a6;
  --color-gray-black-65: #030303a6;
  --color-white-hex-33: #ffffff55;
  --color-white-hex-13: #ffffff22;
  --color-white-hex-53: #ffffff88;

  /* Z-indices */
  --z-detail-view: 2010;
  --z-sidemodel: 2050;
  --z-panel: 2000;
  --z-sidebar: 2000;
  --z-stylemodal: 2100;
  --z-chat-topbar: 2005;
  --z-chat-topbar-left: 2025;
  --z-options-menu: 2020;
}
```

## Custom Font System (Complete)

### Variant Neue Display (Brand Typeface)
Based on Neue Haas Grotesk. 8 weights, each with italic:
- 100 (Thin)
- 200 (ExtraLight)
- 300 (Light)
- 350 (Book)
- 400 (Regular)
- 500 (Medium)
- 700 (Bold)
- 900 (Black)

Path: `/fonts/neue-haas-grotesk/variant-neue-display/VariantNeueDisplay-{weight}.woff2`

### Variant Neue Text (UI Typeface)
3 weights with italic:
- 400 (Regular)
- 500 (Medium)
- 700 (Bold)

Path: `/fonts/neue-haas-grotesk/variant-neue-text/VariantNeueText-{weight}.woff2`

### Inter (System Fallback)
Variable weight 100-900, normal + italic. Full unicode coverage with subset files.

## Keyframe Animations (25 total)

```css
/* Core shimmer */
@keyframes shimmer {
  0% { background-position: 100% 0; }
  100% { background-position: -100% 0; }
}

/* Grid loading shimmer */
@keyframes SquishyGrid_gridShimmer {
  0% { left: -100%; }
  100% { left: 100%; }
}

/* Widget card shimmer (one-shot) */
@keyframes HomepageWidgetGrid_widgetCardShimmerOnce {
  0% { transform: translate3d(-50%, -50%, 0) translate3d(-50%, 0, 0); }
  100% { transform: translate3d(-50%, -50%, 0) translate3d(50%, 0, 0); }
}

/* Empty grid shimmer sweep */
@keyframes ChatGridEmptyState_emptyGridShimmerTranslate {
  0% { transform: translateX(-100%); }
  100% { transform: translateX(100%); }
}

/* Tooltip entrance */
@keyframes tooltipEnterVertical {
  0% { opacity: 0; transform: scale(0.85); }
  100% { opacity: 1; transform: scale(1); }
}

/* Badge spawn */
@keyframes Sidebar_badgeSpawn {
  0% { opacity: 0; filter: blur(2px); transform: translate(calc(-50% + 8px), calc(-50% - 8px)) scale(0.8); }
  100% { opacity: 1; filter: blur(0); transform: translate(calc(-50% + 8px), calc(-50% - 8px)) scale(1); }
}

/* Reroll spin */
@keyframes CardIcons_spinReroll {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(-60deg); }
}

/* Style saved thumbnail */
@keyframes StyleModal_savedTopThumbnailEnter {
  0% { opacity: 0; transform: scale(0.65) rotate(0deg); }
  100% { opacity: 1; transform: scale(1) rotate(0deg); }
}

/* Style thumbnail shimmer sweep */
@keyframes StyleModal_savedTopThumbnailShimmer {
  0% { opacity: 0; transform: translateX(-100%) rotate(45deg); }
  5% { opacity: 1; }
  95% { opacity: 1; }
  100% { opacity: 0; transform: translateX(100%) rotate(45deg); }
}

/* Modal entrance */
@keyframes BillingModal_billingModalEnter {
  0% { opacity: 0; transform: scale(0.96); }
  100% { opacity: 1; transform: none; }
}

/* Shake */
@keyframes EditProfileModal_shake {
  0%, 100% { transform: translateX(0); }
  12.5% { transform: translateX(5px); }
  25% { transform: translateX(-5px); }
  50% { transform: translateX(-5px); }
  75% { transform: translateX(-3px); }
}

/* Slide down */
@keyframes PixelPortraitModal_slideDown {
  0% { transform: translateY(-20px); opacity: 0; }
  100% { transform: translateY(0); opacity: 1; }
}
```

## Signature Gradient Effects

### Card Overlay Gradient (Top Fade)
Used on design cards for icon overlay readability:
```css
background: linear-gradient(to bottom,
  var(--color-black) 0,
  var(--color-black-987) 8.1%,
  var(--color-black-951) 15.5%,
  var(--color-black-896) 22.5%,
  var(--color-black-825) 29%,
  var(--color-black-741) 35.3%,
  var(--color-black-648) 41.2%,
  var(--color-black-55) 47.1%,
  var(--color-black-45) 52.9%,
  var(--color-black-352) 58.8%,
  var(--color-black-259) 64.7%,
  var(--color-black-175) 71%,
  var(--color-black-104) 77.5%,
  var(--color-black-049) 84.5%,
  var(--color-black-013) 91.9%,
  var(--color-black-none) 100%);
```

### Dashed Border Shimmer (Homepage Grid)
```css
background-image: linear-gradient(135deg,
  rgba(255,255,255,0.22),
  rgba(255,255,255,0.22) 48%,
  rgba(255,255,255,0.55) 50%,
  rgba(255,255,255,0.22) 52%,
  rgba(255,255,255,0.22));
/* Applied via SVG mask with stroke-dasharray='2 3' */
```

### Widget Shimmer (Loading State)
```css
background: linear-gradient(135deg,
  rgba(255,255,255,0) 0%,
  rgba(255,255,255,0) 44%,
  rgba(255,255,255,0.008) 45.5%,
  rgba(255,255,255,0.02) 46.5%,
  rgba(255,255,255,0.05) 47.5%,
  rgba(255,255,255,0.09) 48.3%,
  /* ... peaks at 50% ... */
  rgba(255,255,255,0) 56%);
```

### Empty Grid Shimmer Sweep
```css
background: linear-gradient(135deg,
  rgba(255,255,255,0) 0%,
  rgba(255,255,255,0) 42%,
  rgba(255,255,255,0.35) 50%,
  rgba(255,255,255,0) 58%,
  rgba(255,255,255,0));
animation: 6s linear infinite;
```

### Bottom Fade on Grid
```css
background: linear-gradient(
  rgba(0,0,0,0) 0,
  rgba(0,0,0,0.06) 32%,
  rgba(0,0,0,0.2) 56%,
  rgba(0,0,0,0.45) 74%,
  rgba(0,0,0,0.72) 90%,
  rgb(0,0,0));
```

### Input Bar Bottom Gradient Fade
```css
background: linear-gradient(
  rgba(30,30,28,0) 0,
  rgba(30,30,28,0) 6px,
  rgba(30,30,28,0.1) 6.6px,
  rgba(30,30,28,0.24) 7.44px,
  rgba(30,30,28,0.44) 8.4px,
  rgba(30,30,28,0.64) 9.36px,
  rgba(30,30,28,0.82) 10.32px,
  rgba(30,30,28,0.94) 11.16px,
  rgb(30,30,28) 12px,
  rgb(30,30,28) 16px);
```

## Box Shadow Patterns

### Standard inset ring (ubiquitous)
```css
box-shadow: rgba(255, 255, 255, 0.1) 0px 0px 0px 0.5px inset;
```

### Floating composer (dramatic depth)
```css
box-shadow:
  rgba(255,255,255,0.1) 0 0 0 0.5px,
  rgba(0,0,0,0.1) 0 5px 11px,
  rgba(0,0,0,0.09) 0 20px 20px,
  rgba(0,0,0,0.05) 0 44px 26px,
  rgba(0,0,0,0.01) 0 78px 31px,
  rgb(0,0,0) 0 122px 34px;
```

### Dropdown menus
```css
background: rgba(68, 68, 68, 0.65);
backdrop-filter: blur(15px);
border-radius: 10px;
box-shadow: color(display-p3 0 0 0 / 0.03) 0px 8px 20px;
```

### Avatar active
```css
box-shadow: 0 0 0 .5px var(--color-white-10), 0 0 0 2px rgba(255,255,255,.2);
```

## Component Architecture

### App Layout
```
Sidebar (52px fixed left) + Container (flex: 1)
  → Topbar (52px sticky top)
  → GridWrapper (flex: 1, scrollable)
    → SquishyGrid (virtual scroll, transform-positioned items)
  → GlobalComposer (fixed bottom, centered, 520px max)
```

### Sidebar: 52px wide, fixed, icons only, no text
### Topbar: 52px tall, editable title, dropdown menu
### Grid: 4-column preview layout, 8px radius cards, 0.5px inset rings
### GlobalComposer: Floating input bar, 520px max-width, backdrop-blur(25px)
### StyleModal: 240x204px, backdrop-blur(24px), searchable style picker
### Dropdown Menus: 216px wide, backdrop-blur(15px), hover indicator animation

## Display-P3 Color Space Usage

Variant uses wide-gamut colors via `color(display-p3 ...)` with fallbacks:
```css
border: 0.5px solid color(display-p3 1 1 1 / 0.1);
background: color(display-p3 1 1 1 / 0.04);
/* With @supports fallback for sRGB displays */
```

## Toast Notifications
```css
backdrop-filter: blur(20px);
background: rgba(0, 0, 0, 0.85);
border-radius: 8px;
padding: 12px 14px;
font-size: 13px;
box-shadow: 0 0 0 1px rgba(255,255,255,...);
```

## Scrollbar Styling
```css
scrollbar-width: thin;
scrollbar-color: rgba(255,255,255,0.18) transparent;
/* WebKit */
::-webkit-scrollbar { width: 8px; }
::-webkit-scrollbar-track { background: transparent; }
::-webkit-scrollbar-thumb {
  background: content-box rgba(255,255,255,0.18);
  border-radius: 999px;
  border: 2px solid transparent;
}
::-webkit-scrollbar-thumb:hover {
  background: content-box rgba(255,255,255,0.28);
}
```

## Easing Functions
```css
/* Primary easing */
cubic-bezier(0.175, 0.885, 0.32, 1)   /* used for layout transitions */
cubic-bezier(0.19, 1, 0.22, 1)         /* used for container transitions */

/* Standard durations */
0.1s  — hover indicators
0.16s — button states, title blur
0.18s — image load opacity
0.2s  — border-color, background-color transitions
0.3s  — container transitions
0.4s  — layout margin/width shifts
6s    — shimmer sweep animations
```
