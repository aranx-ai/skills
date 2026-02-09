# Spacing & Layout

## Contents
1. [White Space Philosophy](#white-space-philosophy)
2. [Spacing System](#spacing-system)
3. [Screen Real Estate](#screen-real-estate)
4. [Grids](#grids)
5. [Relative Sizing](#relative-sizing)
6. [Ambiguous Spacing](#ambiguous-spacing)

## White Space Philosophy

### Remove, Don't Add
Don't add minimum spacing needed to not look bad. Instead:
1. Give everything way too much space
2. Remove until happy with result

What seems like "too much" in isolation often becomes "just enough" in a complete UI.

### Dense UIs Have Their Place
Dashboards showing lots of data may need compact layouts. Make it a deliberate decision, not the default.

## Spacing System

### Why Linear Scales Fail
"Make everything a multiple of 4px" doesn't help choose between 120px and 125px.

The relative difference matters:
- 12px → 16px is a 33% increase (very noticeable)
- 500px → 520px is a 4% increase (barely visible)

### The Scale
Keep adjacent values at least ~25% apart. Tailwind 4 uses `--spacing: 0.25rem` (4px):

```
p-1   = 0.25rem (4px)   - tight: icon padding, inline spacing
p-2   = 0.5rem  (8px)   - compact: small buttons, tight lists
p-3   = 0.75rem (12px)  - snug: form input padding
p-4   = 1rem    (16px)  - base: standard padding, gaps
p-6   = 1.5rem  (24px)  - comfortable: card padding
p-8   = 2rem    (32px)  - roomy: section spacing
p-12  = 3rem    (48px)  - spacious: component groups
p-16  = 4rem    (64px)  - generous: major sections
p-24  = 6rem    (96px)  - expansive: hero content
p-32  = 8rem    (128px) - dramatic: page breaks
```

### Using the System
Need space under an element? Grab a value. Not enough? Try the next one up. Using a system makes design-by-elimination easy.

## Screen Real Estate

### Don't Fill the Screen
If you need 600px, use 600px. Extra width often makes interfaces harder to interpret.

```css
/* Don't force full-width for no reason */
.content { max-width: 65ch; }  /* 65 characters ≈ optimal reading */
/* Or use Tailwind: max-w-prose (65ch) or max-w-2xl (42rem/672px) */
```

### Shrink the Canvas
Design mobile-first on a ~400px canvas (`max-w-sm` = 24rem/384px). Most designs need fewer adjustments for desktop than expected.

### Think in Columns
Narrow content feeling unbalanced? Split into columns:

```
┌────────────────────────────────────────┐
│ Form Label              │  Form Input  │
│ Supporting text that    │  [________]  │
│ explains the field      │  [________]  │
└────────────────────────────────────────┘
```

## Grids

### Not Everything Should Be Fluid
12-column grids give everything percentage widths. But many elements work better with fixed widths:

**Sidebar example:**
```css
/* Bad: sidebar grows with viewport */
.sidebar { width: 25%; }

/* Good: sidebar stays optimal size */
.sidebar { width: 280px; flex-shrink: 0; }
.main { flex: 1; }  /* fills remaining space */
```

### Don't Shrink Until Necessary
Don't use percentage widths that shrink before they need to:

```css
/* Bad: card is smaller on large screens than medium */
.card { width: 50%; max-width: 500px; }

/* Good: card stays optimal until screen forces shrink */
.card { width: 100%; max-width: 500px; }
```

## Relative Sizing

### Proportional Scaling Doesn't Work
A 2.5em headline that looks perfect at 18px body copy becomes too big at 14px on mobile.

**Desktop:** 18px body → 45px headline (2.5×) ✓
**Mobile:** 14px body → 35px headline (2.5×) ✗ Too big!
**Better:** 14px body → 24px headline (1.7×) ✓

### Components Don't Scale Proportionally
Large buttons shouldn't just be zoomed-in small buttons:

```css
/* Small: tighter proportions */
.btn-sm { padding: 6px 12px; font-size: 14px; }

/* Large: more generous */  
.btn-lg { padding: 16px 32px; font-size: 18px; }
```

The large button has proportionally more padding—it feels larger, not just zoomed.

## Ambiguous Spacing

### Groups Need Definition
Without borders or backgrounds, spacing creates groups. Make sure:
- More space between groups
- Less space within groups

**Bad:**
```
Label           ← equal spacing
[Input]         ← can't tell which label belongs where
Label
[Input]
```

**Good:**
```
Label           ← tight
[Input]
                ← extra space
Label           ← tight
[Input]
```

### Applies Everywhere
- Section headings need more space above than below
- Bulleted list items shouldn't have line-height-sized gaps
- Horizontal layouts need the same care
