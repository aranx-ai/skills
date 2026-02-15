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

You can't build anything with five hex codes. A color palette generator giving you five "perfect" colors is a starting point, not a finished system. To build something real, you need a much more comprehensive set.

**Three Categories:**

**Greys (8-10 shades):**
Text, backgrounds, panels, form controls — almost everything in an interface is grey. True black looks unnatural — start with a really dark grey and work up to white in steady increments.

**Primary Color(s) (5-10 shades):**
One, maybe two colors for primary actions, active navigation, overall look. These are the colors that determine the overall look of a site — the ones that make you think of Facebook as "blue". Ultra-light shades for tinted alert backgrounds, darker shades for text.

**Accent Colors (5-10 shades each):**
- Eye-catching color (yellow, pink, teal) — highlight new features
- Red — errors, destructive actions, confirming dangerous operations, negative trends
- Yellow — warnings, caution states
- Green — success, positive trends

**Total:**
Up to **ten different colors with 5-10 shades each** for complex UIs. If distinguishing similar elements (graph lines, calendar events, tags on a project), you may need even more accents.

---

## Define Your Shades Up Front

When you need a lighter or darker variation, don't get clever using CSS preprocessor functions like `lighten()` or `darken()` to create shades on the fly. That's how you end up with 35 *slightly* different blues that all look the same. Instead, define a fixed set of shades up front that you can choose from as you work.

**Step 1: Choose the Base Color (500)**
Pick a shade that would work as a **button background**. There's no real scientific rule like "start at 50% lightness" — every color behaves differently, so rely on your eyes.

**Step 2: Find the Edges**
- **Darkest (900):** Reserved for text
- **Lightest (50/100):** For tinted backgrounds (subtle off-white/tinted)

Think about where they'll be used. The darkest shade of a color is usually reserved for text, while the lightest shade might be used to tint the background of an element. An alert component is a good example that combines both use cases — dark text on a light tinted background — making it a great place to test your edge colors.

**Step 3: Fill in the Gaps**
Nine is a great number — easy to divide and makes filling gaps straightforward. Label the darkest shade 900, base 500, lightest 100:

| Shade | Role | Process |
|-------|------|---------|
| 900 | Darkest (text) | Picked first |
| 800 | | Fill gap between 900 and 700 |
| 700 | | Midpoint between 900 and 500 — pick first |
| 600 | | Fill gap between 700 and 500 |
| 500 | Base (buttons) | Picked first |
| 400 | | Fill gap between 500 and 300 |
| 300 | | Midpoint between 500 and 100 — pick first |
| 200 | | Fill gap between 300 and 100 |
| 100 | Lightest (backgrounds) | Picked first |

Start by picking shades 700 and 300 (right in the middle of the gaps). These should feel like the perfect compromise between the shades on either side. This creates four more holes (800, 600, 400, 200) which you can fill using the same approach.

**Greys:** The base color isn't as important for greys. Start at the edges and fill in the gaps. Pick your darkest grey by choosing a color for the darkest text in your project, and your lightest grey by choosing something that works well for a subtle off-white background.

**Trust Your Eyes:**
A systematic approach gets you started, but don't be afraid to make little tweaks. Once you start using your colors in designs, it's almost inevitable that you'll want to tweak the saturation on a shade, or make a couple of shades lighter or darker. Trust your eyes, not the numbers. Just avoid adding *new* shades too often — discipline keeps the system useful.

---

## Don't Let Lightness Kill Your Saturation

As lightness moves toward 0% or 100%, saturation's impact weakens. The same saturation value at 50% lightness looks more colorful than at 90% lightness. Without compensation, lighter and darker shades look washed out.

**The Fix:**
Increase the saturation as the lightness gets further away from 50%. It's subtle but these details add up, especially when a color is being applied to a large section of UI.

**But what if the base is already at 100% saturation?** Use perceived brightness and hue rotation instead.

### Use Perceived Brightness to Your Advantage

Every hue has an inherent *perceived* brightness due to how the human eye perceives color. Yellow and blue at the same HSL lightness (50%) look completely different in brightness.

**Perceived brightness formula:**
```
perceived brightness = sqrt(0.299 * r² + 0.587 * g² + 0.114 * b²) / 255
```

Perceived brightness has:
- **Three local minimums (darkest hues):** Red (0°), Green (120°), Blue (240°)
- **Three local maximums (brightest hues):** Yellow (60°), Cyan (180°), Magenta (300°)

### Changing Brightness by Rotating Hue

Since different hues have different perceived brightness, you can change the brightness of a color by *rotating its hue* — not just adjusting lightness.

**To make a color lighter:** Rotate the hue toward the nearest bright hue — 60° (yellow), 180° (cyan), or 300° (magenta).
```
Example: hsl(210, 100%, 50%) → rotate toward cyan → hsl(190, 100%, 50%)
Result: lighter appearance at the same HSL lightness
```

**To make a color darker:** Rotate the hue toward the nearest dark hue — 0° (red), 120° (green), or 240° (blue).
```
Example: hsl(50, 100%, 50%) → rotate toward red → hsl(32, 100%, 50%)
Result: darker appearance at the same HSL lightness
```

**Practical example — Yellow palettes:**
By gradually rotating the hue toward more of an orange as you decrease the lightness, the darker shades will feel warm and rich instead of dull and brown.

**Combine approaches:**
You can get some of the brightness by adjusting the hue and some from adjusting the lightness. Example: a dark blue `hsl(221, 49%, 33%)` paired with a lighter teal `hsl(194, 49%, 73%)` — both retain their intensity.

**Warning:** Don't rotate the hue more than 20-30° or it will look like a totally different color instead of just lighter or darker.

---

## Greys Don't Have to Be Grey

By definition, true grey has a saturation of 0% — it doesn't have any actual *color* in it at all. But in practice, a lot of the colors we *think of* as grey are actually saturated quite heavily. This saturation is what makes some greys feel cool and other greys feel warm.

### Color Temperature

Saturating greys in a user interface works similarly to choosing between "warm white" and "cool white" light bulbs.

**Cool greys** — saturate with blue:
```
H 209, S 15%, L 28%    (dark)
H 207, S 12%, L 43%
H 208, S 12%, L 58%
H 210, S 16%, L 76%
H 208, S 21%, L 88%    (light — note increased saturation)
```
→ Tailwind's `slate`

**Neutral greys** — minimal to no saturation:
```
H ---, S 0%, L 28%
H ---, S 0%, L 43%
H ---, S 0%, L 58%
H ---, S 0%, L 76%
H ---, S 0%, L 88%
```
→ Tailwind's `gray`, `zinc`

**Warm greys** — saturate with yellow or orange:
```
H 41, S 15%, L 28%     (dark)
H 40, S 12%, L 43%
H 39, S 12%, L 58%
H 39, S 16%, L 76%
H 39, S 21%, L 88%     (light — note increased saturation)
```
→ Tailwind's `stone`

**Maintaining Consistency:**
Don't forget to increase the saturation for the lighter and darker shades. If you don't, those shades will look a bit washed out compared to the greys that are closer to 50% lightness.

**How Much:**
- Add a little for subtle temperature shift
- Crank it up if you want the interface to lean strongly in one direction

---

## Accessible Doesn't Have to Mean Ugly

You can meet WCAG contrast requirements while having a beautiful design.

### WCAG Contrast Requirements

**Normal Text** (under ~18px):

| Color | Contrast | Grade |
|-------|----------|-------|
| hsl(0, 0%, 54%) | 3.45:1 | Fail |
| hsl(0, 0%, 42%) | 5.41:1 | AA |
| hsl(0, 0%, 33%) | 7.57:1 | AAA |

**Large Text** (18px+ or 14px+ bold):

| Color | Contrast | Grade |
|-------|----------|-------|
| hsl(0, 0%, 59%) | 2.96:1 | Fail |
| hsl(0, 0%, 54%) | 3.45:1 | AA |
| hsl(0, 0%, 42%) | 5.41:1 | AAA |

For typical dark-text-on-light-background situations, meeting these is easy. It gets trickier with color.

### Flipping the Contrast

When using white text on a colored background, you'd be surprised how dark the color often needs to be to meet that 4.5:1 contrast ratio. This can create hierarchy issues when those elements aren't supposed to be the focus of the page — dark colored backgrounds really grab attention.

**Solution:** Flip it. Instead of light text on a dark colored background, use dark colored text on a light colored background:

```html
<!-- Hard to get 4.5:1 without dark background dominating hierarchy -->
<span class="bg-green-600 text-white">Approved</span>     <!-- 2.25:1 Fail -->

<!-- Flip it — use darker bg for better contrast -->
<span class="bg-green-700 text-white">Approved</span>     <!-- 5.97:1 AA -->

<!-- Best: flip contrast entirely — less attention-grabbing, AAA -->
<span class="bg-green-100 text-green-800">Approved</span> <!-- 9.01:1 AAA -->
```

The color is still there to support the text, but it's way less in-your-face and doesn't interfere with other actions on the page.

### Rotating the Hue

Even harder than white text on a colored background is *colored* text on a colored background. You'll run into this when picking a color for secondary text inside a dark-colored panel.

If you start by taking the background color and simply adjusting the lightness and saturation, you'll find that it's hard to meet the recommended contrast ratio without getting very close to pure white. And you don't want the primary text and secondary text to look the same.

**Solution:** Since some colors are brighter than others, rotate the hue toward a brighter color (cyan, magenta, yellow) to increase contrast while staying colorful:

```
Background: hsl(240, 34%, 34%)

/* Bad — just lighter, looks washed out and close to white */
Text:       hsl(240, 44%, 89%)  →  8.37:1 AAA, but feels white

/* Good — rotate hue toward cyan for colorful contrast */
Text:       hsl(188, 100%, 85%) →  8.71:1 AAA, still feels colorful
```

This makes it a lot easier to make the text accessible while still keeping it colorful.

---

## Don't Rely on Color Alone

Color can be a fantastic way to enhance information, but be careful not to *rely* on it, or users with color blindness will have a hard time interpreting your UI.

**Add Supporting Visual Cues:**
```html
<!-- Bad: color only — red-green colorblind can't tell the difference -->
<span class="text-green-500">+1.4%</span>
<span class="text-red-500">-11.1%</span>

<!-- Good: color + icon — meaning is clear regardless of color perception -->
<span class="text-green-500 flex items-center gap-1">
  <IconArrowUp class="size-4" /> 1.4%
</span>
<span class="text-red-500 flex items-center gap-1">
  <IconArrowDown class="size-4" /> 11.1%
</span>
```

**Use Contrast Instead of Color:**
For graph lines, donut chart segments, or similar elements, try relying on **contrast** (light vs dark shades of one color family) instead of completely different colors. It's much easier for someone who's colorblind to tell the difference between light and dark than it is to tell the difference between two distinct colors.

**The Rule:**
Always use color to **support** something your design already communicates — never use it as the only means of communication.
