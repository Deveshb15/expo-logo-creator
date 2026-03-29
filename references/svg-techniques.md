# SVG Techniques Reference

Complete library of SVG patterns for creating illustrated app icons. All examples use a 1024x1024 canvas with center at (512, 512).

## Canvas Setup

Every SVG file starts with:

```xml
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1024 1024" width="1024" height="1024">
  <defs>
    <!-- Gradients, masks, and filters go here -->
  </defs>
  <!-- Illustration elements go here -->
</svg>
```

## Gradients

### Linear Gradient (Diagonal Background)

```xml
<linearGradient id="bg" x1="0" y1="0" x2="1024" y2="1024" gradientUnits="userSpaceOnUse">
  <stop offset="0%" stop-color="#LIGHTER"/>
  <stop offset="100%" stop-color="#DARKER"/>
</linearGradient>
<rect width="1024" height="1024" rx="228" fill="url(#bg)"/>
```

- `rx="228"` gives iOS-style rounded corners (only on icon-full.svg, not background.svg)
- Diagonal direction creates depth

### Radial Gradient (3D Object Lighting)

```xml
<radialGradient id="object-fill" cx="0.35" cy="0.3" r="0.7">
  <stop offset="0%" stop-color="#FDFCFF"/>    <!-- Bright highlight -->
  <stop offset="55%" stop-color="#F0EDFF"/>   <!-- Mid tone -->
  <stop offset="100%" stop-color="#D8D2F5"/>  <!-- Shadow edge -->
</radialGradient>
```

- **Offset center** (`cx="0.35" cy="0.3"`) simulates top-left light source
- Creates a 3D sphere/dome effect on round shapes
- Tint the colors to match your palette (e.g., warm tones for orange palette)

### Cloud/Multi-Shape Gradient

When multiple overlapping shapes need to share one seamless gradient:

```xml
<linearGradient id="cloud" x1="510" y1="580" x2="510" y2="815" gradientUnits="userSpaceOnUse">
  <stop offset="0%" stop-color="#FFFFFF"/>
  <stop offset="100%" stop-color="#EDE9FF"/>
</linearGradient>
```

**CRITICAL**: Use `gradientUnits="userSpaceOnUse"` with absolute coordinates. Without this, each shape samples the gradient independently, creating visible seams.

### Ambient Glow

```xml
<radialGradient id="glow" cx="0.5" cy="0.5" r="0.5">
  <stop offset="0%" stop-color="#B8AEFF" stop-opacity="0.25"/>
  <stop offset="100%" stop-color="#B8AEFF" stop-opacity="0"/>
</radialGradient>
<circle cx="512" cy="500" r="400" fill="url(#glow)"/>
```

- Place behind the primary motif for atmospheric lighting
- Match the glow color to your palette's accent
- Use `stop-opacity` (NOT `fill-opacity`) for gradient transparency

## Masks

### Cutout/Crescent Shape

Create complex shapes by subtracting one shape from another:

```xml
<mask id="crescent">
  <rect width="1024" height="1024" fill="black"/>          <!-- Hide everything -->
  <circle cx="495" cy="474" r="273" fill="white"/>        <!-- Reveal base shape -->
  <circle cx="649" cy="341" r="238" fill="black"/>        <!-- Cut out portion -->
</mask>
<circle cx="495" cy="474" r="273" fill="url(#gradient)" mask="url(#crescent)"/>
```

- Black = hidden, White = visible
- The mask must start with a black rect covering the full canvas
- The masked element's shape should match the white reveal shape
- Masks can be reused on multiple elements (highlights, face features)

## Filters

### Drop Shadow

```xml
<filter id="shadow" x="-20%" y="-10%" width="140%" height="140%">
  <feDropShadow dx="0" dy="11" stdDeviation="17" flood-color="#1a0a4a" flood-opacity="0.22"/>
</filter>
```

- `dx="0" dy="11"` -- shadow falls straight down with slight offset
- `stdDeviation="17"` -- soft, diffuse shadow
- `flood-color` -- use a very dark version of your palette color
- Apply with `<g filter="url(#shadow)">...</g>`

### Glow Effect (for stars/sparkles)

```xml
<filter id="star-glow" x="-60%" y="-60%" width="220%" height="220%">
  <feGaussianBlur in="SourceGraphic" stdDeviation="4" result="blur"/>
  <feMerge>
    <feMergeNode in="blur"/>       <!-- Blurred copy behind -->
    <feMergeNode in="SourceGraphic"/>  <!-- Sharp original on top -->
  </feMerge>
</filter>
```

- Creates a soft halo around elements
- The `x/y/width/height` on filter must be large enough to contain the blur

## Shape Composition

### Cloud (Overlapping Circles + Rectangle)

```xml
<g filter="url(#shadow)">
  <rect x="229" y="736" width="560" height="77" rx="38" fill="url(#cloud)"/>
  <circle cx="314" cy="722" r="70" fill="url(#cloud)"/>
  <circle cx="430" cy="684" r="87" fill="url(#cloud)"/>
  <circle cx="572" cy="691" r="81" fill="url(#cloud)"/>
  <circle cx="691" cy="716" r="66" fill="url(#cloud)"/>
</g>
```

- Rectangle forms the flat base
- Circles of varying sizes create the puffy top
- Slight asymmetry in circle sizes looks more natural
- All shapes must use the same gradient fill for seamless appearance

### 4-Pointed Sparkle Star (Cubic Bezier)

```xml
<!-- Star centered at (cx, cy) with vertical arm L and horizontal arm H -->
<!-- Control points near center create the thin pinched waist -->
<path d="M cx,cy-L C cx+2,cy-5 cx+5,cy-2 cx+H,cy
                  C cx+5,cy+2 cx+2,cy+5 cx,cy+L
                  C cx-2,cy+5 cx-5,cy+2 cx-H,cy
                  C cx-5,cy-2 cx-2,cy-5 cx,cy-L Z" fill="white"/>
```

Example with real coordinates (star at 789,308 with arms 47/45):
```xml
<path d="M789,261 C791,306 791,306 834,308 C791,310 791,310 789,355 C787,310 787,310 744,308 C787,306 787,306 789,261Z" fill="white" opacity="0.95"/>
```

Create 3 stars at different sizes for depth:
- Large: opacity="0.95"
- Medium: opacity="0.88"
- Small: opacity="0.78"

### Highlight Overlay

```xml
<circle cx="OFFSET_X" cy="OFFSET_Y" r="SMALL_R" fill="white" opacity="0.12" mask="url(#shape-mask)"/>
```

- Position slightly up-left from the main shape's center (toward the light source)
- Use the same mask as the main shape so the highlight is constrained to it
- Very low opacity (0.10-0.15) for subtlety

## Character Elements

### Sleeping Face (Closed Eyes + Smile)

```xml
<g stroke="#6B5CA0" stroke-linecap="round" fill="none" mask="url(#shape-mask)">
  <!-- Left eye (closed arc) -->
  <path d="M 306,453 Q 320,467 334,453" stroke-width="6.3" opacity="0.85"/>
  <!-- Right eye (closed arc) -->
  <path d="M 362,449 Q 376,463 390,449" stroke-width="6.3" opacity="0.85"/>
  <!-- Smile -->
  <path d="M 327,498 Q 347,512 367,498" stroke-width="5" opacity="0.7"/>
</g>
```

- Use Q (quadratic bezier) for smooth arcs
- Stroke color should be darker than the shape fill
- Minimum stroke-width: 5 (for favicon visibility)
- Minimum opacity: 0.7 (for small-size readability)
- Apply the shape's mask so the face stays within bounds

### Happy Face (Dot Eyes + Smile)

```xml
<g mask="url(#shape-mask)">
  <circle cx="LEFT_EYE_X" cy="EYE_Y" r="8" fill="#6B5CA0" opacity="0.8"/>
  <circle cx="RIGHT_EYE_X" cy="EYE_Y" r="8" fill="#6B5CA0" opacity="0.8"/>
  <path d="M MOUTH_LEFT,MOUTH_Y Q MOUTH_CENTER,MOUTH_Y+20 MOUTH_RIGHT,MOUTH_Y"
        stroke="#6B5CA0" stroke-width="5" fill="none" stroke-linecap="round" opacity="0.7"/>
</g>
```

### Floating Zzz Text

```xml
<g fill="white" text-anchor="middle"
   font-family="APP_FONT_FAMILY, Avenir Next, Avenir, Futura, Helvetica Neue, sans-serif"
   font-weight="700">
  <text x="257" y="306" dy="0.35em" font-size="62" opacity="0.9"
        transform="rotate(-12, 257, 306)">z</text>
  <text x="201" y="226" dy="0.35em" font-size="48" opacity="0.68"
        transform="rotate(-8, 201, 226)">z</text>
  <text x="156" y="156" dy="0.35em" font-size="34" opacity="0.48"
        transform="rotate(-5, 156, 156)">z</text>
</g>
```

- Use this only when `text.allowed = true` under `references/typography-rules.md`
- Each z gets progressively smaller, more transparent, and less rotated
- `transform="rotate(angle, cx, cy)"` rotates around the text's own center
- Replace `APP_FONT_FAMILY` with the discovered repo font when available
- If the font is bundled with the app, pass the font file to Resvg during PNG generation
- `dy="0.35em"` vertically centers the text

## Scaling Formula

To scale all illustration elements by factor S from the center (512, 512):

```
new_x     = 512 + (old_x - 512) * S
new_y     = 512 + (old_y - 512) * S
new_r     = old_r * S                    (circle radii)
new_width = old_width * S                (rect widths)
new_height= old_height * S              (rect heights)
new_rx    = old_rx * S                   (corner radii)
new_font  = old_font_size * S           (text sizes)
new_stroke= old_stroke_width * S        (stroke widths)
```

Apply this to EVERY absolute coordinate in the SVG when resizing. The gradient coordinates in `gradientUnits="userSpaceOnUse"` must also be scaled.

## Common Pitfalls

1. **Use SVG `<filter>` elements, NOT CSS filters** -- CSS filters don't render in PNG conversion
2. **Use `stop-opacity` on gradient stops, NOT `fill-opacity`** on the shape when you want gradient transparency
3. **Always use `gradientUnits="userSpaceOnUse"`** when coordinates are absolute -- without it, overlapping shapes sample gradients independently
4. **Masks need a black `<rect>` base** covering the full 1024x1024 canvas
5. **Cloud shapes need the rectangle base** to fill gaps between circles
6. **Never place elements outside 0-1024** bounds
7. **Face features need stroke-width >= 5 and opacity >= 0.7** to be visible at favicon size (48px)
8. **The foreground SVG must NOT have a background fill** -- it must be fully transparent
9. **The monochrome SVG uses ONLY `fill="white"`** -- no gradients, no filters, no opacity variations
10. **Font rendering in resvg requires `loadSystemFonts: true`** -- without it, text elements render as empty rectangles
11. **Repo-only custom fonts must also be supplied as `font.fontFiles`** -- otherwise Resvg falls back or fails to match the intended typeface
