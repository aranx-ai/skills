---
name: pixel-craft
description: Create distinctive, production-grade frontend interfaces with high design quality. Use this skill when the user asks to build web components, pages, artifacts, posters, or applications (examples include websites, landing pages, dashboards, React components, HTML/CSS layouts, or when styling/beautifying any web UI). Generates creative, polished code and UI design that avoids generic AI aesthetics.
---

# Pixel Craft Skill

Create professional, polished UI that looks intentionally designed—not AI-generated.

---

## 1. Starting From Scratch

### Start with a Feature, Not a Layout
Don't design the shell first (nav, sidebar, footer). Design actual functionality:
- What fields does this form need?
- What data does this card display?
- What actions can the user take?

The shell comes later, informed by the features you've designed.

### Hold the Color
Design in grayscale first. This forces you to use spacing, contrast, and size to create hierarchy—not color as a crutch. Color enhances a clear hierarchy; it can't fix a broken one.

### Don't Design Too Much
Don't design every feature upfront. Work in cycles:
1. Design a simple version
2. Build it
3. Discover edge cases in real use
4. Fix them
5. Repeat

**Be a pessimist:** Don't include features you're not ready to build. A comment system without attachments is better than no comment system at all.

### Choose a Personality
Every design communicates something. Decide intentionally:

| Element | Elegant/Serious | Playful/Casual |
|---------|-----------------|----------------|
| Font | Serif or neutral sans | Rounded sans-serif |
| Border radius | None or small (rounded-sm) | Large (rounded-xl, rounded-full) |
| Colors | Muted, blue, gold | Bright, pink, teal |
| Language | "Your account" | "Hey there!" |

Stay consistent—don't mix playful borders with formal language.

### Limit Your Choices
Don't pick from infinite values. Define systems upfront:
- Spacing: 1, 2, 3, 4, 6, 8, 12, 16, 24, 32
- Font sizes: text-xs through text-4xl
- Colors: 8-10 shades per color
- Shadows: shadow-sm through shadow-2xl

Constraints speed up decisions and create consistency.

---

## 2. Visual Hierarchy

### Not All Elements Are Equal
Every interface has:
- **Primary content** — What users came for (text-slate-900)
- **Secondary content** — Supporting info (text-slate-500)
- **Tertiary content** — Least important (text-slate-400)

Use color, weight, and size to make the hierarchy obvious.

### Size Isn't Everything
Don't rely on font size alone. Better tools:
- **Font weight:** 400-500 normal, 600-700 emphasis
- **Color:** Dark for primary, grey for secondary
- Avoid weights under 400—use lighter color instead

### Emphasize by De-emphasizing
When something won't stand out, de-emphasize the competition:

```html
<!-- Don't: Make active item louder -->
<a class="text-blue-600 font-bold">Active</a>
<a class="text-slate-700">Other</a>

<!-- Do: Make inactive items quieter -->
<a class="text-slate-900">Active</a>
<a class="text-slate-400">Other</a>
```

If a sidebar competes with main content, remove its background color entirely.

### Labels Are a Last Resort

**Often you don't need labels:**
- `janedoe@example.com` — obviously an email
- `(555) 765-4321` — obviously a phone
- `$19.99` — obviously a price

**Combine labels with values:**
- Instead of "In stock: 12" → "12 left in stock"
- Instead of "Bedrooms: 3" → "3 bedrooms"

**When you need labels, make them secondary:**
```html
<div>
  <span class="text-xs text-slate-500 uppercase tracking-wide">Revenue</span>
  <span class="text-2xl font-semibold text-slate-900">$45,231</span>
</div>
```

### Semantic Hierarchy ≠ Visual Hierarchy
An `<h1>` doesn't have to be huge. Section titles often work better small:

```html
<h1 class="text-sm font-medium text-slate-500 uppercase tracking-wide">
  Account Settings
</h1>
```

### Balance Weight and Contrast
**Icons feel heavy.** De-emphasize them:
```html
<span class="flex items-center gap-2">
  <Icon class="size-5 text-slate-400" />  <!-- softer -->
  <span class="text-slate-900">Label</span>  <!-- full contrast -->
</span>
```

**Thin borders too subtle?** Make them thicker, not darker:
```html
<div class="border-2 border-slate-200">...</div>  <!-- thicker, soft -->
```

### Button Hierarchy
Don't style by semantics alone. Style by importance:

```html
<!-- Primary: solid, high contrast -->
<button class="bg-blue-600 text-white">Save Changes</button>

<!-- Secondary: outline or muted -->
<button class="border border-slate-300 text-slate-700">Cancel</button>

<!-- Tertiary: link-style -->
<button class="text-slate-500 underline">Reset</button>
```

**Destructive ≠ always red and bold.** If "Delete" isn't the primary action, make it subtle. Show the scary red button in a confirmation modal where it IS the primary action.

---

## 3. Spacing & Layout

### Start with Too Much White Space
Don't add minimum spacing to not look bad. Start with way too much, then remove until happy. What seems like "too much" in isolation is often "just right" in context.

### Use a Spacing Scale
Tailwind 4 uses `--spacing: 0.25rem` (4px) as base:

```
p-1  = 0.25rem (4px)   — icon gaps, tight inline
p-2  = 0.5rem  (8px)   — compact buttons, tight lists
p-3  = 0.75rem (12px)  — form input padding
p-4  = 1rem    (16px)  — base padding, standard gaps
p-6  = 1.5rem  (24px)  — card padding, comfortable
p-8  = 2rem    (32px)  — section spacing
p-12 = 3rem    (48px)  — component groups
p-16 = 4rem    (64px)  — major sections
p-24 = 6rem    (96px)  — hero content
p-32 = 8rem    (128px) — dramatic page breaks
```

The scale should have ~25% jumps between adjacent values. 4px → 6px is imperceptible; 4px → 8px is noticeable.

### Don't Fill the Whole Screen
If content only needs 600px, use 600px. Don't stretch it. Extra width makes interfaces harder to interpret.

```html
<div class="max-w-2xl mx-auto">...</div>  <!-- centered, constrained -->
```

### Grids Are Overrated
Not everything should be fluid/percentage-based. **Sidebars should be fixed width:**

```html
<!-- Bad: sidebar grows/shrinks with viewport -->
<aside class="w-1/4">...</aside>

<!-- Good: sidebar stays optimal, main area flexes -->
<aside class="w-64 shrink-0">...</aside>
<main class="flex-1">...</main>
```

### Relative Sizing Doesn't Scale
A headline at 2.5× body size works on desktop but not mobile. Define sizes independently:
- Desktop: 18px body, 45px headline
- Mobile: 14px body, 24px headline (not 35px)

Large elements shrink faster than small elements at smaller screens.

### Avoid Ambiguous Spacing
Groups need definition. More space BETWEEN groups, less space WITHIN:

```html
<!-- Bad: equal spacing everywhere -->
<label>Name</label>      <!-- 16px gap -->
<input />                <!-- 16px gap -->
<label>Email</label>     <!-- 16px gap -->
<input />

<!-- Good: tight within groups, loose between -->
<label>Name</label>      <!-- 4px gap -->
<input />
                         <!-- 24px gap -->
<label>Email</label>     <!-- 4px gap -->
<input />
```

This applies everywhere: headings need more space above than below, list items shouldn't have line-height-sized gaps between them.

---

## 4. Typography

### Type Scale (Tailwind 4)
```
text-xs   = 0.75rem  (12px)  — captions, badges
text-sm   = 0.875rem (14px)  — secondary text, labels
text-base = 1rem     (16px)  — body text
text-lg   = 1.125rem (18px)  — lead paragraphs
text-xl   = 1.25rem  (20px)  — small headings
text-2xl  = 1.5rem   (24px)  — section headings
text-3xl  = 1.875rem (30px)  — page titles
text-4xl  = 2.25rem  (36px)  — hero headings
text-5xl  = 3rem     (48px)  — display
```

Avoid em units for scale—they compound when nested.

### Use Good Fonts
- **Safe default:** System font stack or neutral sans-serif
- **Quality indicator:** Fonts with 5+ weights are usually better crafted
- **Don't use headline fonts for body text** — they have tight letter-spacing and short x-height

### Line Length: 45-75 Characters
```html
<p class="max-w-prose">...</p>  <!-- 65ch, optimal -->
```

Wide images with narrow text is fine—different elements can have different widths.

### Line-Height Is Proportional
- **Small text (14-16px):** needs more line-height (leading-relaxed, 1.625)
- **Large headings (36px+):** needs less (leading-tight, 1.25)

Also: longer lines need more line-height. Eyes travel farther.

### Align Mixed Sizes by Baseline
```html
<div class="flex items-baseline">  <!-- not items-center -->
  <span class="text-2xl">$49</span>
  <span class="text-sm text-slate-500">/month</span>
</div>
```

### Don't Center Long Text
Center-alignment works for headlines and short blocks. Anything over 2-3 lines should be left-aligned. If one block in a centered group is too long, rewrite it shorter.

### Right-Align Numbers in Tables
Decimals line up, making comparison easy.

### Letter-Spacing
- **Tighten headlines:** `tracking-tight` for large text
- **Loosen all-caps:** `tracking-wide` for uppercase text

### Not Every Link Needs a Color
In link-heavy interfaces (navs, lists), colored links are overbearing:
```html
<a class="font-medium hover:underline">Link</a>  <!-- no special color -->
```

Reserve blue/underline for links in prose.

---

## 5. Color

### Use HSL (or oklch)
HSL makes relationships visible. Hex codes like #5C6AC4 and #14B8A6 look unrelated even if they're from the same palette.

Tailwind 4 uses oklch for wider gamut colors.

### You Need More Colors Than You Think
Real palette needs:
- **Greys:** 8-10 shades (text, backgrounds, borders)
- **Primary:** 5-10 shades (brand, CTAs, active states)
- **Accents:** 5-10 shades each for semantic states:
  - Red: errors, destructive, negative trends
  - Yellow/Amber: warnings
  - Green: success, positive trends

Total: potentially 100+ values across all colors.

### Define Shades Upfront
Don't use `lighten()` or `darken()`. Pick 9 shades (50-900) per color:
1. Pick base (500) — works as button background
2. Pick edges — darkest (900) for text, lightest (50/100) for tinted backgrounds
3. Fill gaps — 700, 300, then 800, 600, 400, 200

### Don't Let Lightness Kill Saturation
At extremes (very light/dark), saturation impact weakens. Compensate by:
- Increasing saturation for light/dark shades
- Rotating hue toward brighter colors for light shades (toward yellow/cyan/magenta)
- Rotating hue toward darker colors for dark shades (toward red/green/blue)

### Greys Need Saturation
Pure grey (0% saturation) feels lifeless. Tailwind provides:
- **Cool:** `slate` (blue undertone)
- **Neutral:** `gray`, `zinc`
- **Warm:** `stone` (slight warmth)

### Don't Use Grey Text on Colored Backgrounds
Grey text on white works because of reduced contrast. On colored backgrounds, pick a color with same hue but adjusted saturation/lightness:

```html
<!-- Bad: washed out -->
<div class="bg-blue-600 text-blue-600/50">...</div>

<!-- Good: hand-picked -->
<div class="bg-blue-600 text-blue-200">...</div>
```

### Accessibility
- Normal text: 4.5:1 contrast minimum
- Large text (18px+): 3:1 minimum

**Flip the contrast** when colored backgrounds are tricky:
```html
<!-- Hard to get 4.5:1 -->
<span class="bg-blue-500 text-white">Badge</span>

<!-- Easier and less attention-grabbing -->
<span class="bg-blue-100 text-blue-800">Badge</span>
```

### Don't Rely on Color Alone
Colorblind users need secondary indicators:
```html
<!-- Bad: color only -->
<span class="text-red-500">-12%</span>

<!-- Good: color + icon -->
<span class="text-red-500 flex items-center gap-1">
  <IconArrowDown class="size-4" /> -12%
</span>
```

---

## 6. Depth & Shadows

### Light Comes from Above
- **Top edges** catch light → slightly lighter
- **Bottom edges** in shadow → slightly darker
- **Below elements** → cast shadow

### Raised Elements
```html
<button class="bg-blue-500 shadow-md 
               border-t border-blue-400">  <!-- lighter top edge -->
  Button
</button>
```

Shadows below should be short offset, minimal blur (1-4px). Real shadows are sharp.

### Inset Elements (inputs, wells)
```html
<input class="shadow-inner border-b border-white" />
<!-- shadow at top (blocked light), lighter bottom edge (catches light) -->
```

### Shadow Elevation System
Closer = larger shadow = more attention.

```
shadow-sm  — buttons at rest, subtle lift
shadow     — cards, default
shadow-md  — dropdowns, popovers
shadow-lg  — cards on hover, sticky headers
shadow-xl  — modals, dialogs
shadow-2xl — full-screen overlays
```

### Interactive Shadows
```html
<!-- Lift on grab -->
<div class="shadow-sm active:shadow-lg cursor-grab">Drag me</div>

<!-- Press on click -->
<button class="shadow-md active:shadow-sm">Click</button>
```

### Two-Part Shadows
Professional shadows combine:
1. **Large, soft:** simulates direct light source
2. **Small, tight:** simulates ambient occlusion (where light can't reach)

At higher elevations, the small shadow fades.

### Flat Design Can Have Depth
Without shadows, use color: lighter = closer, darker = further.

```html
<!-- Raised card (lighter than background) -->
<div class="bg-white">Card</div>
<body class="bg-slate-100">

<!-- Inset well (darker than background) -->
<div class="bg-slate-200">Well</div>
```

**Solid shadows** work for flat aesthetics:
```html
<div class="shadow-[0_4px_0_0_theme(colors.slate.300)]">Card</div>
```

### Overlap to Create Layers
Break elements out of their containers:
```html
<section class="bg-slate-800 pb-16">Hero</section>
<div class="-mt-12 bg-white rounded-lg shadow-lg">Card overlaps hero</div>
```

When images overlap, add invisible border matching background to prevent clashing:
```html
<div class="flex -space-x-3">
  <img class="ring-2 ring-white rounded-full" />
  <img class="ring-2 ring-white rounded-full" />
</div>
```

---

## 7. Images

### Use Good Photos
Bad photos ruin good designs. Either hire a photographer or use quality stock (Unsplash). Never design with placeholders expecting to swap in phone photos later.

### Text Over Images Needs Consistent Contrast
Images have light and dark areas that compete with text. Solutions:
- **Overlay:** Semi-transparent black/white layer
- **Lower contrast:** Reduce image contrast, adjust brightness
- **Colorize:** Desaturate + multiply blend with brand color
- **Text shadow:** Large blur, no offset (like a glow)

```html
<div class="relative">
  <img class="absolute inset-0" />
  <div class="absolute inset-0 bg-black/40"></div>  <!-- overlay -->
  <h1 class="relative text-white">Headline</h1>
</div>
```

### Respect Intended Sizes
- Don't scale 16-24px icons to 64px — they look chunky
- Don't shrink full screenshots — text becomes illegible
- Redraw favicons at 16px instead of shrinking logos

**If icons are too small,** wrap in a shape:
```html
<div class="size-12 bg-blue-100 rounded-full flex items-center justify-center">
  <Icon class="size-5 text-blue-600" />
</div>
```

### User-Uploaded Content
You can't control quality. Protect your layout:
```html
<!-- Force aspect ratio -->
<img class="aspect-square object-cover" />

<!-- Prevent background bleed -->
<img class="ring-1 ring-black/5" />
```

---

## 8. Finishing Touches

### Supercharge Defaults
- Replace bullets with icons (checkmarks, custom icons)
- Promote quotation marks into large decorative elements
- Style links with thick colored underlines
- Use branded colors for checkboxes/radios

### Add Color with Accent Borders
No graphic design skills? Add colored borders:
```html
<div class="border-t-4 border-blue-500">Card</div>
<div class="border-l-4 border-amber-500">Alert</div>
<a class="border-b-2 border-blue-500">Active nav</a>
```

### Decorate Backgrounds
- Change background color between sections
- Use subtle gradients (hues within 30°)
- Add faint repeating patterns
- Place simple geometric shapes

Keep contrast low so nothing interferes with content.

### Don't Overlook Empty States
Empty states are first impressions. Don't show:
```
[Filters that don't work]
No items yet.
```

Do show:
```
[Illustration]
Create your first project
Get started by adding something new.
[+ Add Project]
```

Hide UI that doesn't work yet. Use the space to encourage action.

### Use Fewer Borders
Before adding a border, try:
- **Box shadow:** More subtle separation
- **Different backgrounds:** Adjacent elements with different colors
- **More spacing:** Simply increase the gap

Borders are heavy. Use them as a last resort.

### Think Outside the Box
- Dropdowns can have sections, columns, icons, images
- Tables can combine columns, add hierarchy, use color
- Radio buttons can be selectable cards
- Forms can be multi-column

Don't accept that components must look the way you've always seen them.

---

## Reference Files

For detailed code examples and edge cases:
- **[references/code-examples.md](references/code-examples.md)** — Full component examples (cards, forms, nav, tables, modals, heroes)
- **[references/hierarchy.md](references/hierarchy.md)** — Emphasis, de-emphasis, labels, weight/contrast balance
- **[references/spacing-layout.md](references/spacing-layout.md)** — White space, spacing systems, grids, responsive sizing
- **[references/typography.md](references/typography.md)** — Type scale, font selection, line length/height, alignment
- **[references/color.md](references/color.md)** — HSL/oklch, palette building, shade definition, accessibility
- **[references/depth-shadows.md](references/depth-shadows.md)** — Light source, elevation system, two-part shadows, overlapping layers
- **[references/finishing-touches.md](references/finishing-touches.md)** — Accent borders, empty states, background decoration, images
