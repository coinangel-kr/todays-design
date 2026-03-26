---
name: design-apply
description: "Apply design system to generate styled frontend code, or redesign existing pages/components. Use when user asks to 'apply design', 'design apply', 'use today's design', 'style this', 'make it look like', 'apply DESIGN.md', 'redesign', 'restyle', 'modernize this page', 'make this prettier', 'refresh the UI', 'revamp', 'give this a facelift', or mentions wanting to generate styled components or transform an existing design. Also trigger on requests like 'redesign this site', 'redesign this page', 'make this look like [url]', 'apply [site]'s design to my project'. Korean triggers: '디자인 적용', '이 디자인으로 만들어', '오늘의 디자인으로', '스타일 적용', '리디자인', '리디자인 해줘', '예쁘게 만들어', '디자인 바꿔', '이쁘게', '새로 디자인', '디자인 갈아엎어', '페이지 리뉴얼', 'UI 바꿔'."
---

# Design Apply — Generate Styled Code & Redesign Existing UI

Apply your project's design system (DESIGN.md) to generate new components or **redesign existing pages and components**. Combines DESIGN.md tokens with today's award-winning design reference for production-ready results.

## Phase 1: Gather Design Context

### 1.1 Read DESIGN.md
1. Look for `DESIGN.md` in the project root
2. If not found → suggest running `/design-init` first:
   ```
   No DESIGN.md found. Run /design-init to create one, or provide a design reference URL.
   ```
3. Parse DESIGN.md for all design tokens:
   - Colors, Typography, Spacing, Components, Layout, Patterns

### 1.2 Check Today's Design Cache
1. Look for today's cache: `.todays-design/cache/YYYY-MM-DD.md`
2. If exists → read it for supplementary design context
3. If not → optionally run `/todays-design` (ask user first)
4. If user declines → proceed with DESIGN.md only

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

Also check `package.json` dependencies, existing component patterns, CSS conventions.

## Phase 2: Determine the Task

Identify which scenario the user needs. If unclear, ask.

### Scenario A: Generate New Component
**Triggers**: "Create a hero section", "Make a pricing page", "Build a dashboard layout"

1. Generate complete component code using DESIGN.md tokens
2. Follow existing project patterns (naming, file structure, imports)
3. Apply responsive design, accessibility, and performance best practices

### Scenario B: Redesign Existing Component
**Triggers**: "Restyle this component", "Apply today's design to this", "Make this prettier"

1. Read the existing component file(s) the user indicates
2. Analyze current styling: what's there now (colors, fonts, layout, structure)
3. Identify what needs to change to align with DESIGN.md
4. Rewrite **only the styling** — preserve all business logic, state management, data flow
5. Show a before/after summary of design changes

### Scenario C: Redesign from URL Reference
**Triggers**: "Redesign this to look like [url]", "Make my site look like [url]", "이 사이트처럼 만들어"

This is the **full redesign workflow**:

1. **Analyze the reference site**:
   ```
   WebFetch: {reference-url}
   ```
   Extract the reference's design system:
   - Color palette (theme-color meta, CSS variables, dominant colors)
   - Typography (Google Fonts links, font-family declarations, type scale)
   - Layout patterns (grid system, navigation, hero approach)
   - Component styles (buttons, cards, forms — border-radius, shadows, hover effects)
   - Visual techniques (glassmorphism, gradients, animation patterns)

2. **Analyze the user's existing pages**:
   - Read the current source code (components, pages, styles)
   - Map out what exists: which pages, which components, what layout
   - Identify the structural skeleton that should be preserved

3. **Create a redesign plan** and present it to the user:
   ```
   Redesign Plan:

   Reference: {url} — {brief description of its design approach}

   Changes:
   - Colors: current (#XXX) → new (#YYY, inspired by reference)
   - Typography: current (Roboto) → new (Inter, matching reference's geometric feel)
   - Layout: current (basic centered) → new (asymmetric grid, full-bleed hero)
   - Components: buttons (square → rounded), cards (flat → elevated)
   - Motion: add scroll-triggered fade-up animations

   Preserved:
   - All business logic and data flow
   - Route structure
   - API integrations

   Proceed? (y/n)
   ```

4. **Execute the redesign** after user confirms:
   - Update DESIGN.md with new tokens (or suggest `/design-system` for this)
   - Rewrite component styles systematically
   - Update global styles (CSS variables, Tailwind config, theme file)
   - Ensure consistency across all modified components

### Scenario D: Full Page Redesign (Current Project)
**Triggers**: "Redesign the landing page", "리디자인 해줘", "Refresh the home page UI"

1. **Scan current page**: Read all components that make up the target page
2. **Analyze current design**: document the existing visual approach
3. **Apply DESIGN.md + today's reference**: rewrite styles for every component on the page
4. **Ensure consistency**: all components on the page share the same design language
5. **Preserve structure**: keep routing, data fetching, state — only change visual presentation

### Scenario E: Design System Implementation
**Triggers**: "Create the theme file", "Set up design tokens in code"

Generate theme configuration files: tailwind.config, theme.ts, CSS variables, etc.

## Phase 3: Generate Code

### 3.1 Apply Design Tokens
Map DESIGN.md tokens to the project's styling approach:

**Tailwind CSS**:
```tsx
<div className="bg-background text-text-primary max-w-[1280px] mx-auto px-6">
  <h1 className="font-heading text-4xl font-bold text-primary">
    {title}
  </h1>
  <button className="bg-primary hover:bg-primary-dark text-white rounded-lg px-6 py-2.5 transition-all duration-200">
    Get Started
  </button>
</div>
```

**CSS Variables**:
```css
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
`;
```

### 3.2 Incorporate Today's Design Reference
When today's design cache is available, draw **inspiration** (don't copy):
- Apply the award-winning site's color harmony approach
- Use similar typography pairing style
- Mirror notable layout patterns
- Implement similar micro-interactions
- Adapt the visual hierarchy approach

### 3.3 Chain Skills for Quality
When generating frontend code, invoke these complementary skills if available:
1. **`frontend-design`** — For high-quality, distinctive UI code generation
2. **`vercel-react-best-practices`** — For React/Next.js performance optimization
3. **`web-design-guidelines`** — For accessibility and web standards compliance

## Phase 4: Output

### Summary
After generating or redesigning code, output:

```markdown
## Design Applied

### What was generated/changed:
- {list of files created/modified}

### Design tokens used:
- Primary: {color} | Font: {heading font} + {body font}
- Based on: {today's design reference / DESIGN.md / reference URL}

### For redesigns — what changed:
- Colors: {old} → {new}
- Typography: {old} → {new}
- Layout: {description of structural changes}
- Components: {what was restyled}

### What was preserved:
- {business logic, routing, data flow — everything non-visual}

### Next steps:
- Review the changes in your browser
- Run `/design-system` to fine-tune any tokens
- Install fonts if needed: `npm install @fontsource/{font-name}`
```

## Important Guidelines

1. **Preserve logic during redesigns**: Never modify business logic, API calls, state management, or data flow. Only change visual presentation.
2. **Match existing patterns**: Follow the project's naming, structure, and import conventions
3. **Responsive by default**: All generated layouts should be mobile-first responsive
4. **Accessible**: Include proper ARIA labels, semantic HTML, keyboard navigation
5. **Token consistency**: Every color, font, spacing value should come from DESIGN.md — no magic numbers
6. **Show before/after**: For redesigns, always summarize what changed so the user can review
