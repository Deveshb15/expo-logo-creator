# Icon Theme System

Use this file whenever you need to derive icon colors from a target app. The goal is to convert repo colors into one disciplined `IconTheme` so the icon feels intentional instead of randomly colorful.

## Source priority

Use the first strong source you can find:

1. App theme tokens or design system colors
2. `app.json` / `app.config.*` splash and scheme colors
3. Shared UI constants or brand color exports
4. Existing logo or icon colors already in the repo
5. Fallback themes from `references/color-palettes.md`

Do not mix unrelated sources unless the repo clearly does.

## Required token set

| Token | Purpose | Rule |
|------|---------|------|
| `brand.primary` | dominant brand hue | Must come from the app when possible |
| `brand.secondary` | optional support hue | Use only if the app already has one or the theme needs a closely related accent |
| `bg.gradientStart` | top-left or lighter background stop | Mid-to-bright version of the background hue |
| `bg.gradientEnd` | bottom-right or darker background stop | Darker partner to `bg.gradientStart` |
| `fg.primaryFill` | main motif fill | Usually very light so it separates from the background |
| `fg.secondaryFill` | secondary motif fill or internal highlight | Use for layered shapes, supporting motifs, or inner fills |
| `accent.glow` | ambient glow color | Same hue family as the rest of the icon, never unrelated neon |
| `accent.shadow` | shadow/filter color | Darkest color in the system |
| `detail.stroke` | outlines, faces, edge details | Dark enough to stay visible on `fg.primaryFill` |
| `mono.fill` | monochrome icon fill | Always `#FFFFFF` |
| `text.fontFamily` | icon text font family | Prefer repo font, otherwise safe fallback |
| `text.fontWeight` | icon text weight | Usually `600` to `800` |
| `text.fontFiles` | local font files for rendering | Optional, but required when using repo-only custom fonts in Resvg |
| `text.allowed` | whether icon text is allowed | Must be decided using `references/typography-rules.md` |

## Theme-building workflow

### 1. Pick the hue family

- Choose one dominant brand hue from the repo.
- Add a secondary hue only if the product already uses it or if it is a close tonal companion.
- Prefer adjacent or analogous support colors over clashing complements unless the brand already uses high contrast.

### 2. Build the background

- `bg.gradientStart` and `bg.gradientEnd` should feel like the same family, not two separate palettes.
- The stops should be visibly different, usually by a noticeable lightness step rather than a hue jump.
- If the app's primary color is already dark, keep the background dark and make the motif lighter instead of washing out the whole palette.

### 3. Build the motif fills

- `fg.primaryFill` should clearly separate from the background at small sizes.
- Favor very light, slightly tinted fills for cute or dimensional motifs.
- `fg.secondaryFill` should support the primary motif without collapsing into the background.
- If the background is pale, flip the strategy: use a darker motif and keep `detail.stroke` even darker.

### 4. Build effects and detail colors

- `accent.glow` should be brighter or softer than the background, but still in the same color family.
- `accent.shadow` should be the darkest value in the set.
- `detail.stroke` should never be close in lightness to `fg.primaryFill`; it exists to preserve structure at small sizes.

## Structural rules

- Use one dominant hue family plus at most one support hue.
- Reserve the highest saturation for small accents, not for every large surface.
- Keep backgrounds simpler than motifs.
- Use the same hue family across gradient, glow, and shadow unless the brand strongly suggests otherwise.
- Do not introduce a surprise accent color just to make the icon "pop."

## Validation rules

Before drawing, check:

- Background and motif do not share the same lightness band.
- Glow is visible but does not overpower the silhouette.
- Stroke and face details remain readable on the motif.
- The monochrome silhouette does not depend on gradient contrast or glow to read correctly.
- Small decorative elements do not require unique colors to make sense.

## Quick heuristics

- If the icon feels muddy, reduce the number of hues before increasing contrast.
- If the icon feels flat, increase lightness separation between background and motif before adding more glow.
- If details disappear, darken `detail.stroke` or simplify the motif.
- If the palette feels off-brand, go back to repo sources instead of tweaking fallback colors by feel.

## Example mapping

If the repo exposes:

- primary brand color: `#2EC4B6`
- supporting accent: `#6EDDD2`

A coherent theme could be:

| Token | Value |
|------|-------|
| `brand.primary` | `#2EC4B6` |
| `brand.secondary` | `#6EDDD2` |
| `bg.gradientStart` | `#2EC4B6` |
| `bg.gradientEnd` | `#1A9E8F` |
| `fg.primaryFill` | `#F2FFFC` |
| `fg.secondaryFill` | `#D4F5F0` |
| `accent.glow` | `#6EDDD2` |
| `accent.shadow` | `#0A2E2A` |
| `detail.stroke` | `#1A7A6E` |
| `mono.fill` | `#FFFFFF` |

The exact values can move, but the structure should remain stable.
