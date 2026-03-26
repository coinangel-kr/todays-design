# Today's Design — Workflow Guide

## Quick Start (3 steps)

```
1. /todays-design          → See today's award-winning design
2. /design-init            → Create DESIGN.md based on it
3. /design-apply           → Generate styled code
```

---

## Workflow A: Start a New Project with Today's Design

### Step 1: Get Inspired
```
> /todays-design
```
This fetches today's Awwwards Site of the Day, analyzes its colors, typography, layout, and shows you a structured breakdown.

### Step 2: Initialize Your Design System
```
> /design-init
```
Choose **"Today's Design"** when prompted. This creates a `DESIGN.md` in your project root, pre-filled with design tokens extracted from the award-winning site.

### Step 3: Review and Customize
Open `DESIGN.md` and tweak anything:
- Change the primary color to match your brand
- Swap fonts to your preferred choices
- Adjust spacing or component styles

Or use:
```
> /design-system
> "Change primary to #8B5CF6 and heading font to Poppins"
```

### Step 4: Generate Styled Code
```
> /design-apply
> "Create a hero section and feature cards grid"
```
This generates production-ready code using your DESIGN.md tokens, styled consistently.

---

## Workflow B: Add Design System to an Existing Project

### Step 1: Extract Current Design
```
> /design-init
```
Choose **"Existing Code"** when prompted. The skill scans your project for:
- Tailwind config values
- CSS custom properties
- Theme files
- Component library configs

It creates a `DESIGN.md` that reflects your current design.

### Step 2: Enhance with Today's Reference
```
> /todays-design
```
See what's winning awards today. Then:
```
> /design-system
> "Update the Today's Reference section with this design"
```

### Step 3: Apply to New Components
```
> /design-apply
> "Build a new pricing page using our design system"
```

---

## Workflow C: Use a Specific Reference Site

### Step 1: Initialize from URL
```
> /design-init
```
Choose **"Custom URL"** and provide the reference:
```
> https://stripe.com
```

The skill analyzes the site and creates a DESIGN.md based on its design tokens.

### Step 2: Generate Code
```
> /design-apply
> "Create a landing page inspired by this design"
```

---

## Workflow D: Daily Design Refresh

Every day, check what's new in the design world:

```
> /todays-design
```

If you like what you see:
```
> /design-system
> "Update our design with today's color approach"
```

Or:
```
> /design-system
> "Adopt the typography pairing from today's reference"
```

---

## Tips

### Combining with Other Skills
`/design-apply` works best when combined with:
- **`frontend-design`** — High-quality UI code generation
- **`vercel-react-best-practices`** — React/Next.js performance
- **`web-design-guidelines`** — Accessibility compliance

### DESIGN.md as Source of Truth
- Keep `DESIGN.md` in your project root
- Commit it to version control
- All team members (and AI agents) reference the same file
- Update it as your design evolves

### Caching
- Today's design is cached in `.todays-design/cache/YYYY-MM-DD.md`
- Same-day requests use the cache (no re-fetching)
- Add `.todays-design/cache/` to `.gitignore` (already done by default)

### Framework Support
Works with any frontend framework:
- **Next.js / React** → Tailwind classes or CSS-in-JS
- **Vue / Nuxt** → Scoped styles or Tailwind
- **Svelte** → Scoped CSS or Tailwind
- **React Native / Expo** → StyleSheet or styled-components
- **Plain HTML/CSS** → CSS custom properties
