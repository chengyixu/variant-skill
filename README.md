# variant-website

A comprehensive agent skill that captures the **complete multi-aesthetic design system** of [variant.com](https://variant.com/) — 10+ distinct design styles across 15+ interactive widgets, all extracted from live source code.

## What This Skill Does

When invoked, it gives your AI coding agent the complete design system to build websites in ANY of variant.com's styles:

- **80+ CSS variables** — warm-dark shell, never pure black/white
- **10+ design aesthetics** — dark minimal, retro CRT, atmospheric photo, vibrant stickers, retro radio, robot mascot, fintech card, scribble art, music player, editorial
- **Full widget CSS** — extracted from live source via Jina r.reader API
- **WebGL shaders** — battery energy pulse, holographic sticker sheen
- **Advanced CSS** — squircle clip-paths, mechanical counter animations, 3D perspective flips
- **Shimmer dashed borders** — SVG-masked gradient with stroke-dasharray
- **25 animations** — including rain, typewriter, digit rolling, radar sweep
- **Quick-start HTML template** — production-ready variant.com homepage clone

## Install

### With [skills CLI](https://github.com/anthropics/skills)

```bash
npx skills add chengyixu/variant-website --global
```

### With [webskills CLI](https://github.com/kstonekuan/webskills)

```bash
npx webskills-cli add https://github.com/chengyixu/variant-website --global
```

### Manual

Copy the `SKILL.md` and `references/` directory into your agent's skills folder:

```bash
# Claude Code
cp -r . ~/.claude/skills/variant-website

# Or any agent that follows the skills standard
cp -r . ~/.agents/skills/variant-website
```

## Files

```
variant-website/
├── SKILL.md                    # Complete multi-aesthetic design system + HTML template
└── references/
    ├── REFERENCE.md            # Full DOM structure, computed styles, widget catalog
    ├── WIDGETS.md              # Complete widget source CSS/JS from Jina extraction
    └── CSS_SYSTEM.md           # All 80+ CSS variables, 25 animations, gradients
```

## How It Was Made

1. **[Jina r.reader API](https://jina.ai/reader/)** — scraped full rendered HTML/CSS/JS from all 14 widget URLs using `X-Engine: browser` for JS-heavy pages
2. **[chrome-devtools MCP](https://github.com/nicobailey/chrome-devtools-mcp)** — navigated the live site, captured 15+ screenshots at different scroll positions, extracted the full DOM tree and every computed CSS style (630+ rules, 151 classes)
3. **[webskills CLI](https://github.com/kstonekuan/webskills)** — initial page structure extraction
4. **Combined all three** into a comprehensive agent skill with 10+ design aesthetics, actual source CSS from each widget, and a production-ready HTML template

## Compatibility

Works with any agent that supports the [Agent Skills](https://agentskills.io/) standard, including:

Claude Code, Cursor, GitHub Copilot, Windsurf, Cline, Gemini CLI, Codex, and 20+ more.

## License

MIT
