# Design Apply — Framework-Specific Patterns

## Tailwind CSS Projects

### Setup: Extend tailwind.config with DESIGN.md tokens

```js
// tailwind.config.js
const designTokens = {
  colors: {
    primary: { DEFAULT: '#3B82F6', light: '#60A5FA', dark: '#2563EB' },
    secondary: '#8B5CF6',
    accent: '#F59E0B',
    background: '#FFFFFF',
    surface: '#F8FAFC',
    'text-primary': '#0F172A',
    'text-secondary': '#64748B',
    border: '#E2E8F0',
    success: '#22C55E',
    warning: '#F59E0B',
    error: '#EF4444',
    info: '#3B82F6',
  },
  fontFamily: {
    heading: ['Inter', 'sans-serif'],
    body: ['Inter', 'sans-serif'],
  },
  borderRadius: {
    sm: '4px',
    md: '8px',
    lg: '16px',
    xl: '24px',
  },
};

module.exports = {
  theme: { extend: designTokens },
};
```

### Component Pattern

```tsx
export function HeroSection() {
  return (
    <section className="bg-background min-h-[80vh] flex items-center">
      <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <h1 className="font-heading text-4xl sm:text-5xl lg:text-6xl font-bold text-text-primary">
          Your Headline Here
        </h1>
        <p className="mt-6 text-lg text-text-secondary max-w-2xl">
          Supporting text that describes the value proposition.
        </p>
        <div className="mt-8 flex gap-4">
          <button className="bg-primary hover:bg-primary-dark text-white font-medium rounded-lg px-8 py-3 transition-colors duration-200">
            Primary CTA
          </button>
          <button className="border border-primary text-primary hover:bg-primary/10 font-medium rounded-lg px-8 py-3 transition-colors duration-200">
            Secondary CTA
          </button>
        </div>
      </div>
    </section>
  );
}
```

---

## shadcn/ui Projects

### Setup: Update CSS variables in globals.css

```css
@layer base {
  :root {
    /* Map from DESIGN.md */
    --background: 0 0% 100%;           /* #FFFFFF */
    --foreground: 222.2 84% 4.9%;      /* #0F172A */
    --primary: 217.2 91.2% 59.8%;      /* #3B82F6 */
    --primary-foreground: 210 40% 98%; /* white text on primary */
    --secondary: 210 40% 96.1%;
    --muted: 210 40% 96.1%;
    --accent: 210 40% 96.1%;
    --border: 214.3 31.8% 91.4%;       /* #E2E8F0 */
    --radius: 0.5rem;                   /* 8px */
  }

  .dark {
    --background: 222.2 84% 4.9%;
    --foreground: 210 40% 98%;
    /* ... dark mode values from DESIGN.md */
  }
}
```

---

## CSS-in-JS Projects (styled-components / emotion)

### Setup: Create theme from DESIGN.md

```ts
// src/styles/theme.ts
export const theme = {
  colors: {
    primary: '#3B82F6',
    primaryLight: '#60A5FA',
    primaryDark: '#2563EB',
    background: '#FFFFFF',
    surface: '#F8FAFC',
    textPrimary: '#0F172A',
    textSecondary: '#64748B',
    border: '#E2E8F0',
  },
  fonts: {
    heading: "'Inter', sans-serif",
    body: "'Inter', sans-serif",
  },
  fontSizes: {
    xs: '0.64rem',
    sm: '0.8rem',
    base: '1rem',
    lg: '1.25rem',
    xl: '1.563rem',
    '2xl': '1.953rem',
    '3xl': '2.441rem',
  },
  spacing: {
    xs: '4px', sm: '8px', md: '16px', lg: '24px', xl: '32px', '2xl': '48px',
  },
  radii: {
    sm: '4px', md: '8px', lg: '16px', full: '9999px',
  },
  shadows: {
    sm: '0 1px 2px rgba(0,0,0,0.05)',
    md: '0 4px 6px -1px rgba(0,0,0,0.1)',
    lg: '0 10px 15px -3px rgba(0,0,0,0.1)',
  },
  transitions: {
    fast: '150ms ease',
    normal: '200ms ease',
    slow: '300ms ease',
  },
} as const;

export type Theme = typeof theme;
```

---

## Plain CSS / SCSS Projects

### Setup: CSS Custom Properties from DESIGN.md

```css
:root {
  /* Colors */
  --color-primary: #3B82F6;
  --color-primary-light: #60A5FA;
  --color-primary-dark: #2563EB;
  --color-bg: #FFFFFF;
  --color-surface: #F8FAFC;
  --color-text: #0F172A;
  --color-text-muted: #64748B;
  --color-border: #E2E8F0;

  /* Typography */
  --font-heading: 'Inter', sans-serif;
  --font-body: 'Inter', sans-serif;
  --font-size-base: 16px;
  --line-height: 1.5;

  /* Spacing */
  --space-unit: 4px;
  --space-xs: 4px;
  --space-sm: 8px;
  --space-md: 16px;
  --space-lg: 24px;
  --space-xl: 32px;

  /* Components */
  --radius-sm: 4px;
  --radius-md: 8px;
  --radius-lg: 16px;
  --shadow-sm: 0 1px 2px rgba(0,0,0,0.05);
  --shadow-md: 0 4px 6px -1px rgba(0,0,0,0.1);
  --transition: 200ms cubic-bezier(0.4, 0, 0.2, 1);

  /* Layout */
  --max-width: 1280px;
  --content-width: 768px;
}
```

---

## React Native / Expo Projects

### Setup: Theme constants from DESIGN.md

```ts
// src/theme/index.ts
export const colors = {
  primary: '#007AFF',
  primaryLight: '#4DA3FF',
  background: '#FFFFFF',
  surface: '#F2F2F7',
  text: '#000000',
  textSecondary: '#8E8E93',
  separator: '#C6C6C8',
  success: '#34C759',
  warning: '#FF9500',
  error: '#FF3B30',
} as const;

export const spacing = {
  xs: 4, sm: 8, md: 16, lg: 24, xl: 32, '2xl': 48,
} as const;

export const typography = {
  largeTitle: { fontSize: 34, fontWeight: '700' as const },
  title1: { fontSize: 28, fontWeight: '700' as const },
  title2: { fontSize: 22, fontWeight: '700' as const },
  headline: { fontSize: 17, fontWeight: '600' as const },
  body: { fontSize: 17, fontWeight: '400' as const },
  caption: { fontSize: 12, fontWeight: '400' as const },
} as const;

export const radii = {
  sm: 4, md: 8, lg: 16, xl: 24,
} as const;
```
