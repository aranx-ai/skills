# Creating Depth

## Contents
1. [Light Source Principle](#light-source-principle)
2. [Raised Elements](#raised-elements)
3. [Inset Elements](#inset-elements)
4. [Shadow Elevation System](#shadow-elevation-system)
5. [Two-Part Shadows](#two-part-shadows)
6. [Flat Design Depth](#flat-design-depth)
7. [Overlapping Layers](#overlapping-layers)

## Light Source Principle

### Light Comes from Above
Imagine a light source above and slightly in front of the screen:
- **Top edges** receive more light → slightly lighter
- **Bottom edges** receive less light → slightly darker
- **Below elements** are blocked from light → shadows

This is how our brains interpret depth—use it consistently.

## Raised Elements

### Buttons Example
A button raised off the page:

```css
.btn {
  background: hsl(220, 80%, 50%);
  
  /* Top edge: slightly lighter (catches light) */
  border-top: 1px solid hsl(220, 80%, 60%);
  /* Or use inset shadow */
  box-shadow: 
    inset 0 1px 0 hsl(220, 80%, 60%),
    /* Bottom shadow: blocked light below */
    0 1px 3px rgba(0, 0, 0, 0.2);
}
```

### Tips for Top Edges
- Pick lighter color by hand, not semi-transparent white (white overlay desaturates)
- Keep it subtle—1-2px is enough

### Shadow Below
- Short vertical offset (1-3px)
- Minimal blur (1-4px)
- Look at real shadows: window frames, outlets—they're sharp, not blurry

## Inset Elements

### Wells and Inputs
Elements that feel pressed into the page:

```css
.well {
  background: hsl(220, 10%, 96%);
  
  /* Top: shadow from lip above blocking light */
  box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.06);
  
  /* Bottom edge: catches light (slightly lighter) */
  border-bottom: 1px solid white;
}

.input {
  box-shadow: inset 0 1px 2px rgba(0, 0, 0, 0.1);
  border: 1px solid hsl(220, 10%, 80%);
}
```

## Shadow Elevation System

### Shadows Convey Z-Axis Position
Closer to user = larger shadow = more attention.

**Tailwind 4 Shadow Scale:**

```css
/* Built-in shadow utilities */
shadow-sm    /* Subtle lift: buttons at rest */
shadow       /* Default: cards */
shadow-md    /* Low elevation: dropdowns */
shadow-lg    /* Medium: cards on hover, sticky headers */
shadow-xl    /* High: modals, dialogs */
shadow-2xl   /* Highest: full-screen overlays */

/* Custom two-part shadows for refined depth */
@theme {
  --shadow-custom-sm: 
    0 1px 2px 0 rgb(0 0 0 / 0.05);
  --shadow-custom-md: 
    0 4px 6px -1px rgb(0 0 0 / 0.1),
    0 2px 4px -2px rgb(0 0 0 / 0.1);
  --shadow-custom-lg: 
    0 10px 15px -3px rgb(0 0 0 / 0.1),
    0 4px 6px -4px rgb(0 0 0 / 0.1);
}
```

### Interactive Shadows
Use shadow changes to show interaction:

```html
<!-- Tailwind 4: lift on grab -->
<div class="shadow-sm active:shadow-lg">Draggable</div>

<!-- Button: press down on click -->
<button class="shadow-md active:shadow-sm">Click me</button>
```

## Two-Part Shadows

### Why Two Shadows?
Real objects cast two types of shadows:
1. **Direct light shadow:** Large, soft, from main light source
2. **Ambient occlusion:** Small, tight, where ambient light can't reach

```css
.card {
  box-shadow:
    /* Large, soft: direct light */
    0 10px 20px rgba(0, 0, 0, 0.08),
    /* Small, tight: ambient occlusion */
    0 2px 6px rgba(0, 0, 0, 0.12);
}
```

### Elevation Affects Ratio
At low elevation, both shadows visible.
At high elevation, ambient shadow (small one) fades:

```css
/* Low elevation: both shadows distinct */
--shadow-low: 
  0 4px 8px rgba(0, 0, 0, 0.08),
  0 1px 3px rgba(0, 0, 0, 0.15);

/* High elevation: ambient shadow almost gone */
--shadow-high:
  0 25px 50px rgba(0, 0, 0, 0.15),
  0 3px 8px rgba(0, 0, 0, 0.05);  /* subtle */
```

## Flat Design Depth

### No Shadows? Use Color
Lighter objects feel closer, darker feel further:

```css
/* Raised card on flat design */
.card {
  background: white;  /* lighter than page */
}
body {
  background: hsl(220, 10%, 96%);  /* darker page */
}

/* Inset well */
.well {
  background: hsl(220, 10%, 92%);  /* darker than page */
}
```

### Solid Shadows
A flat-design-friendly shadow: sharp, no blur:

```css
.card {
  box-shadow: 0 4px 0 hsl(220, 10%, 80%);
}
```

Feels raised without the softness of realistic shadows.

## Overlapping Layers

### Break Out of Containers
Create depth by overlapping elements across boundaries:

```html
<!-- Tailwind 4: Card overlaps section boundary -->
<section class="pb-16 bg-gradient-to-b from-slate-800 to-slate-700">
  <!-- hero content -->
</section>
<div class="-mt-12 mx-4 bg-white rounded-lg shadow-lg">
  <!-- card pulls up into hero -->
</div>
```

### Overflow Both Sides
Make elements taller than their containers:

```html
<!-- Tailwind 4 -->
<div class="relative -top-6 -mb-12">
  <img class="testimonial-image" />
</div>
```

### Overlapping Images
When images overlap, add an "invisible border" matching background:

```html
<!-- Tailwind 4: avatar stack -->
<div class="flex -space-x-3">
  <img class="ring-3 ring-white rounded-full" />
  <img class="ring-3 ring-white rounded-full" />
</div>
```

Prevents ugly clashing at overlap points.
