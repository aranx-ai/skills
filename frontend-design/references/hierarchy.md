# Visual Hierarchy

## Contents
1. [Emphasizing Elements](#emphasizing-elements)
2. [De-emphasizing Elements](#de-emphasizing-elements)
3. [Handling Labels](#handling-labels)
4. [Semantic vs Visual Hierarchy](#semantic-vs-visual-hierarchy)
5. [Balance Weight and Contrast](#balance-weight-and-contrast)

## Emphasizing Elements

### Size Isn't Everything
Relying too much on font size leads to primary content that's too large and secondary content that's too small.

**Better tools for emphasis:**
- Font weight (400-500 normal, 600-700 emphasis)
- Color contrast (dark for primary, grey for secondary)
- Position and spacing

### Two Font Weights Are Enough
- Normal: 400 or 500 (depending on font)
- Heavy: 600 or 700 for emphasis

Avoid weights under 400 for UI—use lighter color or smaller size instead.

### Three Colors for Text
1. Dark color — primary content (headlines, important text)
2. Grey — secondary content (dates, metadata)
3. Lighter grey — tertiary content (footnotes, copyright)

## De-emphasizing Elements

### Emphasize by De-emphasizing
When something won't stand out despite your efforts, de-emphasize the competition instead:

```html
<!-- Tailwind 4: De-emphasize inactive items -->
<nav>
  <a class="text-slate-400">Inactive</a>
  <a class="text-slate-900 font-medium">Active</a>
</nav>
```

### Let Content Breathe
If a sidebar competes with main content, remove its background color—let content sit directly on the page background.

## Handling Labels

### Labels Are a Last Resort
Often you don't need labels at all:
- `janedoe@example.com` is obviously an email
- `(555) 765-4321` is obviously a phone number
- `$19.99` is obviously a price

### Combine Labels and Values
Instead of "In stock: 12", try "12 left in stock"
Instead of "Bedrooms: 3", try "3 bedrooms"

### When You Need Labels
If labels are necessary (e.g., dashboards with similar data types):
- Make labels secondary: smaller, lower contrast, lighter weight
- The data is primary, labels are supporting

### When to Emphasize Labels
On info-dense pages (like technical specs), users scan for labels:
- User looks for "depth", not "7.6mm"
- Use darker color for labels, slightly lighter for values

## Semantic vs Visual Hierarchy

### Don't Let HTML Tags Dictate Style
Using `<h1>` doesn't mean it needs to be huge:

```html
<!-- Tailwind 4: Semantic h1 but visually restrained -->
<h1 class="text-sm font-semibold text-slate-500 uppercase tracking-wide">
  Page Title
</h1>
```

Section titles often work better as small, supportive labels—not attention-grabbing headings.

## Balance Weight and Contrast

### Icons Feel Heavy
Solid icons cover more surface area than text. To balance:

```html
<!-- Tailwind 4: De-emphasize icons next to text -->
<span class="flex items-center gap-2">
  <svg class="text-slate-400 size-5">...</svg>
  <span class="text-slate-900">Label text</span>
</span>
```

### Thin Borders Need Help
If 1px borders look too subtle in a soft color but harsh in dark color:

```html
<!-- Tailwind 4: Make it slightly thicker instead of darker -->
<div class="border-2 border-slate-200">...</div>
```
