# Tailwind CSS v3 — Configuration

## Setup

### Via CDN (for CMS / quick prototyping)
```html
<script src="https://cdn.tailwindcss.com"></script>
<script>
  tailwind.config = {
    theme: {
      extend: {
        colors: {
          brand: { 500: '#3b82f6', 600: '#2563eb' },
        },
        fontFamily: {
          display: ['Playfair Display', 'serif'],
        },
      }
    }
  }
</script>
```

### Via npm
```bash
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

## tailwind.config.js

```javascript
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    './src/**/*.{html,js,jsx,ts,tsx}',
    './pages/**/*.{html,js,jsx,ts,tsx}',
    './components/**/*.{html,js,jsx,ts,tsx}',
  ],
  darkMode: 'class', // or 'media'
  theme: {
    extend: {
      colors: {
        brand: {
          50: '#eff6ff',
          100: '#dbeafe',
          500: '#3b82f6',
          600: '#2563eb',
          700: '#1d4ed8',
          900: '#1e3a8a',
        },
        // CSS variables (compatible with shadcn/ui)
        background: 'hsl(var(--background))',
        foreground: 'hsl(var(--foreground))',
        primary: {
          DEFAULT: 'hsl(var(--primary))',
          foreground: 'hsl(var(--primary-foreground))',
        },
      },
      fontFamily: {
        sans: ['Inter', 'system-ui', 'sans-serif'],
        display: ['Playfair Display', 'serif'],
        mono: ['JetBrains Mono', 'monospace'],
      },
      spacing: {
        '18': '4.5rem',
        '88': '22rem',
      },
      borderRadius: {
        lg: 'var(--radius)',
        md: 'calc(var(--radius) - 2px)',
        sm: 'calc(var(--radius) - 4px)',
      },
      keyframes: {
        'fade-in': {
          '0%': { opacity: '0' },
          '100%': { opacity: '1' },
        },
        'slide-up': {
          '0%': { transform: 'translateY(10px)', opacity: '0' },
          '100%': { transform: 'translateY(0)', opacity: '1' },
        },
      },
      animation: {
        'fade-in': 'fade-in 0.3s ease-out',
        'slide-up': 'slide-up 0.4s ease-out',
      },
    },
  },
  plugins: [
    require('@tailwindcss/typography'),
    require('@tailwindcss/forms'),
  ],
}
```

## CSS Entry Point (globals.css)

```css
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer base {
  :root {
    --background: 0 0% 100%;
    --foreground: 222 47% 11%;
    --primary: 217 91% 60%;
    --primary-foreground: 0 0% 100%;
    --radius: 0.5rem;
  }

  .dark {
    --background: 222 47% 4%;
    --foreground: 210 40% 98%;
    --primary: 217 91% 60%;
    --primary-foreground: 0 0% 100%;
  }
}
```

## Plugins (v3 syntax)

### Official plugins
```bash
npm install -D @tailwindcss/typography @tailwindcss/forms @tailwindcss/container-queries
```

```javascript
// tailwind.config.js
module.exports = {
  plugins: [
    require('@tailwindcss/typography'),
    require('@tailwindcss/forms'),
    require('@tailwindcss/container-queries'),
  ],
}
```

### Custom plugin
```javascript
const plugin = require('tailwindcss/plugin')

module.exports = {
  plugins: [
    plugin(function({ addUtilities, addComponents, theme }) {
      addUtilities({
        '.text-shadow': { textShadow: '2px 2px 4px rgba(0,0,0,0.1)' },
        '.text-shadow-lg': { textShadow: '4px 4px 8px rgba(0,0,0,0.2)' },
      })
    }),
  ],
}
```

## Dark Mode

```javascript
// tailwind.config.js
module.exports = {
  darkMode: 'class', // toggle via class on <html>
}
```

```html
<html class="dark">
  <div class="bg-white dark:bg-gray-900 text-gray-900 dark:text-white">
    Responds to .dark class
  </div>
</html>
```

## Safelist (preserve dynamic classes)

```javascript
module.exports = {
  safelist: [
    'bg-red-500',
    'bg-green-500',
    { pattern: /bg-(red|green|blue)-(100|500|900)/ },
  ],
}
```

## @layer and @apply (v3)

```css
@layer base {
  h1 { @apply text-4xl font-bold tracking-tight; }
  a { @apply text-blue-600 hover:text-blue-700; }
}

@layer components {
  .btn { @apply px-4 py-2 rounded-lg font-medium transition-colors; }
  .btn-primary { @apply bg-blue-600 text-white hover:bg-blue-700; }
  .card { @apply bg-white rounded-xl shadow-md p-6; }
}

@layer utilities {
  .text-balance { text-wrap: balance; }
}
```
