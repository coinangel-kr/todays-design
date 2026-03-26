# Design Award Sources — Parsing Guide

## Source 1: Awwwards (Primary)

### RSS Feed
- **URL**: `https://www.awwwards.com/feed/`
- **Format**: RSS 2.0 / XML
- **Update Frequency**: Daily (new Site of the Day)
- **Content**: Title, link (Awwwards page), pubDate, description

### RSS Parsing Strategy

The RSS feed returns XML. Extract these fields from each `<item>`:

```xml
<item>
  <title>Site Name - Awwwards SOTD</title>
  <link>https://www.awwwards.com/sites/site-name</link>
  <pubDate>Wed, 26 Mar 2026 00:00:00 +0000</pubDate>
  <description><![CDATA[<p>Description of the site...</p>]]></description>
</item>
```

**Steps**:
1. Fetch `https://www.awwwards.com/feed/`
2. Find all `<item>` blocks
3. Take the first (most recent) item
4. Extract `<title>`, `<link>`, `<pubDate>`, `<description>`
5. Visit `<link>` to get the actual awarded site URL

### Awwwards Page Structure
The award listing page at `awwwards.com/sites/{name}` typically contains:
- The actual site URL (external link to the awarded website)
- Category tags
- Score breakdown
- Screenshots

### Alternative Endpoints
- Sites of the Day listing: `https://www.awwwards.com/websites/sites_of_the_day/`
- Alternative feed: `https://www.awwwards.com/sites/feed-2`

---

## Source 2: CSS Design Awards (Fallback)

### Winners Page
- **URL**: `https://www.cssdesignawards.com/wotd-award-winners`
- **Format**: HTML
- **Update Frequency**: Daily (new WOTD)

### HTML Parsing Strategy

The winners page lists awarded sites. Look for:

1. **Award entries** with date stamps (e.g., "AWARDED 2026 MAR 26")
2. **Site links** pointing to `/sites/{name}/{id}/`
3. **Thumbnails** at `https://cssdesignawards.com/cdasites/YYYY/YYYYMM/`

### Individual Site Page
URL pattern: `https://www.cssdesignawards.com/sites/{name}/{id}/`

Contains:
- Site name and agency/designer
- External URL to the actual site
- Judge scores: UI Design, UX Design, Innovation
- Individual judge comments
- Award date
- Thumbnail/screenshot

### Score System
- Categories: UI Design, UX Design, Innovation
- Scale: 1-10 per judge
- Averaged across all judges

---

## Source 3: WebSearch Fallback

If both primary sources fail, use WebSearch:

```
"site of the day" OR "website of the day" award 2026
```

Or more specific:
```
awwwards "site of the day" March 2026
cssdesignawards "website of the day" March 2026
```

---

## Fetching the Actual Award-Winning Site

After getting the award listing, the critical step is finding the **actual website URL** (not the award platform page).

### Extraction Methods
1. **Awwwards**: Look for external link on the award page (usually prominent "Visit Site" button)
2. **CSSDA**: Look for external URL on the individual site page
3. **Fallback**: WebSearch for the exact site name

### What to Analyze on the Actual Site
When fetching the real website via WebFetch:

1. **`<head>` section**:
   - `<meta name="theme-color">`
   - `<link>` tags for Google Fonts / Adobe Fonts
   - CSS file links
   - Viewport and other meta tags

2. **CSS analysis** (inline `<style>` or fetched CSS):
   - `:root` / `html` custom properties
   - `body` font-family, font-size, color
   - Heading styles (h1-h6)
   - Button/link styles
   - Media queries (breakpoints)

3. **Body structure**:
   - Navigation pattern (nav, header layout)
   - Hero section (first major section)
   - Grid/layout system classes
   - Footer structure

4. **JavaScript frameworks** (for context):
   - `__NEXT_DATA__` → Next.js
   - `__NUXT__` → Nuxt
   - `ng-version` → Angular
   - `data-reactroot` → React
