# Motif Catalog

Illustrated SVG elements organized by app category. Select 2-4 elements that match the app's purpose. **NEVER default to moon/cloud -- always match the specific app.**

Textual motifs and labels are conditional. Use them only when `references/typography-rules.md` allows text and the selected font can actually be rendered.

All motifs are designed for a 1024x1024 canvas centered at (512, 512). Scale and reposition as needed.

## Category Guide

| Category | Primary Motif | Supporting Motifs | Decorative |
|----------|--------------|-------------------|------------|
| Sleep/Wellness | Crescent Moon, Cloud | Zzz text | Stars, Sparkles |
| Fitness/Health | Heart, Dumbbell | Pulse line | Lightning, Sparkles |
| Finance/Money | Coin, Piggy Bank | Chart line, Arrow up | Sparkles, Dollar sign |
| Social/Chat | Speech Bubble, Smiley | Hearts | Connection dots, Sparkles |
| Productivity | Checkbox, Clipboard | Pencil | Lightning, Stars |
| Food/Cooking | Chef Hat, Bowl | Fork/Spoon, Steam | Hearts, Sparkles |
| Music/Audio | Musical Note, Headphones | Waveform bars | Sparkles, Stars |
| Travel/Maps | Compass, Location Pin | Clouds | Airplane, Stars |
| Education | Book, Lightbulb | Pencil | Graduation cap, Stars |
| Photography | Camera, Aperture | Frame corners | Flash, Sparkles |
| Weather | Sun, Cloud, Raindrop | Rainbow arc | Snowflake, Lightning |
| Shopping/Commerce | Shopping Bag, Cart | Tag, Barcode | Hearts, Stars |
| Gaming | Game Controller, Joystick | Pixel heart | Stars, Lightning |
| Meditation | Lotus Flower, Om | Ripple rings | Sparkles, Stars |
| Generic | App Initial Letter, Abstract Orb | Gradient ring | Stars, Sparkles |

---

## Primary Motifs

### Crescent Moon

```xml
<mask id="crescent">
  <rect width="1024" height="1024" fill="black"/>
  <circle cx="495" cy="474" r="273" fill="white"/>
  <circle cx="649" cy="341" r="238" fill="black"/>
</mask>
<circle cx="495" cy="474" r="273" fill="url(#moon-gradient)" mask="url(#crescent)"/>
```

Position: slightly above center. Pair with: cloud base, stars, zzz text.

### Heart

```xml
<path d="M512,680 C512,680 340,560 340,440 C340,370 390,320 450,320 C490,320 512,355 512,355
         C512,355 534,320 574,320 C634,320 684,370 684,440 C684,560 512,680 512,680Z"
      fill="url(#heart-gradient)"/>
```

Position: centered. Good for health, social, dating apps. Add a cute face or pulse line.

### Speech Bubble

```xml
<rect x="290" y="310" width="444" height="290" rx="55" fill="url(#bubble-gradient)"/>
<path d="M410,600 L440,600 L380,670Z" fill="url(#bubble-gradient)"/>
```

Position: slightly above center. Add dot-dot-dot typing indicator or smiley face inside.

### Musical Note (Eighth Note)

```xml
<g fill="url(#note-gradient)">
  <ellipse cx="430" cy="620" rx="65" ry="50" transform="rotate(-15, 430, 620)"/>
  <rect x="485" y="310" width="18" height="310" rx="9"/>
  <path d="M503,310 C503,310 580,280 600,330 C620,380 560,400 503,390" fill="url(#note-gradient)"/>
</g>
```

Position: centered. The flag curves right. Pair with waveform bars or sparkles.

### Book (Open)

```xml
<g filter="url(#shadow)">
  <path d="M512,360 L310,395 L310,700 L512,665Z" fill="url(#page-left)"/>
  <path d="M512,360 L714,395 L714,700 L512,665Z" fill="url(#page-right)"/>
  <line x1="512" y1="360" x2="512" y2="665" stroke="#C8BFF0" stroke-width="3"/>
</g>
```

Position: centered. Right page slightly brighter. Pair with pencil, lightbulb, or graduation cap.

### Lightbulb

```xml
<g fill="url(#bulb-gradient)">
  <circle cx="512" cy="420" r="150"/>
  <rect x="472" y="560" width="80" height="50" rx="8"/>
  <rect x="482" y="610" width="60" height="15" rx="7"/>
  <rect x="492" y="625" width="40" height="12" rx="6"/>
</g>
<!-- Rays -->
<g stroke="white" stroke-width="6" stroke-linecap="round" opacity="0.6">
  <line x1="512" y1="220" x2="512" y2="250"/>
  <line x1="370" y1="300" x2="390" y2="320"/>
  <line x1="654" y1="300" x2="634" y2="320"/>
  <line x1="310" y1="420" x2="340" y2="420"/>
  <line x1="714" y1="420" x2="684" y2="420"/>
</g>
```

Position: centered, slightly above. Pair with sparkles for "idea" feeling.

### Camera

```xml
<g fill="url(#camera-gradient)">
  <rect x="300" y="380" width="424" height="300" rx="40"/>
  <rect x="420" y="340" width="184" height="60" rx="15"/>
  <circle cx="512" cy="530" r="100" fill="none" stroke="white" stroke-width="12" opacity="0.9"/>
  <circle cx="512" cy="530" r="40" fill="white" opacity="0.3"/>
  <circle cx="660" cy="420" r="15" fill="white" opacity="0.5"/>
</g>
```

Position: centered. The lens aperture creates visual interest. Pair with flash or frame.

### Compass

```xml
<circle cx="512" cy="490" r="200" fill="url(#compass-gradient)" filter="url(#shadow)"/>
<circle cx="512" cy="490" r="170" fill="none" stroke="white" stroke-width="4" opacity="0.3"/>
<!-- Needle -->
<polygon points="512,330 525,490 512,510 499,490" fill="white" opacity="0.9"/>
<polygon points="512,650 525,490 512,470 499,490" fill="white" opacity="0.5"/>
<circle cx="512" cy="490" r="15" fill="white"/>
<!-- Cardinal marks -->
<g fill="white" font-family="APP_FONT_FAMILY, Avenir Next, Avenir, Futura, sans-serif" font-weight="700"
   font-size="28" text-anchor="middle" opacity="0.7">
  <text x="512" y="348">N</text>
  <text x="512" y="652">S</text>
  <text x="340" y="498">W</text>
  <text x="684" y="498">E</text>
</g>
```

Position: centered. Pair with location pin and clouds. If text is not allowed, replace the letters with simple cardinal ticks.

### Chef Hat

```xml
<g fill="url(#hat-gradient)" filter="url(#shadow)">
  <rect x="380" y="530" width="264" height="70" rx="10"/>
  <circle cx="420" cy="480" r="75"/>
  <circle cx="512" cy="450" r="85"/>
  <circle cx="604" cy="480" r="75"/>
  <circle cx="460" cy="430" r="60"/>
  <circle cx="564" cy="430" r="60"/>
</g>
```

Position: slightly above center. Cloud-like puff construction. Pair with fork/spoon.

### Coin / Token

```xml
<circle cx="512" cy="490" r="200" fill="url(#coin-gradient)" filter="url(#shadow)"/>
<circle cx="512" cy="490" r="170" fill="none" stroke="white" stroke-width="6" opacity="0.25"/>
<!-- Dollar sign or symbol -->
<text x="512" y="490" dy="0.35em" text-anchor="middle"
      font-family="APP_FONT_FAMILY, Avenir Next, Avenir, Futura, sans-serif"
      font-size="180" font-weight="700" fill="white" opacity="0.85">$</text>
```

Position: centered. Use a symbol relevant to the app only when the symbol is central to brand recognition. If exact typography is risky, convert the symbol to paths or drop it.

### Game Controller

```xml
<g fill="url(#controller-gradient)" filter="url(#shadow)">
  <rect x="320" y="420" width="384" height="200" rx="60"/>
  <!-- Left grip -->
  <rect x="320" y="480" width="80" height="160" rx="40"/>
  <!-- Right grip -->
  <rect x="624" y="480" width="80" height="160" rx="40"/>
  <!-- D-pad -->
  <rect x="400" y="490" width="60" height="20" rx="4" fill="white" opacity="0.4"/>
  <rect x="420" y="470" width="20" height="60" rx="4" fill="white" opacity="0.4"/>
  <!-- Buttons -->
  <circle cx="610" cy="480" r="12" fill="white" opacity="0.5"/>
  <circle cx="640" cy="510" r="12" fill="white" opacity="0.5"/>
  <circle cx="580" cy="510" r="12" fill="white" opacity="0.5"/>
  <circle cx="610" cy="540" r="12" fill="white" opacity="0.5"/>
</g>
```

Position: centered. Pair with pixel heart, stars, lightning.

### Lotus Flower

```xml
<g fill="url(#petal-gradient)" opacity="0.9">
  <!-- Center petal -->
  <ellipse cx="512" cy="420" rx="50" ry="120" transform="rotate(0, 512, 510)"/>
  <!-- Side petals -->
  <ellipse cx="512" cy="420" rx="50" ry="120" transform="rotate(30, 512, 510)"/>
  <ellipse cx="512" cy="420" rx="50" ry="120" transform="rotate(-30, 512, 510)"/>
  <ellipse cx="512" cy="420" rx="50" ry="120" transform="rotate(60, 512, 510)"/>
  <ellipse cx="512" cy="420" rx="50" ry="120" transform="rotate(-60, 512, 510)"/>
</g>
<!-- Center dot -->
<circle cx="512" cy="510" r="25" fill="white" opacity="0.5"/>
```

Position: centered. Pair with ripple rings and sparkles.

### Shopping Bag

```xml
<g fill="url(#bag-gradient)" filter="url(#shadow)">
  <rect x="360" y="420" width="304" height="300" rx="25"/>
  <!-- Handle -->
  <path d="M430,420 C430,340 512,300 512,300 C512,300 594,340 594,420"
        fill="none" stroke="url(#bag-gradient)" stroke-width="24" stroke-linecap="round"/>
</g>
```

Position: centered. Pair with heart, tag, or sparkles.

### Location Pin

```xml
<g fill="url(#pin-gradient)" filter="url(#shadow)">
  <path d="M512,750 C512,750 350,560 350,440 C350,350 420,280 512,280
           C604,280 674,350 674,440 C674,560 512,750 512,750Z"/>
  <circle cx="512" cy="430" r="70" fill="white" opacity="0.35"/>
</g>
```

Position: centered. The teardrop shape points down. Pair with compass or map elements.

---

## Supporting Motifs

### Pulse/Heartbeat Line

```xml
<polyline points="250,520 380,520 420,520 450,400 480,620 510,450 540,520 700,520"
          fill="none" stroke="white" stroke-width="8" stroke-linecap="round"
          stroke-linejoin="round" opacity="0.7"/>
```

### Fork and Spoon (Crossed)

```xml
<g stroke="white" stroke-width="10" stroke-linecap="round" opacity="0.7" fill="none">
  <!-- Fork -->
  <line x1="460" y1="620" x2="460" y2="380"/>
  <line x1="440" y1="380" x2="440" y2="430"/>
  <line x1="460" y1="380" x2="460" y2="430"/>
  <line x1="480" y1="380" x2="480" y2="430"/>
  <!-- Spoon -->
  <line x1="564" y1="620" x2="564" y2="450"/>
  <ellipse cx="564" cy="410" rx="30" ry="40" fill="white" opacity="0.7"/>
</g>
```

### Waveform/Equalizer Bars

```xml
<g fill="white" opacity="0.6">
  <rect x="390" y="480" width="16" height="80" rx="8"/>
  <rect x="420" y="440" width="16" height="160" rx="8"/>
  <rect x="450" y="460" width="16" height="120" rx="8"/>
  <rect x="480" y="420" width="16" height="200" rx="8"/>
  <rect x="510" y="450" width="16" height="140" rx="8"/>
  <rect x="540" y="430" width="16" height="180" rx="8"/>
  <rect x="570" y="470" width="16" height="100" rx="8"/>
  <rect x="600" y="490" width="16" height="60" rx="8"/>
</g>
```

### Pencil

```xml
<g transform="rotate(-35, 620, 400)">
  <rect x="590" y="300" width="60" height="250" rx="4" fill="url(#pencil-gradient)"/>
  <polygon points="590,550 620,610 650,550" fill="url(#pencil-tip)"/>
  <rect x="590" y="300" width="60" height="30" rx="4" fill="white" opacity="0.3"/>
</g>
```

### Arrow Up (for growth/finance)

```xml
<g stroke="white" stroke-width="10" stroke-linecap="round" stroke-linejoin="round" opacity="0.7">
  <polyline points="400,600 400,420 500,520 500,350 600,450 600,300"/>
  <polyline points="560,300 600,300 600,340"/>
</g>
```

### Graduation Cap

```xml
<g fill="white" opacity="0.7">
  <polygon points="512,350 350,430 512,510 674,430"/>
  <line x1="512" y1="510" x2="512" y2="580" stroke="white" stroke-width="6"/>
  <rect x="490" y="510" width="44" height="60" rx="4" fill="none" stroke="white" stroke-width="5"/>
  <line x1="674" y1="430" x2="674" y2="540" stroke="white" stroke-width="6"/>
  <circle cx="674" cy="550" r="10" fill="white"/>
</g>
```

### Headphones

```xml
<g fill="none" stroke="url(#headphone-gradient)" stroke-width="20">
  <path d="M350,520 C350,350 674,350 674,520"/>
</g>
<rect x="320" y="490" width="60" height="120" rx="20" fill="url(#headphone-gradient)"/>
<rect x="644" y="490" width="60" height="120" rx="20" fill="url(#headphone-gradient)"/>
```

---

## Decorative Elements

### 4-Pointed Sparkle Star

Three sizes for depth:

```xml
<!-- Large -->
<path d="M789,261 C791,306 791,306 834,308 C791,310 791,310 789,355 C787,310 787,310 744,308 C787,306 787,306 789,261Z" fill="white" opacity="0.95"/>
<!-- Medium -->
<path d="M828,478 C830,507 830,507 859,509 C830,511 830,511 828,540 C826,511 826,511 797,509 C826,507 826,507 828,478Z" fill="white" opacity="0.88"/>
<!-- Small -->
<path d="M733,172 C734,193 734,193 755,195 C734,197 734,197 733,218 C732,197 732,197 711,195 C732,193 732,193 733,172Z" fill="white" opacity="0.78"/>
```

### Cloud (as supporting element)

```xml
<g fill="url(#cloud-gradient)">
  <rect x="BASE_X" y="BASE_Y" width="W" height="H" rx="RX"/>
  <circle cx="C1X" cy="C1Y" r="R1"/>
  <circle cx="C2X" cy="C2Y" r="R2"/>
  <circle cx="C3X" cy="C3Y" r="R3"/>
</g>
```

### Lightning Bolt

```xml
<polygon points="540,280 480,510 530,510 470,740 590,460 540,460 600,280"
         fill="white" opacity="0.85"/>
```

### Steam Wisps

```xml
<g stroke="white" stroke-width="5" fill="none" stroke-linecap="round" opacity="0.5">
  <path d="M480,350 C480,330 500,330 500,310 C500,290 520,290 520,270"/>
  <path d="M520,360 C520,340 540,340 540,320 C540,300 560,300 560,280"/>
  <path d="M560,355 C560,335 580,335 580,315 C580,295 600,295 600,275"/>
</g>
```

### Small Hearts

```xml
<path d="M X,Y+20 C X,Y+20 X-15,Y+10 X-15,Y+3 C X-15,Y-5 X,Y-5 X,Y
         C X,Y-5 X+15,Y-5 X+15,Y+3 C X+15,Y+10 X,Y+20 X,Y+20Z"
      fill="white" opacity="0.6"/>
```

Scatter 2-3 at different sizes around the composition.

### Ripple Rings (for meditation)

```xml
<g fill="none" stroke="white" stroke-width="3">
  <circle cx="512" cy="512" r="250" opacity="0.15"/>
  <circle cx="512" cy="512" r="320" opacity="0.10"/>
  <circle cx="512" cy="512" r="390" opacity="0.05"/>
</g>
```

### Connection Dots (for social)

```xml
<g fill="white" opacity="0.5">
  <circle cx="300" cy="350" r="8"/>
  <circle cx="400" cy="250" r="6"/>
  <circle cx="650" cy="300" r="7"/>
  <circle cx="720" cy="450" r="5"/>
  <line x1="300" y1="350" x2="400" y2="250" stroke="white" stroke-width="2" opacity="0.3"/>
  <line x1="400" y1="250" x2="650" y2="300" stroke="white" stroke-width="2" opacity="0.3"/>
  <line x1="650" y1="300" x2="720" y2="450" stroke="white" stroke-width="2" opacity="0.3"/>
</g>
```
