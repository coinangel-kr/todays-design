---
name: todays-design
description: "Fetch and analyze today's award-winning website designs for inspiration or as a redesign reference. Use when user asks for 'today's design', 'todays design', 'daily design', 'design inspiration', 'design reference', 'award winning design', 'design of the day', 'what's trending in design', 'show me good designs', 'design ideas', or mentions wanting fresh design ideas before building or redesigning UI. Also trigger when user wants to see examples before a redesign. Korean triggers: '오늘의 디자인', '디자인 레퍼런스', '디자인 영감', '수상작', '디자인 트렌드', '좋은 디자인 보여줘', '디자인 참고', '요즘 디자인'."
---

# Today's Design — Fetch Daily Award-Winning Designs

Fetch today's award-winning website/app designs from design award platforms, analyze their UI/UX patterns, and present actionable design insights.

## Phase 1: Check Cache

1. Check if today's design is already cached:
   ```
   .todays-design/cache/YYYY-MM-DD.md
   ```
   - If cache exists and is from today → read and present it, skip to Phase 4
   - If no cache → proceed to Phase 2

2. Create cache directory if needed:
   ```bash
   mkdir -p .todays-design/cache
   ```

## Phase 2: Fetch Today's Award Winners

Fetch from multiple sources in priority order. If one fails, fall back to the next.

### Source 1: Awwwards (Primary — RSS Feed)

1. Fetch the RSS feed:
   ```
   WebFetch: https://www.awwwards.com/feed/
   ```

2. Parse the RSS XML to extract the **most recent** entry:
   - `<title>` — Site name
   - `<link>` — Awwwards page URL
   - `<pubDate>` — Publication date
   - `<description>` — Site description (may contain HTML)

3. From the Awwwards page, try to extract:
   - The actual site URL (the awarded website, not the Awwwards listing)
   - Category tags
   - Score/rating if visible

### Source 2: CSS Design Awards (Fallback — Web Scraping)

1. Fetch the winners page:
   ```
   WebFetch: https://www.cssdesignawards.com/wotd-award-winners
   ```

2. Parse the HTML to find the most recent WOTD (Website of the Day):
   - Look for the first/latest entry with award date
   - Extract: site name, URL, award date, scores (UI/UX/Innovation)

3. If a specific site page is found (e.g., `/sites/{name}/{id}/`):
   ```
   WebFetch: https://www.cssdesignawards.com/sites/{name}/{id}/
   ```
   - Extract judge scores and feedback

### Extraction Priority
- Try Awwwards first (most reliable via RSS)
- If Awwwards fails or returns stale data → try CSS Design Awards
- If both fail → use WebSearch as last resort:
  ```
  WebSearch: "site of the day" OR "website of the day" award {today's date}
  ```

## Phase 3: Analyze the Winning Site

Once we have the winning site's URL:

1. **Fetch the site**:
   ```
   WebFetch: {winning-site-url}
   ```

2. **Extract design tokens from HTML/CSS**:

   ### Colors
   - `<meta name="theme-color">` value
   - CSS `:root` custom properties (--primary, --accent, etc.)
   - Most used background colors (hero, header, footer)
   - Most used text colors
   - CTA button colors
   - Build a palette: primary, secondary, accent, neutrals

   ### Typography
   - Google Fonts `<link>` tags → font family names
   - `@font-face` declarations → custom fonts
   - Adobe Fonts (`use.typekit.net`) links
   - CSS `font-family` declarations on body/headings
   - Font sizes used (h1-h6, body, small)
   - Font weights used

   ### Layout
   - Max-width of main container
   - Grid system (columns, gaps)
   - Breakpoint values in media queries
   - Navigation pattern (top bar, sidebar, hamburger)
   - Hero section layout

   ### Components
   - Button styles (border-radius, padding, hover effects)
   - Card patterns (shadows, borders, padding)
   - Form input styles
   - Icon library used (Lucide, Heroicons, FontAwesome, etc.)

   ### Interactions
   - CSS transitions/animations
   - Scroll behaviors
   - Hover effects
   - Loading patterns

3. **Identify design trends**:
   - What makes this design award-worthy?
   - Key visual techniques (glassmorphism, gradients, bold typography, whitespace, etc.)
   - Unique interaction patterns
   - Color harmony approach (monochromatic, complementary, analogous, etc.)

## Phase 4: Present Results

Output the analysis in this structured format:

```markdown
# 🎨 Today's Design — {YYYY-MM-DD}

## Award Winner
- **Site**: {site name}
- **URL**: {site URL}
- **Award**: {Awwwards SOTD / CSSDA WOTD}
- **Award Page**: {award listing URL}
- **Category**: {category tags}

## Design Analysis

### Color Palette
| Role | Color | Hex |
|------|-------|-----|
| Primary | 🟦 | #XXXXXX |
| Secondary | 🟪 | #XXXXXX |
| Accent | 🟨 | #XXXXXX |
| Background | ⬜ | #XXXXXX |
| Text | ⬛ | #XXXXXX |

### Typography
- **Heading**: {font name} ({weight})
- **Body**: {font name} ({weight})
- **Style**: {serif/sans-serif/display/mono}

### Layout & Structure
- **Navigation**: {pattern description}
- **Hero**: {layout description}
- **Grid**: {column/layout system}
- **Scroll**: {scroll behavior}

### Key Design Techniques
1. {technique 1 — e.g., "Bold oversized typography with high contrast"}
2. {technique 2 — e.g., "Subtle micro-animations on scroll"}
3. {technique 3 — e.g., "Monochromatic palette with single accent color"}

### Component Highlights
- **Buttons**: {description}
- **Cards**: {description}
- **Interactions**: {description}

## Applicability
{2-3 sentences on how these design patterns could be applied to the user's current project, based on detected framework and project type}

---
> Fetched by Today's Design | Sources: Awwwards, CSS Design Awards
```

## Phase 5: Cache Results

1. Write the full analysis to cache:
   ```
   .todays-design/cache/YYYY-MM-DD.md
   ```

2. This allows:
   - Same-day re-requests to be instant
   - `/design-init` and `/design-apply` to reference today's design without re-fetching
   - Historical browsing of past designs

## Error Handling

| Scenario | Action |
|----------|--------|
| RSS feed returns 403/timeout | Fall back to CSS Design Awards |
| Both sources fail | Use WebSearch as last resort |
| Winning site blocks WebFetch | Analyze from award page description only |
| No award announced today | Use most recent available (note the date) |
| All sources fail | Inform user, suggest providing a URL manually |

## Notes

- Always respect robots.txt — do not aggressively scrape
- Cache results to minimize external requests
- The analysis should be actionable, not just descriptive
- Focus on patterns the user can actually implement
- If the winning site is highly interactive (WebGL, Three.js), focus on the static design elements (colors, type, layout) rather than the 3D/animation aspects
