# Typography

## Contents
1. [Type Scale](#type-scale)
2. [Choosing Fonts](#choosing-fonts)
3. [Line Length](#line-length)
4. [Line Height](#line-height)
5. [Alignment](#alignment)
6. [Letter Spacing](#letter-spacing)
7. [Links](#links)

## Type Scale

### Why Modular Scales Fall Short
Mathematical ratios (4:5, golden ratio) sound elegant but:
- Create fractional pixel values (31.25px, 39.063px)
- Often lack sizes you actually need
- Too rigid for UI work

### Hand-Crafted Scale
Tailwind 4 provides a well-designed type scale:

```css
/* Tailwind 4 default type scale */
text-xs    = 0.75rem   (12px)   /* captions, badges */
text-sm    = 0.875rem  (14px)   /* secondary text, labels */
text-base  = 1rem      (16px)   /* body text */
text-lg    = 1.125rem  (18px)   /* lead paragraphs */
text-xl    = 1.25rem   (20px)   /* small headings */
text-2xl   = 1.5rem    (24px)   /* section headings */
text-3xl   = 1.875rem  (30px)   /* page titles */
text-4xl   = 2.25rem   (36px)   /* hero headings */
text-5xl   = 3rem      (48px)   /* display text */
text-6xl   = 3.75rem   (60px)   /* large display */
text-7xl   = 4.5rem    (72px)   /* extra large display */
text-8xl   = 6rem      (96px)   /* massive display */
text-9xl   = 8rem      (128px)  /* jumbo display */
```

### Avoid Em Units for Scale
Em units compound when nested. If parent is 1.25em (20px), child at 0.875em becomes 17.5px—not in your scale.

Use `px` or `rem` to guarantee you stay on-scale.

## Choosing Fonts

### Safe Defaults
For UI, start with neutral sans-serifs. System fonts are reliable:

```css
font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", 
             Roboto, "Helvetica Neue", Arial, sans-serif;
```

### Quality Indicators
**Look for fonts with 5+ weights** (10+ including italics). More weights usually means more craftsmanship.

### Legibility Check
Fonts meant for headlines have:
- Tighter letter-spacing
- Shorter x-height (lowercase height)

**Don't use headline fonts for body text.** If it looks condensed or has a short x-height, it's for large sizes only.

### Stealing Fonts
Inspect sites you admire. Design teams put thought into typography—borrow their choices.

## Line Length

### The Sweet Spot: 45-75 Characters
Use `max-w-prose` (65ch) for optimal readability.

```css
/* Tailwind 4 */
.prose { @apply max-w-prose; }  /* 65ch */
/* or */
.prose { max-width: 65ch; }
```

### Mixing Line Lengths
Wide images with narrow text is fine—different elements can have different widths:

```html
<!-- Tailwind 4 -->
<article>
  <img class="w-full max-w-4xl" />  <!-- 56rem/896px -->
  <p class="max-w-prose">...</p>    <!-- 65ch -->
</article>
```

## Line Height

### It's Proportional
- **Small text (14-16px):** needs more line-height (1.5-1.75)
- **Large headings (36px+):** needs less (1.1-1.25)

```css
/* Inverse relationship */
.body-text { font-size: 16px; line-height: 1.6; }
.heading { font-size: 48px; line-height: 1.1; }
```

### Line Length Affects It Too
Longer lines need more line-height—eyes have farther to travel back:

```css
/* Narrow column: can be tighter */
.sidebar p { max-width: 25ch; line-height: 1.4; }

/* Wide column: needs more */
.main p { max-width: 75ch; line-height: 1.75; }
```

## Alignment

### Left-Align by Default
For English and most languages, left-align everything except:

### Center Alignment
Good for:
- Short headlines
- Brief, independent text blocks
- Call-to-action sections

Bad for:
- Anything over 2-3 lines
- Long-form content

If centering but one block is too long, rewrite shorter.

### Right-Align Numbers
In tables, right-align for easy comparison—decimal points line up:

```
  1,234.56
    567.89
 12,345.00
```

### Justified Text
If used, enable hyphenation to avoid awkward gaps:

```css
.justified {
  text-align: justify;
  hyphens: auto;
}
```

### Baseline Alignment
When mixing font sizes on one line, align by baseline (where letters sit), not center:

```css
.flex-row {
  display: flex;
  align-items: baseline;  /* not center */
}
```

## Letter Spacing

### Tighten Headlines
Wide-spaced fonts can be tightened for headlines:

```css
.headline {
  font-family: "Open Sans", sans-serif;
  letter-spacing: -0.02em;  /* slightly tighter */
}
```

### Loosen All-Caps
Uppercase text needs more breathing room:

```css
.caps {
  text-transform: uppercase;
  letter-spacing: 0.05em;  /* wider for legibility */
}
```

## Links

### Not Every Link Needs Color
In link-heavy interfaces (navs, lists), colored links are overbearing:

```css
/* Subtle by default */
.nav-link { color: inherit; font-weight: 500; }
.nav-link:hover { color: var(--primary); }

/* Or underline on hover only */
.list-link { color: inherit; text-decoration: none; }
.list-link:hover { text-decoration: underline; }
```

Reserve traditional blue/underline for links within prose where they need to "pop."
