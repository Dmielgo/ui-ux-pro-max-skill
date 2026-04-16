# Tailwind CSS v4 — Configuration

## Setup

### Vite projects
```bash
npm install -D tailwindcss @tailwindcss/vite
```

```javascript
// vite.config.ts
import tailwindcss from '@tailwindcss/vite'
export default { plugins: [tailwindcss()] }
```

### PostCSS projects
```bash
npm install -D tailwindcss @tailwindcss/postcss
```

```javascript
// postcss.config.js
export default { plugins: { '@tailwindcss/postcss': {} } }
```

## CSS Entry Point (the ONLY config file)

No `tailwind.config.js` needed. Everything in CSS:

```css
@import "tailwindcss";

@theme {
  /* Colors (oklch for perceptual uniformity) */
  --color-brand-50: oklch(0.97 0.02 264);
  --color-brand-500: oklch(0.55 0.22 264);
  --color-brand-900: oklch(0.25 0.15 264);

  /* Semantic colors */
  --color-primary: oklch(0.55 0.22 264);
  --color-success: oklch(0.65 0.18 145);
  --color-warning: oklch(0.75 0.15 85);
  --color-error: oklch(0.60 0.22 25);

  /* Fonts */
  --font-display: "Satoshi", "Inter", sans-serif;
  --font-body: "Inter", system-ui, sans-serif;
  --font-mono: "JetBrains Mono", monospace;

  /* Spacing */
  --spacing-18: calc(var(--spacing) * 18);
  --spacing-section: 6rem;

  /* Breakpoints */
  --breakpoint-3xl: 120rem;

  /* Shadows */
  --shadow-glow: 0 0 20px rgba(139, 92, 246, 0.3);

  /* Radius */
  --radius-large: 1.5rem;
}
```

Usage:
```html
<div class="bg-brand-500 font-display shadow-glow rounded-large">
  All custom tokens as utility classes
</div>
```

## @theme Directive (replaces tailwind.config.js)

### Color palette
```css
@theme {
  --color-primary-50: oklch(0.98 0.02 250);
  --color-primary-100: oklch(0.95 0.05 250);
  --color-primary-500: oklch(0.65 0.22 250);
  --color-primary-900: oklch(0.25 0.15 250);
}
```

### Custom fonts
```css
@theme {
  --font-sans: "Inter", system-ui, sans-serif;
  --font-serif: "Merriweather", Georgia, serif;
  --font-display: "Playfair Display", serif;
}
```

### Custom font sizes
```css
@theme {
  --font-size-jumbo: 4rem;
  --font-size-hero: 5rem;
}
```

## @utility (replaces addUtilities plugin)

```css
@utility content-auto {
  content-visibility: auto;
}

@utility glass {
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.2);
}

@utility text-shadow {
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
}
```

Usage:
```html
<div class="glass">Glassmorphism via utility</div>
```

## @custom-variant (replaces variant plugins)

```css
@custom-variant theme-midnight (&:where([data-theme="midnight"] *));
@custom-variant aria-checked (&[aria-checked="true"]);
```

Usage:
```html
<div class="theme-midnight:bg-navy-900">Midnight theme style</div>
```

## @plugin (replaces require() in config)

```css
@plugin "@tailwindcss/typography";
@plugin "@tailwindcss/forms";
```

## Dark Mode (v4)

```css
/* Automatic via @media (default) */
<div class="dark:bg-gray-900">Responds to OS preference</div>

/* Class-based (opt-in) */
@custom-variant dark (&:where(.dark *));
```

## Key Differences from v3

| v3 | v4 |
|----|-----|
| `tailwind.config.js` | `@theme {}` in CSS |
| `@tailwind base/components/utilities` | `@import "tailwindcss"` |
| `require('@tailwindcss/...')` | `@plugin "@tailwindcss/..."` |
| `addUtilities()` in plugin | `@utility name { ... }` |
| `addVariant()` in plugin | `@custom-variant name (selector)` |
| `content: [...]` | Automatic detection |
| Colors in hex/hsl | Colors in oklch() (recommended) |
| `darkMode: 'class'` | `@custom-variant dark (...)` |
