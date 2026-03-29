# expo-logo-creator

A Claude Code skill for generating illustrated Expo and React Native app icons that stay aligned with the target app's brand colors, typography, and platform constraints.

## What it does

When you ask Claude to create a logo for your Expo app, this skill:

1. Reads your codebase to understand the app's purpose, theme tokens, and fonts
2. Builds an internal `IconTheme` so background, motif, glow, shadow, and detail colors all come from one coherent palette
3. Reuses app fonts when text is actually warranted and renderable
4. Creates 4 SVG source files for iOS, Android adaptive, and monochrome icons
5. Generates 6 PNG files for iOS, Android, splash, and web
6. Updates Expo icon config paths

## Installation

```bash
npx skills add Deveshb15/expo-logo-creator
```

## Usage

Open your Expo project in Claude Code and ask:

```text
Create a logo for my app
```

The skill will inspect the repo first, derive a theme from your existing brand colors, check which fonts are actually available, and then generate a complete icon set.

### Refinement

After the initial generation, you can ask for adjustments such as:

- "Make the icon bigger"
- "Use our teal palette instead of the blue one"
- "Remove the text and keep it purely symbolic"
- "The details disappear at small sizes"

## What gets generated

```text
assets/
├── svg/
│   ├── icon-full.svg
│   ├── icon-foreground.svg
│   ├── icon-background.svg
│   └── icon-monochrome.svg
└── images/
    ├── icon.png
    ├── android-icon-foreground.png
    ├── android-icon-background.png
    ├── android-icon-monochrome.png
    ├── splash-icon.png
    └── favicon.png
```

## Design goals

- Reuse the app's real color theme before falling back to curated palettes
- Keep icons legible at favicon size
- Avoid generic motifs that do not match the product
- Keep Android monochrome icons clean and recognizable
- Use decorative text only when the repo font and icon concept genuinely support it

## Supported app categories

The skill includes motif guidance for sleep and wellness, fitness and health, finance, social and chat, productivity, food, music, travel, education, photography, weather, shopping, gaming, meditation, and generic branded initials or symbols.

## License

MIT
