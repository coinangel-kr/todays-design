---
name: design-apply
description: "Apply design system to generate styled frontend code. Use when user asks to 'apply design', 'design apply', 'use today's design', 'style this', 'make it look like', 'apply DESIGN.md', or mentions wanting to generate styled components. Also trigger on Korean: '디자인 적용', '이 디자인으로 만들어', '오늘의 디자인으로', '스타일 적용'."
allowed-tools: ["Read", "Write", "Edit", "Glob", "Grep", "Bash", "WebFetch", "AskUserQuestion", "Skill"]
---

# Design Apply — Generate Styled Code Using DESIGN.md + Today's Design

Apply your project's design system (DESIGN.md) combined with today's award-winning design reference to generate beautiful, production-ready frontend code.

## Phase 1: Gather Design Context

### 1.1 Read DESIGN.md
1. Look for `DESIGN.md` in the project root
2. If not found → suggest running `/design-init` first:
   ```
   No DESIGN.md found. Run /design-init to create one, or provide a design reference URL.
   ```
3. Parse DESIGN.md for all design tokens:
   - Colors (primary, secondary, semantic, neutral)
   - Typography (fonts, scale, weights)
   - Spacing (base unit, scale)
   - Components (radius, shadows, transitions)
   - Layout (max-width, breakpoints, grid)
   - Patterns (nav, buttons, cards, forms)

### 1.2 Check Today's Design Cache
1. Look for today's cache: `.todays-design/cache/YYYY-MM-DD.md`
2. If exists → read it for supplementary design context
3. If not → optionally run `/todays-design` (ask user first)
4. If user declines → proceed with DESIGN.md only (still works fine)

### 1.3 Detect Project Framework
Scan for framework indicators:

| File/Pattern | Framework | Styling Approach |
|---|---|---|
| `next.config.*` | Next.js | Tailwind / CSS Modules / styled-components |
| `vite.config.*` + React | React (Vite) | Tailwind / CSS Modules / emotion |
| `nuxt.config.*` | Nuxt/Vue | Tailwind / Scoped CSS |
| `svelte.config.*` | SvelteKit | Tailwind / Scoped CSS |
| `angular.json` | Angular | SCSS / Angular Material |
| `tailwind.config.*` | Any + Tailwind | Utility classes |
| `styled-components` in package.json | Any + SC | Tagged template literals |
| `@emotion` in package.json | Any + Emotion | css prop / styled |
| `shadcn` or `components.json` | shadcn/ui | Tailwind + CSS variables |

Also check:
- `package.json` dependencies for UI libraries (MUI, Chakra, Radix, etc.)
- Existing component patterns in `src/components/`
- CSS file conventions (`.module.css`, `.scss`, `.css`)

## Phase 2: Understand the Request

Ask the user what they want to build or style. Common scenarios:

### Scenario A: Generate New Component
"Create a hero section" / "Make a pricing page" / "Build a dashboard layout"
→ Generate complete component code using DESIGN.md tokens

### Scenario B: Restyle Existing Component
"Apply today's design to this component" / "Restyle the landing page"
→ Read existing component, rewrite styles using DESIGN.md tokens

### Scenario C: Full Page/Layout
"Build the home page with today's design" / "Create a complete landing page"
→ Generate full page with multiple sections, all styled consistently

### Scenario D: Design System Implementation
"Create the theme file" / "Set up design tokens in code"
→ Generate theme configuration files (tailwind.config, theme.ts, CSS variables)

## Phase 3: Generate Code

### 3.1 Apply Design Tokens

Map DESIGN.md tokens to the project's styling approach:

**Tailwind CSS** (most common):
```tsx
// Use DESIGN.md values as Tailwind classes
<div className="bg-background text-text-primary max-w-[1280px] mx-auto px-6">
  <h1 className="font-heading text-4xl font-bold text-primary">
    {title}
  </h1>
  <p className="font-body text-base text-text-secondary mt-4">
    {description}
  </p>
  <button className="bg-primary hover:bg-primary-dark text-white rounded-lg px-6 py-2.5 transition-all duration-200">
    Get Started
  </button>
</div>
```

**CSS Variables**:
```css
/* Map DESIGN.md tokens to CSS custom properties */
.hero {
  background: var(--background);
  color: var(--text-primary);
  max-width: var(--max-width);
}
```

**CSS-in-JS**:
```tsx
const Hero = styled.div`
  background: ${({ theme }) => theme.colors.background};
  color: ${({ theme }) => theme.colors.textPrimary};
  max-width: ${({ theme }) => theme.layout.maxWidth};
`;
```

### 3.2 Incorporate Today's Design Reference

When today's design cache is available, use it to:
- Apply the award-winning site's **color harmony** approach
- Use similar **typography pairing** style
- Mirror notable **layout patterns** (e.g., asymmetric grids, full-bleed sections)
- Implement similar **micro-interactions** (hover effects, transitions)
- Adapt the **visual hierarchy** approach

**Important**: Don't copy the design — be **inspired by** it. Adapt patterns to fit the user's project and DESIGN.md tokens.

### 3.3 Chain Skills for Quality

When generating frontend code, invoke these complementary skills if available:

1. **`frontend-design`** — For high-quality, distinctive UI code generation
2. **`vercel-react-best-practices`** — For React/Next.js performance optimization
3. **`web-design-guidelines`** — For accessibility and web standards compliance

Pass DESIGN.md tokens and today's design context to these skills as additional context.

## Phase 4: Output

### Generated Code
- Write components to appropriate locations based on project structure
- Follow existing naming conventions and file organization
- Include necessary imports (fonts, icons, etc.)

### Summary
After generating code, output:

```markdown
## Design Applied ✅

### What was generated:
- {list of files created/modified}

### Design tokens used:
- Primary: {color} | Font: {heading font} + {body font}
- Based on: {today's design reference or DESIGN.md only}

### Framework integration:
- {Tailwind config updated / CSS variables added / Theme file created}

### Next steps:
- Install fonts: `npm install @fontsource/{font-name}` (if needed)
- Review and customize the generated components
- Run `/design-system` to adjust any tokens
```

## Important Guidelines

1. **Match existing patterns**: If the project already has components, follow their style (naming, structure, imports)
2. **Don't over-engineer**: Generate clean, readable code — not overly abstracted
3. **Responsive by default**: All generated layouts should be mobile-first responsive
4. **Accessible**: Include proper ARIA labels, semantic HTML, keyboard navigation
5. **Performance**: Use efficient patterns (no unnecessary re-renders, proper image handling)
6. **Token consistency**: Every color, font, spacing value should come from DESIGN.md — no magic numbers
