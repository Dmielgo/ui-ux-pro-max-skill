# Tailwind v3 → v4 Migration Guide

## Quick Reference

### Config → CSS

**Before (v3):**
```javascript
// tailwind.config.js
module.exports = {
  content: ['./src/**/*.{html,js}'],
  theme: {
    extend: {
      colors: {
        brand: { 500: '#3b82f6' },
      },
      fontFamily: {
        display: ['Playfair Display', 'serif'],
      },
    },
  },
  plugins: [require('@tailwindcss/typography')],
}
```

**After (v4):**
```css
/* styles.css */
@import "tailwindcss";
@plugin "@tailwindcss/typography";

@theme {
  --color-brand-500: oklch(0.55 0.22 264);
  --font-display: "Playfair Display", serif;
}
```

### CSS Directives

| v3 | v4 |
|----|-----|
| `@tailwind base;` | `@import "tailwindcss";` |
| `@tailwind components;` | (included in import) |
| `@tailwind utilities;` | (included in import) |

### Plugins

| v3 | v4 |
|----|-----|
| `require('@tailwindcss/typography')` in config | `@plugin "@tailwindcss/typography";` in CSS |
| `require('@tailwindcss/forms')` in config | `@plugin "@tailwindcss/forms";` in CSS |

### Custom Utilities

**Before (v3):**
```javascript
plugin(function({ addUtilities }) {
  addUtilities({
    '.glass': {
      background: 'rgba(255,255,255,0.1)',
      backdropFilter: 'blur(10px)',
    },
  })
})
```

**After (v4):**
```css
@utility glass {
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
}
```

### Color Format

v4 recommends oklch() for perceptually uniform color scales:

```css
/* v3 style */
--color-brand-500: #3b82f6;

/* v4 style (recommended) */
--color-brand-500: oklch(0.55 0.22 264);
```

### Content Detection

v3 requires explicit `content` array. v4 detects automatically — no config needed.

### Dark Mode

**v3:** `darkMode: 'class'` in config
**v4:** `@custom-variant dark (&:where(.dark *));` in CSS (or automatic via @media)

## What Stays the Same

- All utility classes (`flex`, `grid`, `p-4`, `text-lg`, etc.)
- Breakpoint prefixes (`sm:`, `md:`, `lg:`, `xl:`, `2xl:`)
- State variants (`hover:`, `focus:`, `active:`, `group-hover:`)
- Arbitrary values (`bg-[#FF7A33]`, `w-[calc(100%-2rem)]`)
- `@apply` directive
- `@layer base/components/utilities`
