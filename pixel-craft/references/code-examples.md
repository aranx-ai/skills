# Code Examples

Detailed Tailwind 4 examples for common patterns.

## Cards

### Basic Card with Hierarchy
```html
<div class="bg-white rounded-lg shadow-md p-6 max-w-sm">
  <span class="text-xs font-medium text-blue-600 uppercase tracking-wide">Featured</span>
  <h3 class="mt-2 text-lg font-semibold text-slate-900">Card Title</h3>
  <p class="mt-1 text-sm text-slate-500">Supporting text that explains more about this card.</p>
  <div class="mt-4 flex items-center gap-4">
    <button class="bg-blue-600 text-white text-sm font-medium px-4 py-2 rounded-lg">
      Primary
    </button>
    <button class="text-slate-600 text-sm font-medium">
      Secondary
    </button>
  </div>
</div>
```

### Card with Accent Border
```html
<div class="bg-white rounded-lg shadow-sm border-t-4 border-indigo-500 p-6">
  <h3 class="font-semibold text-slate-900">Plan Features</h3>
  <ul class="mt-4 space-y-3">
    <li class="flex items-center gap-3">
      <svg class="size-5 text-green-500">...</svg>
      <span class="text-slate-700">Unlimited projects</span>
    </li>
    <!-- more items -->
  </ul>
</div>
```

## Forms

### Form with Grouped Spacing
```html
<form class="space-y-6">
  <!-- Group 1 -->
  <div class="space-y-1">
    <label class="block text-sm font-medium text-slate-700">Email</label>
    <input type="email" class="w-full px-3 py-2 border border-slate-300 rounded-lg 
                                shadow-sm focus:ring-2 focus:ring-blue-500 focus:border-blue-500" />
  </div>
  
  <!-- Group 2 -->
  <div class="space-y-1">
    <label class="block text-sm font-medium text-slate-700">Password</label>
    <input type="password" class="w-full px-3 py-2 border border-slate-300 rounded-lg 
                                   shadow-sm focus:ring-2 focus:ring-blue-500 focus:border-blue-500" />
  </div>
  
  <button type="submit" class="w-full bg-blue-600 text-white font-medium py-2 px-4 rounded-lg 
                                hover:bg-blue-700 focus:ring-2 focus:ring-blue-500 focus:ring-offset-2">
    Sign in
  </button>
</form>
```

### Radio Cards
```html
<fieldset class="grid grid-cols-3 gap-4">
  <label class="relative flex cursor-pointer rounded-lg border border-slate-200 p-4 
                shadow-sm hover:border-blue-500 has-[:checked]:border-blue-600 has-[:checked]:ring-2 has-[:checked]:ring-blue-600">
    <input type="radio" name="plan" value="basic" class="sr-only" />
    <div class="flex flex-col">
      <span class="text-sm font-medium text-slate-900">Basic</span>
      <span class="mt-1 text-2xl font-semibold">$9</span>
      <span class="text-sm text-slate-500">/month</span>
    </div>
  </label>
  <!-- more options -->
</fieldset>
```

## Navigation

### Nav with Active State
```html
<nav class="flex gap-1">
  <a href="#" class="px-4 py-2 text-sm font-medium text-slate-900 bg-slate-100 rounded-lg">
    Dashboard
  </a>
  <a href="#" class="px-4 py-2 text-sm font-medium text-slate-500 hover:text-slate-900 hover:bg-slate-50 rounded-lg">
    Projects
  </a>
  <a href="#" class="px-4 py-2 text-sm font-medium text-slate-500 hover:text-slate-900 hover:bg-slate-50 rounded-lg">
    Settings
  </a>
</nav>
```

### Sidebar Navigation
```html
<aside class="w-64 shrink-0 border-r border-slate-200 p-4">
  <nav class="space-y-1">
    <a href="#" class="flex items-center gap-3 px-3 py-2 text-sm font-medium text-slate-900 bg-slate-100 rounded-lg">
      <svg class="size-5 text-slate-500">...</svg>
      Dashboard
    </a>
    <a href="#" class="flex items-center gap-3 px-3 py-2 text-sm font-medium text-slate-600 hover:bg-slate-50 rounded-lg">
      <svg class="size-5 text-slate-400">...</svg>
      Projects
    </a>
  </nav>
</aside>
```

## Data Display

### Stats with Icon
```html
<div class="bg-white rounded-lg shadow-sm p-6">
  <div class="flex items-center gap-4">
    <div class="size-12 bg-green-100 rounded-full flex items-center justify-center">
      <svg class="size-6 text-green-600">...</svg>
    </div>
    <div>
      <p class="text-sm font-medium text-slate-500">Total Revenue</p>
      <p class="text-2xl font-semibold text-slate-900">$45,231</p>
    </div>
  </div>
  <div class="mt-4 flex items-center gap-1 text-sm">
    <svg class="size-4 text-green-500">...</svg>
    <span class="text-green-600 font-medium">12%</span>
    <span class="text-slate-500">vs last month</span>
  </div>
</div>
```

### Table with Combined Columns
```html
<table class="w-full">
  <thead>
    <tr class="border-b border-slate-200">
      <th class="py-3 text-left text-xs font-medium text-slate-500 uppercase tracking-wide">User</th>
      <th class="py-3 text-left text-xs font-medium text-slate-500 uppercase tracking-wide">Status</th>
      <th class="py-3 text-right text-xs font-medium text-slate-500 uppercase tracking-wide">Amount</th>
    </tr>
  </thead>
  <tbody class="divide-y divide-slate-100">
    <tr>
      <td class="py-4">
        <div class="flex items-center gap-3">
          <img class="size-10 rounded-full" src="..." />
          <div>
            <p class="font-medium text-slate-900">Jane Cooper</p>
            <p class="text-sm text-slate-500">jane@example.com</p>
          </div>
        </div>
      </td>
      <td class="py-4">
        <span class="inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-medium bg-green-100 text-green-800">
          Active
        </span>
      </td>
      <td class="py-4 text-right font-medium text-slate-900">$2,500.00</td>
    </tr>
  </tbody>
</table>
```

## Alerts & Feedback

### Alert with Icon
```html
<div class="flex gap-3 p-4 bg-amber-50 border-l-4 border-amber-500 rounded-r-lg">
  <svg class="size-5 text-amber-500 shrink-0">...</svg>
  <div>
    <p class="font-medium text-amber-800">Attention needed</p>
    <p class="mt-1 text-sm text-amber-700">Your trial expires in 3 days. Upgrade to continue using all features.</p>
  </div>
</div>
```

### Empty State
```html
<div class="text-center py-12">
  <svg class="mx-auto size-12 text-slate-400">...</svg>
  <h3 class="mt-4 text-lg font-medium text-slate-900">No projects yet</h3>
  <p class="mt-2 text-sm text-slate-500">Get started by creating your first project.</p>
  <button class="mt-6 bg-blue-600 text-white font-medium px-4 py-2 rounded-lg hover:bg-blue-700">
    + New Project
  </button>
</div>
```

## Modals & Overlays

### Modal Dialog
```html
<!-- Backdrop -->
<div class="fixed inset-0 bg-black/50 flex items-center justify-center p-4">
  <!-- Dialog -->
  <div class="bg-white rounded-xl shadow-2xl max-w-md w-full p-6">
    <h2 class="text-lg font-semibold text-slate-900">Delete project?</h2>
    <p class="mt-2 text-sm text-slate-500">
      This action cannot be undone. All data will be permanently removed.
    </p>
    <div class="mt-6 flex justify-end gap-3">
      <button class="px-4 py-2 text-sm font-medium text-slate-700 hover:bg-slate-100 rounded-lg">
        Cancel
      </button>
      <button class="px-4 py-2 text-sm font-medium text-white bg-red-600 hover:bg-red-700 rounded-lg">
        Delete
      </button>
    </div>
  </div>
</div>
```

### Dropdown Menu
```html
<div class="relative inline-block">
  <button class="flex items-center gap-2 px-4 py-2 text-sm font-medium text-slate-700 
                 bg-white border border-slate-300 rounded-lg hover:bg-slate-50">
    Options
    <svg class="size-4">...</svg>
  </button>
  
  <div class="absolute right-0 mt-2 w-56 bg-white rounded-lg shadow-lg border border-slate-200 py-1">
    <a href="#" class="flex items-center gap-3 px-4 py-2 text-sm text-slate-700 hover:bg-slate-50">
      <svg class="size-4 text-slate-400">...</svg>
      Edit
    </a>
    <a href="#" class="flex items-center gap-3 px-4 py-2 text-sm text-slate-700 hover:bg-slate-50">
      <svg class="size-4 text-slate-400">...</svg>
      Duplicate
    </a>
    <hr class="my-1 border-slate-200" />
    <a href="#" class="flex items-center gap-3 px-4 py-2 text-sm text-red-600 hover:bg-red-50">
      <svg class="size-4">...</svg>
      Delete
    </a>
  </div>
</div>
```

## Hero Sections

### Hero with Gradient Background
```html
<section class="relative bg-gradient-to-br from-blue-600 to-indigo-700 py-24">
  <div class="max-w-4xl mx-auto px-4 text-center">
    <h1 class="text-4xl font-bold text-white sm:text-5xl">
      Build something amazing
    </h1>
    <p class="mt-6 text-xl text-blue-100 max-w-2xl mx-auto">
      The fastest way to turn your ideas into reality with our powerful platform.
    </p>
    <div class="mt-10 flex justify-center gap-4">
      <a href="#" class="bg-white text-blue-600 font-semibold px-6 py-3 rounded-lg hover:bg-blue-50">
        Get started
      </a>
      <a href="#" class="text-white font-semibold px-6 py-3 rounded-lg border border-white/30 hover:bg-white/10">
        Learn more
      </a>
    </div>
  </div>
</section>
```

### Hero with Overlapping Card
```html
<section class="bg-slate-900 pt-24 pb-32">
  <div class="max-w-4xl mx-auto px-4 text-center">
    <h1 class="text-4xl font-bold text-white">Dashboard</h1>
    <p class="mt-4 text-slate-400">Track your metrics in real-time</p>
  </div>
</section>

<div class="-mt-16 max-w-6xl mx-auto px-4">
  <div class="bg-white rounded-xl shadow-xl p-6">
    <!-- Dashboard content overlaps hero -->
  </div>
</div>
```
