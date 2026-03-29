---
name: expo-logo-creator
description: >
  Generate beautiful illustrated SVG app icons for Expo and React Native projects.
  Creates all required icon assets (iOS, Android adaptive, monochrome, splash,
  favicon) from hand-crafted SVG source files while reusing the target app's color
  theme and typography when appropriate.
license: MIT
metadata:
  author: Deveshb15
  version: "1.1.0"
---

# Expo Logo Creator

Create illustrated SVG icon systems for Expo and React Native apps. Prioritize brand consistency, legibility, and platform correctness over novelty. Every icon must be grounded in the target repo's product purpose, color system, and typography before any SVG is drawn.

## Workflow

### 1. Ground in the app

Read the repo before making design choices:

1. Read `app.json` or `app.config.*` and extract:
   - `expo.name`, `expo.slug`, existing icon paths, splash config, and scheme
2. Read `package.json` and infer app purpose from dependencies
3. Read `README`, `CLAUDE.md`, or equivalent product docs to understand audience and tone
4. Search for brand colors and tokens:
   - `theme*.{ts,tsx,js,jsx}`
   - `colors*.{ts,tsx,js,jsx}`
   - `tokens*.{ts,tsx,js,jsx,json}`
   - `constants/Colors*`
   - any design-system or UI package exports
5. Search for typography and font assets:
   - `expo-font`, `useFonts`, `Font.loadAsync`
   - `fontFamily`, `fontWeight`, `typography`, `textVariants`
   - `assets/fonts`, `fonts/`, or custom font folders
6. Note whether the app already uses an initial, symbol, mascot, or other recognizable brand cue

Ask the user only if the app purpose or brand direction is still unclear after inspection.

### 2. Build an `IconTheme` before sketching

Before motif selection, read:
- `references/theme-system.md`
- `references/color-palettes.md`
- `references/typography-rules.md`

Normalize the repo findings into this internal theme brief:

```txt
IconTheme
- brand.primary
- brand.secondary
- bg.gradientStart
- bg.gradientEnd
- fg.primaryFill
- fg.secondaryFill
- accent.glow
- accent.shadow
- detail.stroke
- mono.fill
- text.fontFamily
- text.fontWeight
- text.fontFiles (optional)
- text.allowed
```

Rules:
- Follow the precedence in `references/theme-system.md`: app theme tokens first, then Expo config colors, then shared constants, then fallback palettes
- Reuse the app's actual brand hues when they exist
- Keep the icon to one dominant hue family plus at most one support hue unless the product already uses a broader palette
- Derive glow, shadow, stroke, and foreground fills from the brand colors instead of inventing unrelated accents
- If the app has no usable brand colors, choose a fallback theme from `references/color-palettes.md` and map it into the same token structure
- If the app uses custom fonts and the font files are discoverable, store those file paths in `text.fontFiles`
- If no usable app font is discoverable, use the safe fallback chain from `references/typography-rules.md`

Record a short internal note saying where the theme came from, for example:
- `brand.primary` from `theme/colors.ts`
- `text.fontFamily` from `useFonts()` in `app/_layout.tsx`

### 3. Run a design preflight

Do not start SVG authoring until all of these are true:

- The primary motif matches the app's purpose, not a generic cute default
- `bg.gradientStart` and `bg.gradientEnd` are visibly distinct
- The primary motif fill will separate clearly from the background at favicon size
- `detail.stroke` is dark or saturated enough to stay visible on the motif
- `accent.glow` and `accent.shadow` stay inside the same color family as the rest of the icon
- The composition can fit inside the Android safe zone
- `text.allowed` is `true` only if `references/typography-rules.md` allows it
- The monochrome silhouette will still read clearly without glow, gradients, or decorative text

If any item fails, revise `IconTheme` first.

### 4. Choose motif and composition

Read `references/motif-catalog.md` after the theme brief is ready.

Motif rules:
- Never default to moon/cloud unless the app is actually about sleep, weather, or a related calm motif
- Choose 1 primary motif that directly matches the app category
- Choose 1-2 supporting motifs only if they improve recognition
- Choose 0-2 decorative elements only if they support the theme without cluttering the silhouette

Composition rules:
- Primary motif is large and centered or slightly above center
- Supporting motifs are smaller and should not compete with the primary
- Decorative elements stay in negative space and never define the silhouette
- Keep critical shapes inside the Android safe zone described in `references/expo-icon-spec.md`

Typography rules:
- Text is optional and should be rare
- Only use text when `text.allowed` is `true`
- Reuse the app's own font family when possible
- Limit icon text to short, legible glyphs such as an initial, `z`, a currency symbol, or cardinal letters
- Do not add decorative words or slogans

### 5. Create the SVG files

Read:
- `references/svg-techniques.md`
- `references/expo-icon-spec.md`

Create all 4 SVG source files in `assets/svg/`:

#### `icon-full.svg`

- Use `bg.gradientStart` -> `bg.gradientEnd` for the rounded background
- Use `fg.primaryFill`, `fg.secondaryFill`, `accent.glow`, `accent.shadow`, and `detail.stroke` consistently across the motif
- Use faces or line details only if they improve clarity
- Use text only if `text.allowed` is `true`, and apply `text.fontFamily` / `text.fontWeight`

#### `icon-foreground.svg`

- Same illustration as `icon-full.svg`
- No background rect
- Preserve only effects that still work on transparency

#### `icon-background.svg`

- Background only
- No rounded corners
- Use only the background gradient tokens

#### `icon-monochrome.svg`

- Transparent background
- Use only `fill="white"` or the equivalent `mono.fill`
- No gradients, filters, opacity variation, face details, or decorative text
- Preserve the cleanest recognizable silhouette of the icon

### 6. Generate PNGs

Follow `references/png-generation.md`.

If the icon uses a repo font:
- Pass the discovered font file paths to Resvg so text renders correctly
- Keep `loadSystemFonts: true` for fallback coverage

After generation:
- remove any temporary script file
- uninstall `@resvg/resvg-js` if it was added only for one-off generation

### 7. Update Expo config

Update `app.json` or `app.config.*` with:
- `expo.icon`
- `expo.ios.icon`
- `expo.android.adaptiveIcon.foregroundImage`
- `expo.android.adaptiveIcon.backgroundImage`
- `expo.android.adaptiveIcon.monochromeImage`
- `expo.web.favicon`

If `expo-splash-screen` is installed, update the splash icon/background to match the new icon system.

### 8. Final validation checklist

Before finishing, verify:

- [ ] All 4 SVG files exist in `assets/svg/`
- [ ] All 6 PNG files exist in `assets/images/`
- [ ] Expo config points at the generated PNGs
- [ ] The foreground SVG has no background fill
- [ ] The monochrome SVG uses only white shapes on transparency
- [ ] The primary motif stays readable at 48px
- [ ] The composition stays inside the Android safe zone
- [ ] `detail.stroke` remains visible against the motif fill
- [ ] No unrelated accent hue was introduced without a source in the app or fallback theme
- [ ] Any text uses the repo font or the documented fallback chain
- [ ] Any custom font used in SVG text is also supplied to Resvg during PNG generation
- [ ] Temporary generation files were removed

## Handling refinement requests

When the user asks for adjustments:

- **"Change the color"**: update `IconTheme` first, then propagate the revised tokens through all 4 SVGs and regenerate PNGs
- **"Make it bigger/smaller"**: apply the scaling rules from `references/svg-techniques.md` to every absolute coordinate, radius, and stroke width
- **"Text doesn't feel right"**: re-run the typography rules, confirm the font source, and remove text entirely if it is not helping
- **"Face/details aren't visible"**: darken `detail.stroke` or increase stroke width and opacity
- **"Add more sparkle"**: add only if the silhouette remains clear and the extra accents still fit the theme
- **After any SVG change**: always regenerate the PNG outputs
