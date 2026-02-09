# Visual Hierarchy

Detailed guidance on controlling what users see first by establishing clear visual hierarchy.

---

## Not All Elements Are Equal

Visual hierarchy — how important elements appear in relation to one another — is the most effective tool you have for making something feel "designed."

When everything in an interface is competing for attention, it feels noisy and chaotic. When you deliberately de-emphasize secondary and tertiary information and highlight what's most important, the result is immediately more pleasing — even with the same color scheme, font, and layout.

---

## Size Isn't Everything

Relying too much on font size to control hierarchy often leads to primary content that's too large and secondary content that's too small.

**Use Font Weight and Color Instead:**
- Making a primary element **bolder** lets you use a more reasonable font size
- Using a **softer color** for supporting text instead of a tiny font size makes it secondary while preserving readability

**Recommended Approach:**
Two or three colors:
- **Dark color** for primary content (e.g., headline)
- **Grey** for secondary content (e.g., date published)
- **Lighter grey** for tertiary content (e.g., copyright notice)

Two font weights are usually enough:
- **Normal** (400 or 500) for most text
- **Heavier** (600 or 700) for emphasis

**Warning:** Stay away from font weights under 400 for UI work — they're too hard to read at smaller sizes. Use lighter color or smaller font size instead.

---

## Don't Use Grey Text on Colored Backgrounds

Making text lighter grey works on white backgrounds because it reduces contrast. On colored backgrounds, it looks washed out.

**Don't Reduce Opacity:**
White text with reduced opacity looks dull and sometimes disabled. On images or patterns, the background shows through.

**Hand-Pick Colors Instead:**
1. Choose a color with the **same hue** as the background
2. Adjust **saturation and lightness** until it looks right

```html
<!-- Bad: washed out -->
<div class="bg-blue-600 text-white/50">...</div>

<!-- Good: hand-picked -->
<div class="bg-blue-600 text-blue-200">...</div>
```

---

## Emphasize by De-emphasizing

Sometimes the main element isn't standing out enough, but there's nothing you can add to give it more emphasis. Instead, de-emphasize the elements competing with it.

**Example — Active Navigation:**
Instead of making the active item louder (bolder, colored), give inactive items a softer color so they recede.

```html
<!-- Don't: Make active item louder -->
<a class="text-blue-600 font-bold">Active</a>
<a class="text-slate-700">Other</a>

<!-- Do: Make inactive items quieter -->
<a class="text-slate-900">Active</a>
<a class="text-slate-400">Other</a>
```

**Apply to Larger Pieces:**
If a sidebar competes with main content, don't give it a background color — let the content sit directly on the page background.

---

## Labels Are a Last Resort

Avoid defaulting to a naive label:value format — it makes it difficult to present data with hierarchy.

**You Might Not Need a Label:**
- `janedoe@example.com` — obviously an email
- `(555) 765-4321` — obviously a phone number
- `$19.99` — obviously a price
- "Customer Support" listed below a name — context makes it obvious

**Combine Labels and Values:**
- Instead of "In stock: 12" → "12 left in stock"
- Instead of "Bedrooms: 3" → "3 bedrooms"

**When You Need Labels, De-emphasize Them:**
```html
<div>
  <span class="text-xs text-slate-500 uppercase tracking-wide">Revenue</span>
  <span class="text-2xl font-semibold text-slate-900">$45,231</span>
</div>
```

**When to Emphasize Labels:**
On information-dense pages (technical specs), emphasize labels when users scan for category names, not values. Use darker color for labels, slightly lighter for values.

---

## Separate Visual Hierarchy from Document Hierarchy

Don't let the HTML element influence styling. Pick elements for semantics, style them for visual hierarchy.

Section titles often act more like labels than headings — they support the content, not steal attention:

```html
<h1 class="text-sm font-medium text-slate-500 uppercase tracking-wide">
  Account Settings
</h1>
```

Taken to the extreme, you might include titles in markup for accessibility but hide them visually because the content speaks for itself.

---

## Balance Weight and Contrast

Bold text feels emphasized because it covers more surface area. This relationship applies to all UI elements.

**Icons Feel Heavy:**
Solid icons cover a lot of surface area. To balance them with text, lower their contrast:
```html
<span class="flex items-center gap-2">
  <Icon class="size-5 text-slate-400" />  <!-- softer -->
  <span class="text-slate-900">Label</span>  <!-- full contrast -->
</span>
```

**Thin Borders Too Subtle:**
If a thin 1px border with soft color is too subtle but darkening it feels harsh, make it thicker instead:
```html
<div class="border-2 border-slate-200">...</div>  <!-- thicker, soft -->
```

---

## Semantics Are Secondary (Actions)

When there are multiple actions on a page, don't design based purely on semantics — hierarchy matters more.

**The Action Hierarchy:**
- **Primary actions:** Obvious. Solid, high contrast background.
- **Secondary actions:** Clear but not prominent. Outline or lower contrast background.
- **Tertiary actions:** Discoverable but unobtrusive. Link-style.

```html
<!-- Primary -->
<button class="bg-blue-600 text-white">Save Changes</button>

<!-- Secondary -->
<button class="border border-slate-300 text-slate-700">Cancel</button>

<!-- Tertiary -->
<button class="text-slate-500 underline">Reset</button>
```

**Destructive Actions:**
Being destructive doesn't mean big, red, and bold. If "Delete" isn't the primary action, give it secondary or tertiary treatment. Show the scary red button in a confirmation dialog where it IS the primary action.
