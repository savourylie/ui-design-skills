# claude-skills

A plugin marketplace for Claude Code that extracts design systems from UI screenshots and generates platform-native theme files for web and mobile.

## Overview

This repository provides three Claude Code skills that form a complete **extract → review → apply** workflow for design systems:

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

```
/plugin marketplace add savourylie/claude-skills
/plugin install design-system-skills@claude-skills
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
├── README.md
├── LICENSE
└── skills/
    ├── design-system-extractor/
    │   ├── SKILL.md              # Skill definition and workflow
    │   ├── scripts/
    │   │   └── validate_tokens.py
    │   └── references/
    │       ├── token-schema.md   # Shared token JSON schema
    │       ├── extraction-guide.md
    │       └── example-output.md
    ├── design-system-web-applier/
    │   ├── SKILL.md
    │   ├── scripts/
    │   │   └── generate_css.py
    │   └── references/
    │       ├── token-schema.md
    │       ├── css-variables.md
    │       ├── tailwind-config.md
    │       └── react-theme.md
    └── design-system-mobile-applier/
        ├── SKILL.md
        ├── scripts/
        │   ├── generate_swift.py
        │   └── generate_kotlin.py
        └── references/
            ├── token-schema.md
            ├── ios-swiftui.md
            ├── ios-uikit.md
            ├── android-compose.md
            ├── android-xml.md
            ├── flutter.md
            └── react-native.md
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

- [Agent Skills Spec](https://docs.anthropic.com/en/docs/claude-code/skills)
- [Plugin Marketplace](https://docs.anthropic.com/en/docs/claude-code/plugins)

## License

MIT
