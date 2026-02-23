# claude-skills

Design system skills for Claude Code. Extract design tokens from UI screenshots and generate platform-native theme files for web and mobile.

## Installation

```
/plugin marketplace add savourylie/claude-skills
/plugin install design-system-skills@claude-skills
```

## Included Skills

| Skill | Description |
|-------|-------------|
| **design-system-extractor** | Extract structured design tokens (colors, typography, spacing, shadows) from UI screenshots into a Markdown + JSON artifact. |
| **design-system-web-applier** | Generate web theme files from design tokens — CSS custom properties, SCSS variables, Tailwind config, React themes (styled-components/Emotion/Chakra), CSS Modules, or Vue 3 composables. |
| **design-system-mobile-applier** | Generate mobile theme files from design tokens — iOS (SwiftUI/UIKit), Android (Compose/XML), Flutter (ThemeData), or React Native (theme.ts). |

## Workflow

1. Provide one or more UI screenshots to the **extractor** skill
2. Review the generated design token JSON
3. Use the **web applier** or **mobile applier** to generate theme files for your target stack

## Links

- [Agent Skills Spec](https://docs.anthropic.com/en/docs/claude-code/skills)
- [Plugin Marketplace](https://docs.anthropic.com/en/docs/claude-code/plugins)

## License

MIT
