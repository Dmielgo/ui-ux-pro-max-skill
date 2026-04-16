# Tailwind CSS v3 — CDN Usage

For CMS-based projects (Acai CMS, WordPress, etc.) where npm is not available.

## Basic Setup

```html
<script src="https://cdn.tailwindcss.com"></script>
```

## With Custom Config

```html
<script src="https://cdn.tailwindcss.com"></script>
<script>
  tailwind.config = {
    theme: {
      extend: {
        colors: {
          'main-color': 'var(--main-color)',
          'main-color-light': 'var(--main-color-light)',
          'main-color-dark': 'var(--main-color-dark)',
          brand: {
            50: '#eff6ff',
            500: '#3b82f6',
            900: '#1e3a8a',
          },
        },
        fontFamily: {
          display: ['Playfair Display', 'serif'],
          body: ['Inter', 'system-ui', 'sans-serif'],
        },
      }
    }
  }
</script>
```

## With Plugins via CDN

```html
<script src="https://cdn.tailwindcss.com"></script>
<script src="https://cdn.tailwindcss.com/3.4.0?plugins=typography,forms"></script>
```

## Custom CSS with CDN

Use a `<style type="text/tailwindcss">` block:

```html
<style type="text/tailwindcss">
  @layer base {
    h1 { @apply text-4xl font-bold; }
  }

  @layer components {
    .btn { @apply px-4 py-2 rounded-lg font-medium transition-colors; }
    .btn-primary { @apply bg-blue-600 text-white hover:bg-blue-700; }
  }
</style>
```

## Limitations

- Not for production (larger file size, no purging)
- No PostCSS plugins
- Config limited to what the CDN supports
- Good for: prototyping, CMS templates, admin panels, quick demos

## Arbitrary Values (work with CDN)

```html
<div class="bg-[#FF7A33]">Custom hex color</div>
<div class="w-[calc(100%-2rem)]">Custom calc</div>
<div class="grid-cols-[1fr_2fr]">Custom grid</div>
<div class="text-[clamp(1rem,3vw,2rem)]">Responsive text</div>
```
