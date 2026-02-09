# Color

Detailed guidance on building and using a comprehensive color system.

---

## Ditch Hex for HSL

HSL represents colors using attributes the human eye intuitively perceives — hue, saturation, and lightness.

**The Problem with Hex and RGB:**
Colors that are visually related look nothing alike in hex or RGB code. You can't tell how colors relate to each other.

**HSL Components:**

**Hue** — position on the color wheel (0-360 degrees):
- 0° = Red
- 60° = Yellow
- 120° = Green
- 180° = Cyan
- 240° = Blue
- 300° = Magenta

**Saturation** — how vivid the color is:
- 0% = Grey (no color at all)
- 100% = Vibrant and intense
- At 0% saturation, hue is irrelevant

**Lightness** — how close to black or white:
- 0% = Pure black
- 50% = Pure color at given hue
- 100% = Pure white

**HSL vs. HSB:**
Don't confuse them. In HSB, 100% brightness with 100% saturation gives you a vivid color (equivalent to 50% lightness in HSL). In HSL, 100% lightness is always white regardless of saturation.

HSB is common in design software, but browsers only understand HSL. **Use HSL for web design.**

Tailwind 4 uses **oklch** for wider gamut colors — an even more perceptually uniform color space.

---

## You Need More Colors Than You Think

You can't build anything with five hex codes. You need a comprehensive set.

**Three Categories:**

**Greys (8-10 shades):**
Text, backgrounds, panels, form controls. True black looks unnatural — start with a really dark grey and work up to white.

**Primary Color(s) (5-10 shades):**
One, maybe two colors for primary actions, active navigation, overall look. Ultra-light shades for tinted backgrounds, darker shades for text.

**Accent Colors (5-10 shades each):**
- Eye-catching color (yellow, pink, teal) — highlight new features
- Red — errors, destructive actions, negative trends
- Yellow — warnings
- Green — success, positive trends

**Total:**
Up to **ten different colors with 5-10 shades each** for complex UIs. If distinguishing similar elements (graph lines, calendar events, tags), you may need even more accents.

---

## Define Your Shades Up Front

Don't use preprocessor `lighten()` or `darken()`. Define a fixed set of shades.

**Step 1: Choose the Base Color (500)**
Pick a shade that would work as a **button background**.

**Step 2: Find the Edges**
- **Darkest (900):** Reserved for text
- **Lightest (50/100):** For tinted backgrounds

An alert component (dark text on light background) uses both extremes.

**Step 3: Fill in the Gaps**
Nine shades labeled 100-900:

| Shade | Role | Process |
|-------|------|---------|
| 900 | Darkest (text) | Picked first |
| 800 | | Fill gap between 900 and 700 |
| 700 | | Midpoint between 900 and 500 |
| 600 | | Fill gap between 700 and 500 |
| 500 | Base (buttons) | Picked first |
| 400 | | Fill gap between 500 and 300 |
| 300 | | Midpoint between 500 and 100 |
| 200 | | Fill gap between 300 and 100 |
| 100 | Lightest (backgrounds) | Picked first |

**Greys:** Same process. Darkest based on darkest text, lightest based on subtle off-white background.

**Trust Your Eyes:**
A systematic approach gets you started, but tweak as you go. Just avoid adding new shades too often — discipline keeps the system useful.

---

## Don't Let Lightness Kill Your Saturation

As lightness moves toward 0% or 100%, saturation's impact weakens. Compensate.

**The Problem:**
The same saturation at 50% lightness looks more colorful than at 90% lightness. Without compensation, lighter and darker shades look washed out.

**Perceived Brightness:**
Not all hues have the same perceived brightness. Yellow appears lighter than blue at the same HSL lightness.

Perceived brightness has:
- **Three local minimums:** Red (0°), Green (120°), Blue (240°)
- **Three local maximums:** Yellow (60°), Cyan (180°), Magenta (300°)

**Changing Brightness by Rotating Hue:**
- **To make lighter:** Rotate toward nearest bright hue (60°, 180°, 300°)
- **To make darker:** Rotate toward nearest dark hue (0°, 120°, 240°)

**Practical Example:**
For yellow palettes, rotate toward orange as you decrease lightness. Darker shades will feel warm and rich instead of dull and brown.

**Warning:** Don't rotate more than 20-30° or it looks like a different color entirely.

---

## Greys Don't Have to Be Grey

True grey (0% saturation) feels lifeless. Adding saturation creates warmer or cooler tones.

**Color Temperature:**
- **Cool greys:** Saturate with a bit of **blue** → Tailwind's `slate`
- **Neutral greys:** Minimal saturation → Tailwind's `gray`, `zinc`
- **Warm greys:** Saturate with **yellow or orange** → Tailwind's `stone`

**Maintaining Consistency:**
Increase saturation for lighter and darker shades — if you don't, they'll look washed out compared to mid-range greys.

**How Much:**
- Add a little for subtle temperature
- Crank it up for a strong directional lean

---

## Accessible Doesn't Have to Mean Ugly

You can meet WCAG contrast requirements while having a beautiful design.

**WCAG Contrast Requirements:**
- **Normal text** (under ~18px): **4.5:1** contrast ratio
- **Larger text** (18px+ or 14px+ bold): **3:1** contrast ratio

**Flipping the Contrast:**
When white text on a colored background requires the color to be very dark (creating hierarchy problems), flip it:

```html
<!-- Hard to get 4.5:1 without dark background dominating -->
<span class="bg-blue-500 text-white">Badge</span>

<!-- Easier and less attention-grabbing -->
<span class="bg-blue-100 text-blue-800">Badge</span>
```

**Rotating the Hue:**
For colored text on colored backgrounds, adjusting lightness alone pushes toward pure white. Since some colors are brighter than others, rotate hue toward a brighter color (cyan, magenta, yellow) to increase contrast while staying colorful.

---

## Don't Rely on Color Alone

Color can enhance information, but don't rely on it as the only indicator — users with color blindness need alternatives.

**Add Supporting Visual Cues:**
```html
<!-- Bad: color only -->
<span class="text-red-500">-12%</span>

<!-- Good: color + icon -->
<span class="text-red-500 flex items-center gap-1">
  <IconArrowDown class="size-4" /> -12%
</span>
```

**Use Contrast Instead of Color:**
For graph lines or similar elements, light vs dark is easier to distinguish than two distinct colors for colorblind users.

**The Rule:**
Always use color to **support** something your design already communicates — never as the only means.
