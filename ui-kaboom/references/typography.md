# Typography

Detailed guidance on typography choices that make text look great and easy to read.

---

## Establish a Type Scale

Most interfaces use way too many font sizes. Define a type system for consistency and speed.

**The Problem:**
Without a rigid system, every pixel value from 10px to 24px appears somewhere, creating inconsistencies and slowing workflow.

**Modular Scales:**
Calculate using a ratio (4:5 "major third", 2:3 "perfect fifth", golden ratio 1:1.618). Problems:
1. Fractional values (31.25px, 39.063px) — browsers handle subpixel rounding differently
2. Too few sizes for interface design — the jumps are too limiting

**Hand-Crafted Scales (Recommended):**
Pick values by hand. No rounding errors, total control.

**Practical scale:**
```
12, 14, 16, 18, 20, 24, 30, 36, 48, 60, 72
```

**Tailwind equivalents:**
```
text-xs   = 0.75rem  (12px)  — captions, badges
text-sm   = 0.875rem (14px)  — secondary text, labels
text-base = 1rem     (16px)  — body text
text-lg   = 1.125rem (18px)  — lead paragraphs
text-xl   = 1.25rem  (20px)  — small headings
text-2xl  = 1.5rem   (24px)  — section headings
text-3xl  = 1.875rem (30px)  — page titles
text-4xl  = 2.25rem  (36px)  — hero headings
text-5xl  = 3rem     (48px)  — display text
```

**Avoid em Units:**
em units are relative to the current font size. Nested elements compute to values not in your scale (e.g., 1.25em inside 20px = nested 0.875em computes to 17.5px — not in any scale). Stick to **px or rem**.

---

## Use Good Fonts

Developing an eye for typefaces takes years. Shortcuts to start now:

**Play It Safe:**
For UI design, use a fairly neutral sans-serif. If you don't trust your taste, use the system font stack:
```
-apple-system, Segoe UI, Roboto, Noto Sans, Ubuntu, Cantarell, Helvetica Neue
```

**Filter by Weight Count:**
Typefaces with many weights (5+) tend to be crafted with more care. On Google Fonts, filter by 10+ styles (accounting for italics) — this cuts out 85% of options, leaving fewer than 50 sans-serifs.

**Optimize for Legibility:**
- **Headline fonts:** tighter letter-spacing, shorter x-height
- **Body fonts:** wider letter-spacing, taller x-height
- Avoid condensed typefaces with short x-heights for main UI text

**Trust Popularity:**
Popular fonts are usually good fonts. Sort by popularity to limit choices.

**Steal from Great Sites:**
Inspect favorite sites and note their typefaces. Great design teams choose excellent fonts you might never find otherwise.

---

## Keep Your Line Length in Check: 45-75 Characters

**The Problem:**
Fitting text to layout instead of creating the best reading experience usually means lines that are too long.

**The Solution:**
Use em units for paragraph width: **20-35em** = 45-75 characters per line.

```html
<p class="max-w-prose">...</p>  <!-- 65ch, optimal -->
```

**Mixing Widths:**
If content area needs to be wider for images, still limit paragraph width. Different widths in the same content area looks more polished.

---

## Baseline, Not Center

When mixing font sizes on a single line, align by baseline — not vertical center.

**The Problem:**
Vertically centering mixed sizes (large title + small actions) creates an awkward misalignment when text is close together.

**The Solution:**
```html
<div class="flex items-baseline">  <!-- not items-center -->
  <span class="text-2xl">$49</span>
  <span class="text-sm text-slate-500">/month</span>
</div>
```

Baseline alignment uses an alignment reference your eyes already perceive — the result is simpler and cleaner.

---

## Line-Height Is Proportional

The right line-height depends on both line length and font size.

**Line-Height and Width:**
Longer lines need more line-height because eyes travel further horizontally:
- **Narrow content:** shorter line-height (1.5)
- **Wide content:** taller line-height (up to 2)

**Line-Height and Font Size:**
- **Small text** (14-16px): extra spacing helps eyes find the next line → `leading-relaxed` (1.625)
- **Large headings** (36px+): no extra spacing needed → `leading-tight` (1.25) or even `leading-none` (1)

**Rule:** Line-height and font size are inversely proportional.

---

## Not Every Link Needs a Color

In interfaces where almost everything is a link, making them all "pop" is overbearing.

**In Paragraph Text:**
Links in non-link text should stand out and look clickable — use color and/or underline.

**In Navigation and UI:**
Emphasize subtly:
- Heavier font weight
- Darker color
- Underline or color change on hover only

Ancillary links that aren't part of the main user path: style on hover only. They'll be discoverable without competing for attention.

---

## Align with Readability in Mind

Text should be aligned to match the reading direction. For English: left-aligned by default.

**Don't Center Long Text:**
Center-alignment works for headlines and short blocks. Anything over 2-3 lines should be left-aligned. If centered text is too long, rewrite it shorter.

**Right-Align Numbers:**
When decimals line up, numbers are easy to compare at a glance.

**Justified Text:**
For a formal look, always enable hyphenation with justified text to avoid awkward word gaps. Best for mimicking print (online magazines, newspapers).

---

## Use Letter-spacing Effectively

Generally trust the typeface designer. Two exceptions:

**Tighten Headlines:**
Fonts designed for small-size legibility (Open Sans) have wider built-in letter-spacing. For headlines, decrease it:
```html
<h1 class="tracking-tight">Large Heading</h1>
```

Don't try the reverse — headline fonts rarely work at small sizes even with increased spacing.

**Widen All-Caps:**
All-caps text has less visual variety (every letter same height). Increase letter-spacing to improve readability:
```html
<span class="uppercase tracking-wide text-xs font-medium">
  Section Label
</span>
```
