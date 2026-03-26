# DESIGN.md Template Reference

## Template Selection Guide

All platforms use a single `DESIGN.md` template. Platform-specific sections are marked with HTML comments (`<!-- FOR MOBILE APP -->`). When generating:

| Framework Detected | Platform Sections to Activate | Focus |
|---|---|---|
| Next.js, React, Vue, Svelte, Angular | Web sections (breakpoints, scroll, accessibility) | Responsive, web accessibility, scroll behaviors |
| React Native, Expo, Flutter | Mobile comment blocks (safe areas, gestures, haptics, tab bar) | Safe areas, gestures, haptics, platform-specific tokens |
| None / Mixed / Unclear | Both web and mobile sections | Universal patterns |

## Framework-Specific Mapping Tips

### Tailwind CSS
DESIGN.md tokens map to `tailwind.config.js`:
```js
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
        primary: 'var(--primary)',        // from DESIGN.md Colors
        'primary-light': 'var(--primary-light)',
      },
      fontFamily: {
        heading: ['var(--font-heading)'], // from DESIGN.md Typography
        body: ['var(--font-body)'],
      },
      spacing: {
        // from DESIGN.md Spacing scale
      },
      borderRadius: {
        // from DESIGN.md Components > Border Radius
      },
    },
  },
}
```

### CSS Custom Properties
```css
:root {
  /* Colors - from DESIGN.md */
  --primary: #3B82F6;
  --primary-light: #60A5FA;
  --primary-dark: #2563EB;

  /* Typography */
  --font-heading: 'Inter', sans-serif;
  --font-body: 'Inter', sans-serif;
  --font-size-base: 16px;

  /* Spacing */
  --space-unit: 4px;

  /* Components */
  --radius-sm: 4px;
  --radius-md: 8px;
  --radius-lg: 16px;
}
```

### CSS-in-JS (styled-components, emotion)
```ts
// theme.ts - generated from DESIGN.md
export const theme = {
  colors: {
    primary: '#3B82F6',
    primaryLight: '#60A5FA',
    primaryDark: '#2563EB',
  },
  fonts: {
    heading: "'Inter', sans-serif",
    body: "'Inter', sans-serif",
  },
  spacing: (n: number) => `${n * 4}px`,
  radii: { sm: '4px', md: '8px', lg: '16px' },
}
```

### React Native / Expo
```ts
// theme.ts - mobile tokens from DESIGN.md
export const theme = {
  colors: {
    primary: '#007AFF',
    background: '#FFFFFF',
    surface: '#F2F2F7',
    text: '#000000',
  },
  typography: {
    largeTitle: { fontSize: 34, fontWeight: '700' },
    title1: { fontSize: 28, fontWeight: '700' },
    body: { fontSize: 17, fontWeight: '400' },
  },
  spacing: { xs: 4, sm: 8, md: 16, lg: 24, xl: 32 },
}
```

## Color Extraction Methods

When analyzing a reference site:

1. **Meta tags**: `<meta name="theme-color" content="#...">`
2. **CSS variables**: `:root { --primary: #... }`
3. **Inline styles**: Look for repeated color values
4. **SVG fills**: Logo and icon colors often reveal brand colors
5. **Background colors**: Hero sections, CTAs, headers
6. **Text colors**: Body text, headings (reveals neutral palette)

## Font Detection Methods

1. **Google Fonts link**: `<link href="fonts.googleapis.com/css2?family=...">`
2. **CSS font-family**: First declared non-generic font
3. **@font-face declarations**: Custom font files
4. **Adobe Fonts**: `use.typekit.net` links
