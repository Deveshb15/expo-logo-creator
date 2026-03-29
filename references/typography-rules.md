# Typography Rules

Use this file when the icon concept includes letters, symbols, or text-like decorative elements. Typography in an app icon should be rare, deliberate, and renderable.

## Font discovery

Search the target repo for:

- `expo-font`
- `useFonts`
- `Font.loadAsync`
- `fontFamily`
- `fontWeight`
- `typography`
- `textVariants`
- `assets/fonts`
- `fonts/`

Capture both:

- the font family name used in code
- the actual local font file paths when custom fonts are bundled with the app

If the repo uses a custom font but the actual font files cannot be found, do not assume Resvg can render it.

## Font selection order

1. A clearly branded display or heading font used by the app and backed by discoverable font files
2. The app's default sans or UI font if it is clean and legible
3. Safe fallback chain only when no suitable app font exists:
   - `Avenir Next, Avenir, Futura, Helvetica Neue, sans-serif`

Use only one font family per icon.

## When text is allowed

Set `text.allowed = true` only if all of these are true:

- The motif genuinely benefits from text or a symbol
- The text is short: usually one glyph, one initial, repeated `z`, a currency sign, or a tiny set of directional letters
- The font is legible at 48px output size
- The font can actually be rendered in Resvg:
  - system font available, or
  - local font files supplied through `fontFiles`

## When text should be removed

Set `text.allowed = false` if any of these apply:

- The icon already reads clearly without text
- The app font is thin, condensed, decorative, or script-heavy
- The text would need more than a few glyphs
- The symbol is not central to app recognition
- The exact brand font cannot be rendered correctly
- The monochrome icon would rely on text to stay recognizable

When in doubt, remove text and strengthen the motif instead.

## Rendering rules

- Prefer `font-weight` between `600` and `800`
- Keep text fill simple and high-contrast
- Use `text-anchor="middle"` and `dy="0.35em"` for centered text snippets
- If using a repo font, pass the corresponding font files to Resvg in `font.fontFiles`
- Keep `loadSystemFonts: true` enabled so fallbacks still work
- If exact lettering is essential and Resvg cannot load the font, convert the lettering to SVG paths instead of hoping the fallback matches

## Motif-specific guidance

- Compass labels: only use `N`, `S`, `E`, `W` if they materially help the motif; simple ticks are often cleaner
- Currency or product symbols: use only when the app identity is strongly tied to the symbol
- Floating `z` or similar accents: only use when the font feels native to the app and the effect does not become the main subject
- App initials: use only when the app already brands itself with the initial

## Sanity checks

Before keeping text in the icon, confirm:

- The text still reads after downscaling
- The font style matches the app's brand personality
- The glyph shapes do not create rendering artifacts at small sizes
- The icon remains recognizable if the text is removed from the monochrome version
