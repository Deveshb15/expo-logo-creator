# Expo Icon Specification

Complete specification for Expo/React Native app icon assets.

## Required Files

### SVG Source Files (Design Masters)

Create these in `assets/svg/`:

| File | Purpose | Background | Effects | Colors |
|------|---------|------------|---------|--------|
| `icon-full.svg` | iOS icon + web + splash source | Gradient rect with `rx="228"` | Shadows, glow, filters | Full color with gradients |
| `icon-foreground.svg` | Android adaptive foreground | **Transparent** (no background) | Shadows, glow, filters | Full color with gradients |
| `icon-background.svg` | Android adaptive background | Gradient rect, **no rounded corners** | None | Gradient only |
| `icon-monochrome.svg` | Android 13+ themed icon | **Transparent** | **None** | `fill="white"` only |

### PNG Output Files

Generate these in `assets/images/`:

| File | Size | Source SVG | Platform |
|------|------|-----------|----------|
| `icon.png` | 1024x1024 | `icon-full.svg` | iOS app icon |
| `android-icon-foreground.png` | 1024x1024 | `icon-foreground.svg` | Android adaptive foreground |
| `android-icon-background.png` | 1024x1024 | `icon-background.svg` | Android adaptive background |
| `android-icon-monochrome.png` | 1024x1024 | `icon-monochrome.svg` | Android 13+ themed icon |
| `splash-icon.png` | 512x512 | `icon-full.svg` | Launch screen |
| `favicon.png` | 48x48 | `icon-full.svg` | Web browser tab |

## app.json Configuration

```json
{
  "expo": {
    "icon": "./assets/images/icon.png",
    "ios": {
      "icon": "./assets/images/icon.png"
    },
    "android": {
      "adaptiveIcon": {
        "foregroundImage": "./assets/images/android-icon-foreground.png",
        "backgroundImage": "./assets/images/android-icon-background.png",
        "monochromeImage": "./assets/images/android-icon-monochrome.png"
      }
    },
    "web": {
      "favicon": "./assets/images/favicon.png"
    }
  }
}
```

If `expo-splash-screen` is installed, also add:

```json
{
  "expo": {
    "plugins": [
      ["expo-splash-screen", {
        "backgroundColor": "#BACKGROUND_COLOR",
        "image": "./assets/images/splash-icon.png",
        "imageWidth": 200
      }]
    ]
  }
}
```

## Platform-Specific Rules

### iOS

- Single flat icon at 1024x1024
- iOS automatically applies corner rounding (~22.3% radius)
- Use `rx="228"` on the background rect in `icon-full.svg` to preview how corners will look
- No transparency allowed -- icon must be fully opaque
- The OS scales down to all required sizes (29pt, 40pt, 60pt, 76pt, 83.5pt at 1x/2x/3x)

### Android Adaptive Icons

- Two-layer system: foreground + background composed by the OS
- The OS applies a shape mask (circle, squircle, rounded square -- varies by OEM)
- **Safe zone**: Only the inner ~66% circle (diameter ~680px of 1024) is guaranteed visible
- For the foreground SVG, keep critical elements within a 680px diameter circle from center
- The foreground layer has slight parallax movement, so avoid edge-touching elements
- `icon-background.svg` should NOT have rounded corners -- the OS applies its own mask

### Android Monochrome (Android 13+)

- Used for Material You dynamic theming
- The OS applies the user's chosen theme color
- Must be pure white shapes on transparent background
- No gradients, no filters, no opacity, no stroke effects
- Think of it as a silhouette/stencil of your icon

### Web Favicon

- 48x48 PNG
- Must be recognizable at this tiny size
- Complex details (faces, text) may be invisible -- that's okay
- The main shape/silhouette should be clear

## SVG Canvas Rules

- All SVGs use: `viewBox="0 0 1024 1024" width="1024" height="1024"`
- Center point: (512, 512)
- iOS corner radius on full icon: `rx="228"` (the background rect)
- Android safe zone circle: center (512, 512), radius 340px

## File Organization

```
your-expo-app/
├── assets/
│   ├── svg/                              # Vector source files
│   │   ├── icon-full.svg
│   │   ├── icon-foreground.svg
│   │   ├── icon-background.svg
│   │   └── icon-monochrome.svg
│   └── images/                           # Rasterized PNGs
│       ├── icon.png                      # 1024x1024
│       ├── android-icon-foreground.png   # 1024x1024
│       ├── android-icon-background.png   # 1024x1024
│       ├── android-icon-monochrome.png   # 1024x1024
│       ├── splash-icon.png              # 512x512
│       └── favicon.png                   # 48x48
└── app.json                              # References the PNGs
```
