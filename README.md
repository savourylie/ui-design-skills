# design-system-skills

Multi-platform agent skills that extract design systems from UI screenshots and generate platform-native theme files for web and mobile. Works with [Claude Code](https://docs.anthropic.com/en/docs/claude-code/skills), [Codex CLI](https://github.com/openai/codex), and [Antigravity](https://github.com/ArcadeLabsInc/antigravity) via the open [Agent Skills](https://agentskills.io) standard.

## Overview

This repository provides three agent skills that form a complete **extract → review → apply** workflow for design systems:

1. **Extract** design tokens (colors, typography, spacing, shadows) from one or more UI screenshots
2. **Review** the generated token JSON — a structured, platform-agnostic artifact
3. **Apply** tokens to your target stack, producing production-ready theme files for web or mobile

All three skills share a common [token schema](#token-schema), so the extractor's output plugs directly into either applier.

## Skills

| Skill | Description |
|-------|-------------|
| **design-system-extractor** | Analyzes UI screenshots to reverse-engineer design tokens (colors, typography, spacing, border radii, shadows, component patterns) into a structured Markdown + JSON artifact. |
| **design-system-web-applier** | Converts design token JSON into web theme files — CSS custom properties, SCSS variables, Tailwind config, React themes (styled-components / Emotion / Chakra UI), CSS Modules + TypeScript, or Vue 3 composables. |
| **design-system-mobile-applier** | Converts design token JSON into native mobile theme files — iOS (SwiftUI / UIKit), Android (Jetpack Compose / XML resources), Flutter (ThemeData), or React Native (theme.ts). |

## Installation

### Claude Code

```
/plugin marketplace add savourylie/claude-skills
/plugin install design-system-skills@claude-skills
```

### Codex CLI

Install skills directly from GitHub using `$skill-installer` inside Codex (no cloning required):

```
$skill-installer install https://github.com/savourylie/claude-skills/tree/main/skills/design-system-extractor
$skill-installer install https://github.com/savourylie/claude-skills/tree/main/skills/design-system-web-applier
$skill-installer install https://github.com/savourylie/claude-skills/tree/main/skills/design-system-mobile-applier
```

Restart Codex after installing to pick up the new skills.

Alternatively, clone this repo into your project or add it as a submodule — skills are discovered automatically from `.agents/skills/`:

```bash
git clone https://github.com/savourylie/claude-skills.git .claude-skills
# or
git submodule add https://github.com/savourylie/claude-skills.git .claude-skills
```

### Antigravity

Install skills directly from GitHub (no cloning required):

```bash
# Download skills and set up Antigravity discovery
curl -sL https://github.com/savourylie/claude-skills/archive/refs/heads/main.tar.gz \
  | tar xz --strip-components=1 -C /tmp claude-skills-main/skills
mkdir -p .agent/skills
for s in design-system-extractor design-system-web-applier design-system-mobile-applier; do
  cp -r /tmp/skills/$s .agent/skills/
done
rm -rf /tmp/skills
```

Or for global installation (available across all projects):

```bash
curl -sL https://github.com/savourylie/claude-skills/archive/refs/heads/main.tar.gz \
  | tar xz --strip-components=1 -C /tmp claude-skills-main/skills
mkdir -p ~/.gemini/antigravity/skills
for s in design-system-extractor design-system-web-applier design-system-mobile-applier; do
  cp -r /tmp/skills/$s ~/.gemini/antigravity/skills/
done
rm -rf /tmp/skills
```

Alternatively, clone the full repo into your workspace:

```bash
git clone https://github.com/savourylie/claude-skills.git .claude-skills
```

## Usage / Workflow

### 1. Extract tokens from screenshots

Provide one or more UI screenshots and invoke the **design-system-extractor** skill. It will analyze the visuals and produce a Markdown file with human-readable tables and a machine-readable JSON block.

### 2. Review the token artifact

Inspect the generated Markdown. Each token includes its value, usage context, and a confidence annotation. Edit any values that need adjustment before applying.

### 3. Apply tokens to your target stack

Pass the token JSON to the **web applier** or **mobile applier**. The skill auto-detects your project's stack (e.g., Tailwind, SwiftUI, Compose) and generates the appropriate theme files, or you can specify the target explicitly.

## Supported Platforms

### Web

- CSS custom properties
- SCSS variables
- Tailwind CSS config
- React (styled-components, Emotion, Chakra UI)
- CSS Modules + TypeScript
- Vue 3 composables

### Mobile

- iOS — SwiftUI extensions, UIKit constants
- Android — Jetpack Compose (MaterialTheme), XML resources
- Flutter — ThemeData
- React Native — theme.ts

## Project Structure

```
claude-skills/
├── .claude/
│   └── settings.local.json              # Claude Code settings
├── .claude-plugin/
│   └── marketplace.json                 # Claude Code plugin registry
├── .agents/
│   └── skills/                          # Codex CLI discovery (symlinks)
│       ├── design-system-extractor      -> ../../skills/design-system-extractor
│       ├── design-system-web-applier    -> ../../skills/design-system-web-applier
│       └── design-system-mobile-applier -> ../../skills/design-system-mobile-applier
├── .agent/
│   └── skills/                          # Antigravity discovery (symlinks)
│       ├── design-system-extractor      -> ../../skills/design-system-extractor
│       ├── design-system-web-applier    -> ../../skills/design-system-web-applier
│       └── design-system-mobile-applier -> ../../skills/design-system-mobile-applier
├── catalog.json                         # Antigravity skill catalog
├── skills/                              # Canonical skill definitions
│   ├── design-system-extractor/
│   │   ├── SKILL.md
│   │   ├── scripts/
│   │   └── references/
│   ├── design-system-web-applier/
│   │   ├── SKILL.md
│   │   ├── scripts/
│   │   └── references/
│   └── design-system-mobile-applier/
│       ├── SKILL.md
│       ├── scripts/
│       └── references/
├── README.md
└── LICENSE
```

## Token Schema

All three skills share a common JSON token format inspired by the W3C Design Tokens Community Group spec. The top-level structure:

```json
{
  "meta": {
    "name": "My Design System",
    "source": "Screenshots of example.com",
    "version": "1.0.0",
    "generated": "2025-01-15"
  },
  "color": {
    "primary": { "value": "#2563EB", "type": "color" },
    "background": { "value": "#FFFFFF", "type": "color" }
  },
  "typography": {
    "family": { "heading": { "value": "'Inter', sans-serif" } },
    "size": { "base": { "value": "16px" } }
  },
  "spacing": {
    "4": { "value": "16px" }
  },
  "borderRadius": {
    "md": { "value": "8px" }
  },
  "shadow": {
    "sm": { "value": "0 1px 2px rgba(0,0,0,0.05)" }
  },
  "components": { }
}
```

All values use platform-agnostic `px` units. The applier skills convert to the appropriate unit for each target (`rem`, `pt`, `dp`, `sp`, etc.).

See [`skills/design-system-extractor/references/token-schema.md`](skills/design-system-extractor/references/token-schema.md) for the full schema specification.

## Links

- [Agent Skills Standard](https://agentskills.io)
- [Claude Code Skills](https://docs.anthropic.com/en/docs/claude-code/skills)
- [Claude Code Plugin Marketplace](https://docs.anthropic.com/en/docs/claude-code/plugins)
- [Codex CLI](https://github.com/openai/codex)
- [Antigravity](https://github.com/ArcadeLabsInc/antigravity)

## License

MIT
