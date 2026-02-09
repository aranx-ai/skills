# Working with Color

## Contents
1. [HSL Over Hex](#hsl-over-hex)
2. [Building a Palette](#building-a-palette)
3. [Defining Shades](#defining-shades)
4. [Perceived Brightness](#perceived-brightness)
5. [Saturated Greys](#saturated-greys)
6. [Accessibility](#accessibility)
7. [Color Independence](#color-independence)

## HSL Over Hex

### Why HSL?
Colors that look similar appear completely different in hex:

```css
/* These look related but hex shows no connection */
#5C6AC4  /* brand blue */
#14B8A6  /* accent teal */

/* HSL shows the relationship */
hsl(235, 44%, 56%)  /* brand blue */
hsl(168, 80%, 40%)  /* accent teal */
```

### HSL Components
- **Hue (0-360°):** Position on color wheel (0°=red, 120°=green, 240°=blue)
- **Saturation (0-100%):** Color intensity (0%=grey, 100%=vivid)
- **Lightness (0-100%):** Light to dark (0%=black, 50%=pure color, 100%=white)

### HSL vs HSB
Design tools use HSB (brightness), browsers use HSL (lightness). They're different:
- HSB 100% brightness at 100% saturation = vivid color
- HSL 100% lightness at any saturation = white

Convert to HSL for web.

## Building a Palette

### You Need More Colors Than You Think
Five-color generators are useless. Real UIs need:

**Greys (8-10 shades):** Text, backgrounds, borders, disabled states
**Primary (5-10 shades):** Brand color, CTAs, active states
**Accent colors (5-10 shades each):**
- Green: success, positive trends
- Red: errors, destructive actions, negative trends
- Yellow: warnings
- Possibly others for categorization (charts, tags, calendars)

### Total Palette Size
A complex UI might have 100+ color values (8-10 colors × 10 shades each).

Tailwind 4 ships with a comprehensive oklch-based palette (`slate`, `gray`, `zinc`, `neutral`, `stone` for greys; `red`, `orange`, `amber`, `yellow`, `lime`, `green`, `emerald`, `teal`, `cyan`, `sky`, `blue`, `indigo`, `violet`, `purple`, `fuchsia`, `pink`, `rose` for colors), each with shades 50-950.

## Defining Shades

### Don't Generate on the Fly
`lighten()` and `darken()` functions create inconsistent results. Define shades upfront.

### The Process

**1. Pick the base (500):**
Choose a shade that works as a button background—not too light, not too dark.

**2. Pick the edges:**
- Darkest (900): Good for text on light backgrounds
- Lightest (100): Good for tinted backgrounds (alerts, badges)

**3. Fill the gaps:**
Add 700, 300, then 800, 600, 400, 200 to create 9 shades.

### Example Primary Blue
Tailwind 4 provides pre-built shades. For custom colors, define in CSS:

```css
/* Tailwind 4 @theme syntax */
@theme {
  --color-brand-50:  oklch(0.97 0.01 250);
  --color-brand-100: oklch(0.93 0.02 250);
  --color-brand-200: oklch(0.85 0.04 250);
  --color-brand-300: oklch(0.73 0.08 250);
  --color-brand-400: oklch(0.60 0.12 250);
  --color-brand-500: oklch(0.48 0.15 250);  /* base: buttons */
  --color-brand-600: oklch(0.40 0.14 250);
  --color-brand-700: oklch(0.32 0.12 250);
  --color-brand-800: oklch(0.24 0.10 250);
  --color-brand-900: oklch(0.16 0.08 250);  /* text */
}
```

Then use as `bg-brand-500`, `text-brand-900`, etc.

### Adjustments at Extremes
As lightness approaches 0% or 100%, saturation's impact weakens. Compensate:
- Increase saturation for very light/dark shades
- Rotate hue toward brighter colors for light shades (see next section)

## Perceived Brightness

### Not All Hues Are Equal
At the same HSL lightness, some colors look brighter:

**Bright hues:** Yellow (60°), Cyan (180°), Magenta (300°)
**Dark hues:** Red (0°), Green (120°), Blue (240°)

Yellow at 50% lightness looks way lighter than blue at 50% lightness.

### Rotate Hue for Better Shades
To lighten a color without washing it out:
- Rotate hue toward nearest bright hue (60°, 180°, or 300°)
- Stay within 20-30° to avoid looking like a different color

To darken:
- Rotate toward nearest dark hue (0°, 120°, or 240°)

**Example for orange (30°):**
```css
/* Lighter shades: rotate toward yellow (60°) */
--orange-200: hsl(40, 90%, 80%);   /* hue 40, not 30 */
--orange-300: hsl(36, 88%, 70%);

/* Base */
--orange-500: hsl(30, 85%, 50%);

/* Darker shades: rotate toward red (0°) */  
--orange-700: hsl(24, 82%, 35%);
--orange-800: hsl(20, 80%, 25%);   /* hue 20, not 30 */
```

## Saturated Greys

### Pure Grey Is Lifeless
True grey (0% saturation) feels flat. Tailwind 4 provides several grey palettes with different temperatures:

**Cool greys:** `slate` (blue undertone), `gray` (neutral-cool)
```html
<p class="text-slate-600">Cool, professional</p>
```

**Warm greys:** `stone` (slight warm), `neutral` (true neutral)
```html
<p class="text-stone-600">Warm, friendly</p>
```

**True neutral:** `zinc` (balanced)
```html
<p class="text-zinc-600">Neutral</p>
```

### Custom Saturated Greys
For custom greys, add subtle saturation in your theme:

```css
@theme {
  /* Cool grey with blue undertone */
  --color-cool-500: oklch(0.45 0.02 250);
  
  /* Warm grey with yellow undertone */
  --color-warm-500: oklch(0.45 0.02 80);
}
```

## Accessibility

### Contrast Ratios (WCAG)
- Normal text (<18px): 4.5:1 minimum
- Large text (18px+ or 14px bold): 3:1 minimum

### Dark Backgrounds Are Tricky
White text on colored backgrounds often needs darker colors than you'd expect to hit 4.5:1.

**Solution: Flip the contrast**
Instead of white text on dark brand color, use dark brand color text on light tinted background:

```html
<!-- Tailwind 4: Hard to get enough contrast -->
<span class="bg-blue-500 text-white">Badge</span>

<!-- Easier and less attention-grabbing -->
<span class="bg-blue-100 text-blue-800">Badge</span>
```

### Colored Text on Colored Background
When you need secondary text on a colored panel:
- Rotating hue toward a brighter color increases perceived contrast
- This helps hit accessibility targets while staying colorful

## Color Independence

### Don't Rely on Color Alone
Colorblind users can't distinguish red/green or other combinations.

**Pair color with another indicator:**
- Icons: ↑ with green, ↓ with red
- Patterns: Solid vs. dashed lines on charts
- Labels: "Approved" badge, not just green dot

```html
<!-- Bad: color only -->
<span class="text-red-500">-12%</span>

<!-- Good: color + icon -->
<span class="text-red-500 flex items-center gap-1"><IconDown class="size-4" /> -12%</span>
```

### Trend Lines
Use contrast (light/dark) instead of distinct colors for colorblind-friendly charts.
