---
name: design-audit
description: "Audit your current site's design quality against award-winning standards and generate an improvement roadmap. Use when user asks to 'audit my design', 'review my UI', 'how does my design compare', 'design score', 'what's wrong with my design', 'improve my design', 'design feedback', 'design critique', 'rate my design', or wants to know where their UI falls short. Also trigger when user says 'my site looks outdated', 'why does my site look bad', 'how can I improve the design'. Korean triggers: '디자인 감사', '디자인 평가', '디자인 점수', '내 디자인 어때', '디자인 리뷰', '디자인 개선', '어디가 별로야', '디자인 피드백', 'UI 점검', '디자인 진단', '리디자인 해야할까'."
---

# Design Audit — Score Your Design & Get an Improvement Roadmap

Analyze your current project's design against award-winning standards. Produces a structured audit report with scores, specific weaknesses, and a prioritized improvement roadmap ordered by impact.

This skill is valuable because it doesn't just say "redesign everything" — it tells you **exactly what to fix first** for maximum visual improvement, backed by patterns from daily award-winning sites.

## Phase 1: Collect Context

### 1.1 Gather the current design
Determine what to audit. The user might provide:

- **A URL** ("audit https://mysite.com") → fetch with WebFetch
- **Current project code** ("audit my site") → scan project files
- **A specific page/component** ("audit the landing page") → read those files
- **A screenshot** → analyze the image directly

For **project code**, scan in this order:
1. `DESIGN.md` if it exists — read current design tokens
2. Global styles: `globals.css`, `tailwind.config.*`, `theme.*`, CSS variables
3. Key pages: look in `src/app/page.*`, `src/pages/index.*`, `pages/index.*`
4. Components: `src/components/` — sample 3-5 representative components
5. Layout files: `src/app/layout.*`, wrapper components

For **URLs**, fetch the site and extract:
- Color values from CSS/meta tags
- Font declarations
- Layout structure
- Component patterns

### 1.2 Gather the benchmark
The audit compares against award-winning design patterns. Load context from:

1. **Today's design cache** (`.todays-design/cache/YYYY-MM-DD.md`) — if available, use as primary benchmark
2. **DESIGN.md** — if it exists, compare current implementation vs. intended design
3. **Built-in criteria** — the analysis guide below always applies

If no today's design cache exists, offer to run `/todays-design` first for a fresher benchmark. But the audit can proceed without it using the built-in criteria.

## Phase 2: Score Across 6 Dimensions

Evaluate each dimension on a 1-10 scale. Be honest — generous scores aren't helpful.

### 2.1 Color & Contrast (Weight: High)
Award-winning patterns to check against:
- **Palette discipline**: Does the site use ≤5 distinct colors purposefully, or is it a rainbow? Award winners typically use 2-3 colors + neutrals.
- **Contrast ratios**: Does text meet WCAG AA (4.5:1)? Are CTAs visually distinct from surrounding elements?
- **Color harmony**: Is there a recognizable color relationship (monochromatic, complementary, analogous)? Or random colors?
- **Semantic consistency**: Is the same color always used for the same purpose (all CTAs same color, all errors same red)?
- **Dark/light balance**: Is the overall brightness intentional and consistent?

Score 1-3: Random colors, poor contrast, no system
Score 4-6: Basic palette exists but inconsistent, some contrast issues
Score 7-8: Clean palette, good contrast, minor inconsistencies
Score 9-10: Award-level — disciplined palette, perfect contrast, every color has clear purpose

### 2.2 Typography (Weight: High)
- **Font selection**: Is the font pairing intentional and complementary? Or default system fonts with no thought?
- **Hierarchy**: Can you immediately tell what's most important on the page? Are there clear visual levels (h1 > h2 > body > caption)?
- **Readability**: Line height, line length (45-75 chars ideal), letter-spacing — are they optimized?
- **Consistency**: Same font sizes/weights for same-level elements across pages?
- **Scale**: Is there a mathematical ratio between sizes, or random px values?

Score 1-3: Default fonts, no hierarchy, walls of same-size text
Score 4-6: Decent fonts but inconsistent sizing, hierarchy unclear
Score 7-8: Good font pairing, clear hierarchy, minor readability issues
Score 9-10: Award-level — expressive typography, perfect hierarchy, considered line lengths

### 2.3 Layout & Spacing (Weight: High)
- **Grid alignment**: Do elements align to an invisible grid, or float randomly?
- **Whitespace**: Is there enough breathing room? Or cramped elements with inconsistent gaps?
- **Spacing consistency**: Are spacing values from a system (4px base, multiples) or arbitrary?
- **Responsive**: Does the layout adapt cleanly across breakpoints, or break awkwardly?
- **Visual flow**: Does the layout guide the eye in a natural reading pattern?

Score 1-3: No grid, random spacing, breaks on mobile
Score 4-6: Basic grid but inconsistent spacing, passable responsive
Score 7-8: Clean grid, systematic spacing, good responsive
Score 9-10: Award-level — intentional whitespace rhythm, flawless responsiveness

### 2.4 Components & Interactions (Weight: Medium)
- **Button consistency**: Same style for same-level actions? Clear primary/secondary hierarchy?
- **Card patterns**: Consistent padding, radius, shadow across all cards?
- **Form design**: Inputs have clear focus states, labels, validation?
- **Hover/focus states**: Do interactive elements respond to interaction?
- **Micro-animations**: Are transitions smooth (200-300ms)? Or jarring/absent?

Score 1-3: Inconsistent components, no hover states, no transitions
Score 4-6: Some consistency, basic hover states, minimal transitions
Score 7-8: Consistent component library, good interactions
Score 9-10: Award-level — polished components, delightful micro-interactions

### 2.5 Visual Identity & Personality (Weight: Medium)
- **Distinctiveness**: Could you recognize this site with the logo removed? Or is it generic?
- **Mood coherence**: Does every element contribute to the same feeling?
- **Intentionality**: Does every design decision feel deliberate, or accidental?
- **Modern feel**: Does it use current patterns, or feel dated (gradients from 2015, etc.)?

Score 1-3: Generic template look, no personality
Score 4-6: Some character but inconsistent, partially dated
Score 7-8: Clear identity, mostly modern, coherent mood
Score 9-10: Award-level — immediately recognizable, every pixel intentional

### 2.6 Accessibility & Performance (Weight: Medium)
- **Semantic HTML**: Proper heading hierarchy, landmarks, button vs. div?
- **Keyboard navigation**: Can you tab through everything logically?
- **Alt text**: Do images have meaningful alt text?
- **Touch targets**: Are interactive elements ≥44x44px?
- **Loading**: Do images lazy-load? Is there a loading skeleton or spinner?

Score 1-3: Div soup, no keyboard support, missing alt text
Score 4-6: Some semantic HTML, partial keyboard support
Score 7-8: Good semantics, keyboard works, minor gaps
Score 9-10: Exemplary — full WCAG AA, perfect keyboard flow

## Phase 3: Generate the Audit Report

Present the report in this format:

```markdown
# Design Audit Report

## Overall Score: {X}/10
{One-sentence summary of the design's current state}

## Scores by Dimension

| Dimension | Score | Status |
|-----------|-------|--------|
| Color & Contrast | {X}/10 | {weak/average/strong/excellent} |
| Typography | {X}/10 | {weak/average/strong/excellent} |
| Layout & Spacing | {X}/10 | {weak/average/strong/excellent} |
| Components & Interactions | {X}/10 | {weak/average/strong/excellent} |
| Visual Identity | {X}/10 | {weak/average/strong/excellent} |
| Accessibility | {X}/10 | {weak/average/strong/excellent} |

## Top 3 Strengths
1. {What the design does well — be specific}
2. {Another strength}
3. {Another strength}

## Top 3 Weaknesses
1. {Most impactful issue — be specific about WHERE and WHAT}
2. {Second issue}
3. {Third issue}

## Compared to Today's Award Winner
{If today's design cache is available: "Today's winner ({site name}) scores high on {X} and {Y}. Your biggest gap is in {Z}, where they {specific technique} while your site {specific shortcoming}."}
```

## Phase 4: Improvement Roadmap

This is the key deliverable — a prioritized list of specific improvements, ordered by **impact/effort ratio** (highest impact, lowest effort first).

```markdown
## Improvement Roadmap

### Quick Wins (< 1 hour each, high visual impact)
1. **{Specific fix}** — {what to change, where, why it matters}
   - Current: {what it looks like now}
   - Target: {what it should look like}
   - Impact: {which score dimension this improves}

2. **{Another quick fix}**
   ...

### Medium Effort (1-4 hours, significant improvement)
3. **{Improvement}** — {details}
   ...

### Major Upgrades (4+ hours, transformative)
5. **{Big change}** — {details}
   ...

## Suggested Next Steps
- Run `/design-system` to update DESIGN.md with the recommended changes
- Run `/design-apply` to regenerate components with improved tokens
- Run `/todays-design` for fresh inspiration on {weakest dimension}
```

## Important Notes

- **Be honest, not generous** — inflated scores don't help anyone. A typical site without professional design attention scores 4-6. Reserve 9-10 for genuinely award-worthy work.
- **Be specific, not vague** — "improve typography" is useless. "Change body text from 14px to 16px, increase line-height from 1.3 to 1.5, and add 0.01em letter-spacing to captions" is actionable.
- **Prioritize by visual impact** — a color palette fix often transforms a site more than perfect accessibility, so list it first. But note accessibility issues clearly.
- **Reference the benchmark** — when today's design cache is available, make direct comparisons: "Today's winner uses 3 colors; you're using 8."
- **The roadmap is the product** — the scores set context, but the prioritized action items are what the user actually needs.
