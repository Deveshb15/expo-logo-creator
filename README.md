# expo-logo-creator

A Claude Code skill that generates beautiful, illustrated SVG app icons for Expo and React Native projects.

## What it does

When you ask Claude to create a logo for your Expo app, this skill:

1. **Reads your codebase** to understand your app's purpose, brand colors, and theme
2. **Designs a unique illustrated icon** with motifs tailored to your app category (not a generic template)
3. **Creates 4 SVG source files** with gradients, masks, shadows, and cute illustrations
4. **Generates 6 PNG files** for all platforms (iOS, Android adaptive, monochrome, splash, favicon)
5. **Updates app.json** with the correct icon paths

## Installation

```bash
npx skills add Deveshb15/expo-logo-creator
```

## Usage

Open your Expo project in Claude Code and ask:

```
Create a logo for my app
```

Claude will analyze your project, choose appropriate motifs and colors, and generate a complete icon set.

### Refinement

After the initial generation, you can ask for adjustments:

- "Make the icon bigger"
- "Change the color to blue"
- "The face details aren't visible enough"
- "Add more sparkle effects"

## What gets generated

```
assets/
├── svg/                              # Editable vector source files
│   ├── icon-full.svg                 # Complete icon (iOS)
│   ├── icon-foreground.svg           # Android adaptive foreground
│   ├── icon-background.svg           # Android adaptive background
│   └── icon-monochrome.svg           # Android 13+ themed icon
└── images/                           # Ready-to-use PNGs
    ├── icon.png                      # 1024x1024 (iOS)
    ├── android-icon-foreground.png   # 1024x1024
    ├── android-icon-background.png   # 1024x1024
    ├── android-icon-monochrome.png   # 1024x1024
    ├── splash-icon.png              # 512x512
    └── favicon.png                   # 48x48
```

## Supported app categories

The skill includes motifs for: Sleep/Wellness, Fitness/Health, Finance, Social/Chat, Productivity, Food/Cooking, Music/Audio, Travel/Maps, Education, Photography, Weather, Shopping, Gaming, Meditation, and more.

## License

MIT
