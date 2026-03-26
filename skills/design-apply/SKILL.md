---
name: design-apply
description: "Apply design system to generate styled frontend code. Use when user asks to 'apply design', 'design apply', 'use today's design', 'style this', 'make it look like', 'apply DESIGN.md', 'restyle this component', 'generate styled code', or mentions wanting to generate new styled components or pages. For redesign/improvement requests ('redesign', 'make this prettier', 'improve my design'), suggest running /design-audit first to get a prioritized roadmap, then come back to /design-apply. Korean triggers: '디자인 적용', '이 디자인으로 만들어', '오늘의 디자인으로', '스타일 적용', '스타일 코드 생성', '컴포넌트 만들어'."
---

# Design Apply — Generate Styled Code Using DESIGN.md

Apply your project's design system (DESIGN.md) to generate new components or restyle existing ones. Combines DESIGN.md tokens with today's award-winning design reference for production-ready results.

For **redesign or design improvement** requests, suggest running `/design-audit` first — it produces a prioritized improvement roadmap. Then use `/design-apply` to execute the roadmap items.

## Phase 1: Gather Design Context

### 1.1 Read DESIGN.md
1. Look for `DESIGN.md` in the project root
2. If not found → suggest running `/design-init` first
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
| `shadcn` or `components.json` | shadcn/ui | Tailwind + CSS variables |

Also check `package.json` dependencies, existing component patterns, CSS conventions.

## Phase 2: Determine the Task

### Scenario A: Generate New Component
**Triggers**: "Create a hero section", "Make a pricing page", "Build a dashboard"

1. Generate complete component code using DESIGN.md tokens
2. Follow existing project patterns (naming, file structure, imports)
3. Apply responsive design, accessibility, performance best practices

### Scenario B: Restyle Existing Component
**Triggers**: "Restyle this component", "Apply the design system to this file"

1. Read the existing component file(s)
2. Rewrite **only the styling** — preserve all business logic, state, data flow
3. Map every color/font/spacing to DESIGN.md tokens (no magic numbers)
4. Show a summary of what changed

### Scenario C: Design System Implementation
**Triggers**: "Create the theme file", "Set up design tokens in code"

Generate theme configuration files: tailwind.config, theme.ts, CSS variables, etc.

## Phase 3: Generate Code

### 3.1 Apply Design Tokens
Map DESIGN.md tokens to the project's styling approach:

**Tailwind CSS**:
```tsx
<div className="bg-background text-text-primary max-w-[1280px] mx-auto px-6">
  <h1 className="font-heading text-4xl font-bold text-primary">{title}</h1>
  <button className="bg-primary hover:bg-primary-dark text-white rounded-lg px-6 py-2.5 transition-all duration-200">
    Get Started
  </button>
</div>
```

**CSS Variables**:
```css
.hero { background: var(--background); color: var(--text-primary); }
```

**CSS-in-JS**:
```tsx
const Hero = styled.div`
  background: ${({ theme }) => theme.colors.background};
`;
```

### 3.2 Incorporate Today's Design Reference
When today's design cache is available, draw **inspiration** (don't copy):
- Apply the award-winning site's color harmony approach
- Use similar typography pairing style
- Mirror notable layout patterns
- Implement similar micro-interactions

### 3.3 Chain Skills for Quality
When generating frontend code, invoke these complementary skills if available:
1. **`frontend-design`** — For high-quality, distinctive UI code generation
2. **`vercel-react-best-practices`** — For React/Next.js performance optimization
3. **`web-design-guidelines`** — For accessibility and web standards compliance

## Phase 4: Output

After generating code, output:

```markdown
## Design Applied

### Files created/modified:
- {list}

### Design tokens used:
- Primary: {color} | Font: {heading font} + {body font}
- Based on: {today's design reference or DESIGN.md only}

### Next steps:
- Install fonts if needed: `npm install @fontsource/{font-name}`
- Run `/design-audit` to verify design quality
- Run `/design-system` to adjust any tokens
```

## Guidelines

1. **Match existing patterns**: Follow the project's naming, structure, imports
2. **Responsive by default**: Mobile-first responsive
3. **Accessible**: Semantic HTML, ARIA labels, keyboard navigation
4. **Token consistency**: Every value from DESIGN.md — no magic numbers
5. **Preserve logic during restyles**: Never modify business logic or data flow
