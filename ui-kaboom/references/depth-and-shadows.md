# Depth and Shadows

Detailed guidance on making elements feel raised, inset, or layered.

---

## Emulate a Light Source

To create the illusion of depth, mimic how light affects things in the real world. Light comes from above.

**How Light Creates Depth:**
- **Top edges** facing upward → lighter (receive more light)
- **Bottom edges** facing downward → darker (receive less light)
- **Below elements** → cast shadow

**Raised Elements (Buttons):**
1. People look slightly downward at screens — reveal a bit of top edge, hide bottom
2. Make the top edge lighter using a top border or inset box shadow with slight vertical offset
3. Choose the lighter color by hand (not semi-transparent white, which can suck saturation out)
4. Add a small dark box shadow with slight vertical offset below
5. Keep blur radius small (1-4px) — real shadows have sharp edges

```html
<button class="bg-blue-500 shadow-md border-t border-blue-400">
  Button
</button>
```

**Inset Elements (Inputs, Wells):**
1. Only the bottom lip is visible when looking downward
2. Give bottom edge a slightly lighter color
3. Add a small dark inset box shadow at the top

```html
<input class="shadow-inner border-b border-white" />
```

**Don't Get Carried Away:**
Borrow real-world cues for depth, but don't try for photo-realism. It leads to busy, unclear interfaces.

---

## Use Shadows to Convey Elevation

Shadows position elements on a virtual z-axis. Closer elements attract more focus.

**Shadow Size = Elevation:**
- **Small shadows** (tight blur): slightly raised → buttons
- **Medium shadows**: further from surface → dropdowns
- **Large shadows** (big blur): much closer to user → modals

**Establish an Elevation System:**
Define a fixed set (five options is usually plenty):
1. Define smallest and largest shadow
2. Fill middle with linear size increases

**Tailwind elevation system:**
```
shadow-sm  — buttons at rest, subtle lift
shadow     — cards, default elevation
shadow-md  — dropdowns, popovers
shadow-lg  — hover cards, sticky headers
shadow-xl  — modals, dialogs
shadow-2xl — full-screen overlays
```

**Interactive Shadows:**
```html
<!-- Lift on drag -->
<div class="shadow-sm active:shadow-lg cursor-grab">Drag me</div>

<!-- Press on click -->
<button class="shadow-md active:shadow-sm">Click</button>
```

**Key Takeaway:** Don't think about the shadow itself — think about where the element sits on the z-axis and assign the corresponding shadow.

---

## Shadows Can Have Two Parts

The best shadows combine two separate shadows, each doing a specific job.

**First Shadow — Direct Light:**
- Larger and softer
- Considerable vertical offset
- Large blur radius
- Simulates shadow cast by direct light source

**Second Shadow — Ambient Light:**
- Tighter and darker
- Less vertical offset
- Smaller blur radius
- Simulates where even ambient light can't reach

**Why Two Shadows:**
Much more control than a single shadow. Keep the larger shadow subtle while making the edge shadow well-defined.

**Accounting for Elevation:**
As an object moves further from a surface, the ambient (tight, dark) shadow fades:
- **Low elevation:** Ambient shadow quite distinct
- **High elevation:** Ambient shadow almost or completely invisible

---

## Even Flat Designs Can Have Depth

The most effective flat designs still convey depth — just without shadows, gradients, or light-mimicking effects.

**Depth with Color:**
- **Lighter than background** → feels raised
- **Darker than background** → feels inset

```html
<!-- Raised card (lighter than background) -->
<body class="bg-slate-100">
  <div class="bg-white">Card</div>
</body>

<!-- Inset well (darker than background) -->
<div class="bg-slate-200">Well</div>
```

**Solid Shadows:**
Short, vertically offset shadows with **no blur radius**:
```html
<div class="shadow-[0_4px_0_0_theme(colors.slate.300)]">Card</div>
```

Great for making cards or buttons stand off the page while maintaining a flat aesthetic.

---

## Overlap Elements to Create Layers

One of the most effective ways to create depth — overlap different elements to create multiple visual layers.

**Techniques:**
- Offset a card across a background color transition
- Make an element taller than its parent so it overlaps both sides
- Overlap controls on smaller components (carousel arrows)

```html
<section class="bg-slate-800 pb-16">Hero</section>
<div class="-mt-12 bg-white rounded-lg shadow-lg">Card overlaps hero</div>
```

**Overlapping Images:**
Without care, overlapping images clash. Use an "invisible border" that matches the background color:

```html
<div class="flex -space-x-3">
  <img class="ring-2 ring-white rounded-full" />
  <img class="ring-2 ring-white rounded-full" />
</div>
```

Creates the appearance of layers without the ugly clashing.
