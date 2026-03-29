# PNG Generation

Generate PNG icon files from SVG sources using `@resvg/resvg-js`.

## Why resvg?

- Rust-based SVG renderer with full filter support (blur, drop-shadow, masks)
- Handles `<text>` elements with system fonts via `loadSystemFonts: true`
- Produces clean, high-quality PNG output
- No browser/DOM required

## Workflow

### Step 1: Install (temporary)

```bash
npm install @resvg/resvg-js
```

### Step 2: Create generation script

Create `generate-icons.mjs` in the project root:

```javascript
import { Resvg } from '@resvg/resvg-js';
import { readFileSync, writeFileSync, mkdirSync } from 'fs';

// Ensure output directory exists
mkdirSync('assets/images', { recursive: true });

const configs = [
  { svg: 'assets/svg/icon-full.svg',        png: 'assets/images/icon.png',                        size: 1024 },
  { svg: 'assets/svg/icon-foreground.svg',   png: 'assets/images/android-icon-foreground.png',     size: 1024 },
  { svg: 'assets/svg/icon-background.svg',   png: 'assets/images/android-icon-background.png',     size: 1024 },
  { svg: 'assets/svg/icon-monochrome.svg',   png: 'assets/images/android-icon-monochrome.png',     size: 1024 },
  { svg: 'assets/svg/icon-full.svg',         png: 'assets/images/splash-icon.png',                 size: 512  },
  { svg: 'assets/svg/icon-full.svg',         png: 'assets/images/favicon.png',                     size: 48   },
];

for (const { svg, png, size } of configs) {
  const svgData = readFileSync(svg, 'utf-8');
  const resvg = new Resvg(svgData, {
    fitTo: { mode: 'width', value: size },
    font: { loadSystemFonts: true },
  });
  const rendered = resvg.render();
  writeFileSync(png, rendered.asPng());
  console.log(`Generated ${png} (${size}x${size})`);
}

console.log('Done! All icons generated.');
```

### Step 3: Run the script

```bash
node generate-icons.mjs
```

Expected output:
```
Generated assets/images/icon.png (1024x1024)
Generated assets/images/android-icon-foreground.png (1024x1024)
Generated assets/images/android-icon-background.png (1024x1024)
Generated assets/images/android-icon-monochrome.png (1024x1024)
Generated assets/images/splash-icon.png (512x512)
Generated assets/images/favicon.png (48x48)
Done! All icons generated.
```

### Step 4: Cleanup

```bash
rm generate-icons.mjs
npm uninstall @resvg/resvg-js
```

### Step 5: Verify

Check that all 6 PNG files exist and have reasonable sizes:

```bash
ls -la assets/images/icon.png assets/images/android-icon-*.png assets/images/splash-icon.png assets/images/favicon.png
```

Expected sizes (approximate):
- `icon.png`: 100-400 KB
- `android-icon-foreground.png`: 100-300 KB
- `android-icon-background.png`: 50-150 KB
- `android-icon-monochrome.png`: 5-30 KB
- `splash-icon.png`: 50-200 KB
- `favicon.png`: 1-10 KB

## Alternative: Inline Script

Instead of creating a file, you can run the generation inline:

```bash
node -e "
const { Resvg } = require('@resvg/resvg-js');
const { readFileSync, writeFileSync, mkdirSync } = require('fs');
mkdirSync('assets/images', { recursive: true });
const configs = [
  ['assets/svg/icon-full.svg', 'assets/images/icon.png', 1024],
  ['assets/svg/icon-foreground.svg', 'assets/images/android-icon-foreground.png', 1024],
  ['assets/svg/icon-background.svg', 'assets/images/android-icon-background.png', 1024],
  ['assets/svg/icon-monochrome.svg', 'assets/images/android-icon-monochrome.png', 1024],
  ['assets/svg/icon-full.svg', 'assets/images/splash-icon.png', 512],
  ['assets/svg/icon-full.svg', 'assets/images/favicon.png', 48],
];
for (const [svg, png, size] of configs) {
  const r = new Resvg(readFileSync(svg, 'utf-8'), { fitTo: { mode: 'width', value: size }, font: { loadSystemFonts: true } });
  writeFileSync(png, r.render().asPng());
  console.log('Generated', png);
}
"
```

This avoids creating a temporary file but is harder to debug if something fails.

## Troubleshooting

- **Text renders as empty boxes**: Ensure `font: { loadSystemFonts: true }` is set in Resvg options
- **Filters not rendering**: Make sure you're using SVG `<filter>` elements, not CSS filters
- **Transparent areas appear black**: The PNG format supports transparency -- verify your viewer supports it
- **Monochrome icon is too large**: It should be small (~5-30KB) since it's just white shapes, no gradients
- **npm install fails on M1/ARM Mac**: Try `npm install @resvg/resvg-js --force` or update Node.js
