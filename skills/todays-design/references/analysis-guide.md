# Design Analysis Guide

## What Makes Award-Winning Design?

When analyzing a Site of the Day winner, evaluate these dimensions:

### 1. Visual Hierarchy
- How does the site guide the eye?
- What's the primary focal point?
- How are headings, subheadings, and body text differentiated?
- Is whitespace used effectively?

### 2. Color Strategy
- **Monochromatic**: Single hue with variations (elegant, cohesive)
- **Complementary**: Opposite colors on the wheel (high contrast, energetic)
- **Analogous**: Adjacent colors (harmonious, natural)
- **Triadic**: Three equidistant colors (vibrant, balanced)
- **Split-complementary**: Base + two adjacent to complement (versatile)
- How many colors are used total? (Award winners often use 3-5 max)
- Is there a clear accent color for CTAs?

### 3. Typography
- **Font pairing**: How do heading and body fonts complement each other?
- **Contrast**: serif + sans-serif? Display + text?
- **Hierarchy**: Size, weight, and color differentiation
- **White space**: Line height, letter spacing, paragraph spacing
- **Trends**: Oversized headings, variable fonts, kinetic type

### 4. Layout Patterns
- **Asymmetric grids**: Breaking traditional 12-column grid
- **Bento grid**: Mixed-size cards in a grid
- **Full-bleed sections**: Edge-to-edge content blocks
- **Scroll-driven**: Horizontal scroll, parallax, snap sections
- **Split-screen**: Dual panel layouts

### 5. Micro-interactions
- Button hover effects (scale, color, underline)
- Cursor customization
- Scroll-triggered animations
- Page transitions
- Loading states
- Form field interactions

### 6. Current Design Trends (2025-2026)
- **Brutalism**: Raw, unpolished aesthetics
- **Neo-morphism**: Soft shadows, embossed elements
- **Glassmorphism**: Frosted glass, blur effects
- **3D elements**: WebGL, Three.js integration
- **AI-generated art**: Unique, non-stock imagery
- **Variable fonts**: Dynamic typography
- **Dark mode first**: Dark as default
- **Oversized typography**: Hero text at 120px+
- **Organic shapes**: Blobs, waves, irregular borders
- **Grain/noise textures**: Subtle texture overlays

## Analysis Output Structure

For each design, produce:

### Actionable Insights (Most Important)
Don't just describe what you see — explain **how to implement it**:

**Bad**: "The site uses a gradient background"
**Good**: "Hero section uses a radial gradient from #1a1a2e to #16213e, centered at 30% 40%, creating depth. Implement with: `background: radial-gradient(ellipse at 30% 40%, #1a1a2e, #16213e)`"

**Bad**: "Nice typography"
**Good**: "Headings use Space Grotesk (700) at a 1.333 ratio scale, paired with Inter (400) for body text. The contrast between the geometric display font and neutral body font creates clear hierarchy."

### Design Token Extraction
Map observations directly to DESIGN.md tokens:

```
Observed: Hero background is #0F172A
→ DESIGN.md: Colors > Neutral > Background: #0F172A

Observed: CTA button is #3B82F6 with 8px radius
→ DESIGN.md: Colors > Primary: #3B82F6
→ DESIGN.md: Components > Border Radius > md: 8px

Observed: Body text is 16px Inter, heading is 48px Space Grotesk
→ DESIGN.md: Typography > Body Font: Inter
→ DESIGN.md: Typography > Heading Font: Space Grotesk
→ DESIGN.md: Typography > Base Size: 16px
```

### Applicability Assessment
Consider the user's project context:
- Is the design pattern appropriate for their industry/audience?
- Can the patterns be implemented with their framework?
- Which elements are universally applicable vs. site-specific?
- What's the effort level? (Quick win vs. significant refactor)
