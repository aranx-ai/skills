# Working with Images

Detailed guidance on using photography and images effectively in designs.

---

## Use Good Photos

Bad photos ruin good designs, even if everything else looks great.

**Your Options:**
1. **Hire a professional photographer** — great photos are about lighting, composition, and color, not expensive cameras
2. **Use high quality stock** — sites like Unsplash offer beautiful photography for free

**The Cardinal Rule:**
Don't design with placeholder images and expect to swap in smartphone photos later. **It never works.**

---

## Text Needs Consistent Contrast

When placing text on background images, the problem isn't the text — it's the image. You need to reduce the dynamics in the image to make contrast consistent.

**The Problem:**
Photos have light and dark areas. White text works in dark areas but gets lost in light areas, and vice versa.

**Solution 1: Add an Overlay**
```html
<div class="relative">
  <img class="absolute inset-0 w-full h-full object-cover" />
  <div class="absolute inset-0 bg-black/40"></div>  <!-- overlay -->
  <h1 class="relative text-white">Headline</h1>
</div>
```
- Black overlay: tones down light areas, helps light text
- White overlay: brightens dark areas, helps dark text

**Solution 2: Lower Image Contrast**
Reduce the contrast of the image itself for more control. Adjust brightness to compensate (lowering contrast alone darkens mid-tones). More surgical than an overlay, which lightens or darkens everything uniformly.

**Solution 3: Colorize the Image**
1. Lower the image contrast
2. Desaturate to remove existing color
3. Add a solid fill using "multiply" blend mode

Great for making background images pair with existing brand colors.

**Solution 4: Add a Text Shadow**
For preserving more image dynamics, use text shadow with:
- **Large blur radius** (10-20px)
- **No offset**
- Looks like a subtle glow, not an actual shadow

Combine with a lighter contrast reduction for best results.

---

## Everything Has an Intended Size

Even vector images have an intended size. Scaling beyond that degrades design quality.

**Don't Scale Up Icons:**
Icons drawn at 16-24px look chunky and unprofessional at 3-4x their intended size. They lack the detail needed for larger rendering.

**Workaround:** Enclose small icons in a shape:
```html
<div class="size-12 bg-blue-100 rounded-full flex items-center justify-center">
  <Icon class="size-5 text-blue-600" />
</div>
```
Icon stays near intended size while filling larger space.

**Don't Scale Down Screenshots:**
A full-size screenshot shrunk by 70% crams too much detail (16px font → 4px). Better approaches:
1. Take the screenshot at a **smaller screen size** (tablet layout)
2. Take a **partial screenshot** (just the relevant section)
3. Draw a **simplified version** with details removed and small text replaced with simple lines

**Don't Scale Down Icons Either:**
128px icons shrunk to favicon size look choppy and fuzzy. **Redraw a simplified version** at the target size so you control the compromises.

---

## Beware User-Uploaded Content

You can't control user image quality. Protect your layout.

**Control Shape and Size:**
Displaying user images at intrinsic aspect ratios throws off layouts, especially with many images.

**Solution:** Center images in fixed containers, cropping what doesn't fit:
```html
<img class="aspect-square object-cover rounded-lg" />
```

**Prevent Background Bleed:**
When a user provides an image with a background color similar to your UI background, the image loses its shape.

**Solutions (in preference order):**

1. **Subtle inner box shadow** — most people won't notice:
```html
<div class="relative">
  <img class="rounded-lg" />
  <div class="absolute inset-0 rounded-lg shadow-[inset_0_0_0_1px_rgba(0,0,0,0.05)]"></div>
</div>
```

2. **Semi-transparent inner border** — if you don't like the inset look:
```html
<img class="ring-1 ring-black/5 rounded-lg" />
```

**Avoid regular borders** — they clash with image colors.
