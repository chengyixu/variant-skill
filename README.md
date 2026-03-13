# variant-website

An agent skill that captures the design language of [variant.com](https://variant.com/) — a warm-dark, ultra-refined aesthetic with interactive widget showcases, subtle borders, and clean typography.

## What This Skill Does

When invoked, it gives your AI coding agent the complete design system to build websites in variant.com's style:

- **Warm-dark color palette** (`#222222` body, `#f0ede5` text — never pure black/white)
- **Ultra-subtle borders** (0.5px at 10% opacity)
- **Light-weight Inter typography** (400 weight headlines, italic emphasis)
- **Two-column grid layout** (hero left, masonry widget showcase right)
- **Interactive widget cards** with Canvas animations
- **Floating input bar** at bottom-left
- **Quick-start HTML template** ready to customize

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
├── SKILL.md                    # Design system, components, quick-start template
└── references/
    └── REFERENCE.md            # Exhaustive extracted specs from variant.com
```

## How It Was Made

1. **[webskills](https://github.com/kstonekuan/webskills)** — attempted content extraction (variant.com is fully client-rendered Next.js, so the HTML fallback captured RSC payload)
2. **[browser-use](https://docs.browser-use.com/cloud/guides/skills) pattern** — used chrome-devtools to navigate the live site, capture screenshots, extract the full DOM tree, and pull every computed CSS style
3. **Combined both** into a structured agent skill with design tokens, layout specs, component patterns, and a ready-to-use HTML template

## Compatibility

Works with any agent that supports the [Agent Skills](https://agentskills.io/) standard, including:

Claude Code, Cursor, GitHub Copilot, Windsurf, Cline, Gemini CLI, Codex, and 20+ more.

## License

MIT
