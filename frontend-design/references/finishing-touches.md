# Finishing Touches

## Contents
1. [Supercharge Defaults](#supercharge-defaults)
2. [Accent Borders](#accent-borders)
3. [Background Decoration](#background-decoration)
4. [Empty States](#empty-states)
5. [Fewer Borders](#fewer-borders)
6. [Think Outside the Box](#think-outside-the-box)
7. [Images](#images)

## Supercharge Defaults

### Replace Bullets with Icons
```html
<!-- Before: boring bullets -->
<ul>
  <li>Secure encryption</li>
  <li>24/7 support</li>
</ul>

<!-- After: meaningful icons -->
<ul class="icon-list">
  <li><IconLock /> Secure encryption</li>
  <li><IconSupport /> 24/7 support</li>
</ul>
```

Checkmarks and arrows work for generic lists. Use specific icons when content allows (padlock for security, etc.).

### Promote Quotation Marks
Make quotes into visual elements:

```css
.testimonial::before {
  content: """;
  font-size: 4rem;
  color: var(--primary-200);
  position: absolute;
  top: -1rem;
  left: -0.5rem;
}
```

### Style Links Creatively
```css
/* Thick colored underline */
.fancy-link {
  text-decoration: none;
  background-image: linear-gradient(
    to bottom,
    var(--primary-200) 0%,
    var(--primary-200) 100%
  );
  background-position: 0 1.1em;
  background-repeat: no-repeat;
  background-size: 100% 0.4em;
}
```

### Custom Form Controls
Replace browser defaults with branded versions:

```css
/* Custom checkbox */
.checkbox:checked {
  background: var(--primary-500);
  border-color: var(--primary-500);
}

/* Custom radio */
.radio:checked::before {
  background: var(--primary-500);
}
```

Even just using brand colors for selected states elevates the design.

## Accent Borders

### Add Color Without Graphics
No illustration skills? Add colored borders:

```html
<!-- Tailwind 4 examples -->
<!-- Top of card -->
<div class="border-t-4 border-blue-500 rounded-lg">...</div>

<!-- Side of alert -->
<div class="border-l-4 border-amber-500 bg-amber-50 p-4">...</div>

<!-- Active nav item -->
<a class="border-b-2 border-blue-500">Active</a>

<!-- Under headline -->
<h2 class="after:content-[''] after:block after:w-12 after:h-1 
           after:bg-blue-500 after:mt-2">Heading</h2>

<!-- Top of entire layout -->
<body class="before:content-[''] before:block before:h-1 
             before:bg-gradient-to-r before:from-blue-500 before:to-purple-500">
```

### Gradient Accents
Use gradients for more energy:

```html
<!-- Tailwind 4: gradient border top -->
<div class="border-t-4 border-transparent 
            [border-image:linear-gradient(to_right,#6366f1,#8b5cf6)_1]">
</div>
```

## Background Decoration

### Change Background Color
Break monotony by sectioning with color:

```css
.features-section {
  background: hsl(220, 20%, 97%);  /* slightly off-white */
}

.cta-section {
  background: linear-gradient(to right, hsl(220, 60%, 50%), hsl(240, 60%, 55%));
  color: white;
}
```

Keep gradient hues within ~30° for best results.

### Repeating Patterns
Subtle patterns add texture without distraction:

```css
.hero {
  background-color: #1e3a5f;
  position: relative;
}
.hero::after {
  content: "";
  position: absolute;
  inset: 0;
  background-image: url("pattern.svg");
  background-size: 80px;
  opacity: 0.05;  /* keep it subtle — only affects the pattern layer */
  pointer-events: none;
}
```

Edge patterns work too—doesn't need to cover everything.

### Simple Shapes
Add geometric elements in specific positions:

```css
.hero::before {
  content: "";
  position: absolute;
  right: -100px;
  top: 50%;
  width: 400px;
  height: 400px;
  background: radial-gradient(circle, var(--primary-100) 0%, transparent 70%);
  z-index: 0;
}
```

### World Maps, Blobs, etc.
Simplified illustrations work as backgrounds. Keep contrast low.

## Empty States

### Don't Neglect Them
Empty states are first impressions for new features. Don't show:

```
┌─────────────────────────────┐
│ [Filter] [Sort]             │
│                             │
│    No items yet.            │
│                             │
└─────────────────────────────┘
```

### Do This Instead
```
┌─────────────────────────────┐
│                             │
│        [Illustration]       │
│                             │
│    Create your first item   │
│    Get started by adding    │
│    something to your list   │
│                             │
│      [ + Add Item ]         │
│                             │
└─────────────────────────────┘
```

- Add illustration or icon
- Clear, encouraging copy
- Prominent call-to-action
- Hide filters/sorting that don't work yet

Empty states are opportunities to be interesting.

## Fewer Borders

### Borders Aren't the Only Separator

**Box shadows instead of borders:**
```css
/* Border approach */
.card { border: 1px solid #e5e7eb; }

/* Shadow approach (more subtle) */
.card { box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1); }
```

**Different backgrounds:**
```css
/* No border needed when colors differ */
.sidebar { background: #f8fafc; }
.main { background: white; }
```

**Spacing alone:**
```css
/* No divider needed with enough space */
.item + .item { margin-top: 2rem; }
```

### When to Use Borders
- When neither shadow nor background difference works
- When you need very clear hard separation
- In tables (though even then, zebra striping or spacing can work)

## Think Outside the Box

### Dropdowns Don't Have to Be Boring
Instead of a plain list:
- Break into sections
- Use multiple columns
- Add supporting text or icons
- Include imagery

### Tables Can Have Hierarchy
Combine columns, add visual interest:

```html
<!-- Before: flat data -->
<td>John Smith</td>
<td>john@example.com</td>
<td>Admin</td>

<!-- After: combined with hierarchy -->
<td>
  <div class="font-medium">John Smith</div>
  <div class="text-sm text-gray-500">john@example.com</div>
</td>
<td><span class="badge">Admin</span></td>
```

### Radio Buttons Can Be Cards
```html
<!-- Before: boring radios -->
<label><input type="radio"> Basic Plan</label>
<label><input type="radio"> Pro Plan</label>

<!-- After: selectable cards -->
<label class="plan-card">
  <input type="radio" class="sr-only">
  <div class="plan-name">Basic</div>
  <div class="plan-price">$9/mo</div>
  <ul class="plan-features">...</ul>
</label>
```

## Images

### Use Quality Photos
Bad photos ruin good designs. Either:
- Hire a photographer
- Use quality stock (Unsplash, etc.)

Never design with placeholders expecting to take your own photos later.

### Text Over Images Needs Contrast
Images are dynamic—light and dark areas compete with text.

**Solutions:**
- Semi-transparent overlay (dark for light text, light for dark text)
- Lower image contrast + adjust brightness
- Colorize image (desaturate + multiply blend with brand color)
- Text shadow (large blur, no offset—more like a glow)

```css
/* Overlay approach */
.hero-image::after {
  content: "";
  position: absolute;
  inset: 0;
  background: rgba(0, 0, 0, 0.4);
}

/* Text shadow approach */
.hero-text {
  text-shadow: 0 0 40px rgba(0, 0, 0, 0.5);
}
```

### Respect Intended Sizes
- Don't scale up 24px icons to 64px—they look chunky
- Don't shrink full screenshots—text becomes unreadable
- Redraw favicons at 16px instead of shrinking logos

**If icons are too small,** put them in a colored circle:
```html
<!-- Tailwind 4 -->
<div class="size-12 bg-blue-100 rounded-full flex items-center justify-center">
  <svg class="size-6 text-blue-600">...</svg>
</div>
```

### User-Uploaded Content
You can't control what users upload. Protect your layout:

```html
<!-- Tailwind 4: Force consistent aspect ratio -->
<img class="aspect-square object-cover" />

<!-- Prevent background bleed with ring -->
<img class="ring-1 ring-black/5 rounded-lg" />
```
