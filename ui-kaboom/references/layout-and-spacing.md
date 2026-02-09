# Layout and Spacing

Detailed guidance on sizing elements and distributing space to create clean, organized interfaces.

---

## Start with Too Much White Space

White space should be removed, not added.

**The Problem:**
When designing for the web, white space is almost always added — if something looks cramped, you add margin or padding until it looks better. This gives elements only the minimum breathing room necessary to not look actively bad.

**The Better Approach:**
Start by giving something way too much space, then remove it until you're happy. What might seem like "a little too much" when focused on an individual element ends up being closer to "just enough" in a complete UI.

**Dense UIs Have Their Place:**
Dashboards where a lot of information needs to be visible at once can be compact. The important thing is making density a deliberate decision, not the default.

---

## Establish a Spacing and Sizing System

Limit yourself to a constrained set of spacing and sizing values, defined in advance.

**A Linear Scale Won't Work:**
"Make everything a multiple of 4px" doesn't help you choose between 120px and 125px. The system needs to consider the **relative difference** between adjacent values:
- 12px → 16px = 33% increase — very noticeable
- 500px → 520px = 4% increase — barely perceptible

**Rule:** No two values should be closer than about 25%.

**Defining the System:**
Start with **16px** as a base (it divides nicely, default browser font size). Values at the small end are packed together, progressively more spaced going up.

**Practical scale:**
```
4, 8, 12, 16, 24, 32, 48, 64, 96, 128, 192, 256, 384, 512, 640, 768
```

**Tailwind equivalents:**
```
p-1=4px    p-2=8px    p-3=12px   p-4=16px
p-6=24px   p-8=32px   p-12=48px  p-16=64px
p-24=96px  p-32=128px p-48=192px p-64=256px
```

**Using the System:**
1. Need space? Grab a value from the scale
2. Not enough? Try the next value
3. A subtle consistency emerges across designs

---

## You Don't Have to Fill the Whole Screen

Just because you have the space doesn't mean you need to use it.

If you only need 600px, use 600px. On high resolution displays with 1200-1400px of space, spreading things out just makes interfaces harder to interpret.

```html
<div class="max-w-2xl mx-auto">...</div>  <!-- centered, constrained -->
```

**Shrink the Canvas:**
Start with ~400px and design mobile layout first. Once happy, bring it to a larger screen and adjust. You won't change as much as you think.

**Think in Columns:**
If narrow content feels unbalanced in a wide layout, split into columns instead of making it wider. A narrow form + supporting text in a separate column feels balanced without compromising optimal form width.

---

## Grids Are Overrated

Outsourcing all layout decisions to a grid can do more harm than good.

**Not All Elements Should Be Fluid:**
Using a 12-column grid, a sidebar at 25% gets too wide on large screens and too narrow on small screens.

**Better approach — fixed width:**
```html
<!-- Bad: sidebar scales with viewport -->
<aside class="w-1/4">...</aside>

<!-- Good: sidebar stays optimal, main flexes -->
<aside class="w-64 shrink-0">...</aside>
<main class="flex-1">...</main>
```

**Don't Shrink Until You Need To:**
If 500px is optimal for a card, why should it shrink when there's space? Use `max-width` and only force shrinking when the screen gets smaller:

```html
<div class="max-w-lg w-full">...</div>
```

**Key Takeaway:**
Don't be a slave to the grid. Give components the space they need. Don't use percentages unless you actually want something to scale.

---

## Relative Sizing Doesn't Scale

Don't be fooled into believing that relationships defined with relative units can remain static across screen sizes.

**The Problem:**
Body copy at 18px with headlines at 2.5em (45px) works on desktop. On mobile, if body shrinks to 14px, 2.5em gives 35px — way too big. A better headline size for small screens is 20-24px (only 1.5-1.7x).

**Rule:** Elements that are large on large screens need to shrink faster than elements that are already small. The difference between small and large elements should be less extreme at small screen sizes.

**Relationships Within Elements:**
Buttons too. Don't define padding relative to font size. Instead:
- Padding gets **more generous** at larger sizes
- Padding gets **disproportionately tighter** at smaller sizes

This makes a large button actually feel like a larger button, not just zoomed in.

**Key Takeaway:** Let go of proportional scaling. Fine-tune things independently for each context.

---

## Avoid Ambiguous Spacing

Whenever relying on spacing to connect elements, always make sure there's more space *around* the group than *within* it.

**The Problem:**
When margin below a label equals margin below the input, the form group doesn't feel connected. Users might put data in the wrong field.

**Fix:**
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

**Where This Shows Up:**
- **Headings:** Not enough space above section headings makes it unclear which section they belong to
- **Bulleted lists:** When bullet spacing matches single-bullet line-height
- **Horizontal layouts:** Components side by side with same ambiguity

**The Rule:** More space around a group than within the group. Always.
