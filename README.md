<p align="center">
  <h1 align="center">Today's Design</h1>
  <p align="center">
    <strong>AI design agent for <a href="https://claude.ai/claude-code">Claude Code</a></strong><br>
    Fetch today's award-winning design. Apply it to your code.
  </p>
  <p align="center">
    <a href="#installation">Installation</a> &middot;
    <a href="#skills">Skills</a> &middot;
    <a href="#designmd">DESIGN.md</a> &middot;
    <a href="#workflows">Workflows</a>
  </p>
</p>

---

Every day, sites like [Awwwards](https://www.awwwards.com/) and [CSS Design Awards](https://www.cssdesignawards.com/) pick award-winning websites. **Today's Design** brings those designs into your development workflow — it fetches the winner, analyzes its design system (colors, typography, layout, components), and helps you apply those patterns to your own project through a `DESIGN.md` file.

Inspired by [Google Stitch](https://stitch.withgoogle.com/)'s `DESIGN.md` — a portable design system that AI agents can read. The twist: **your reference updates daily** from real award-winning sites.

매일 Awwwards, CSS Design Awards 같은 플랫폼에서 수상하는 웹사이트를 가져와 디자인 시스템을 분석하고, `DESIGN.md`를 통해 프로젝트에 적용합니다. Google Stitch의 DESIGN.md 컨셉에서 영감을 받았으며, **매일 실제 수상작 기반으로 레퍼런스가 자동 갱신**되는 것이 핵심입니다.

```
/todays-design  →  /design-init  →  /design-apply  →  Your beautiful app
```

---

## Installation

```bash
git clone https://github.com/coinangel-kr/todays-design.git ~/todays-design

# Link skills to Claude Code
ln -s ~/todays-design/skills/todays-design ~/.claude/skills/todays-design
ln -s ~/todays-design/skills/design-init   ~/.claude/skills/design-init
ln -s ~/todays-design/skills/design-apply  ~/.claude/skills/design-apply
ln -s ~/todays-design/skills/design-system ~/.claude/skills/design-system
```

Restart Claude Code. All 4 skills will be recognized automatically.

> **Alternative:** Clone directly to `~/.claude/plugins/todays-design` for plugin-style install.

---

## Skills

### `/todays-design`

Fetch and analyze today's award-winning website.

오늘의 수상작 웹사이트를 가져와 분석합니다.

1. Check cache → 2. Fetch Awwwards RSS (or CSSDA fallback) → 3. Visit winning site → 4. Extract design tokens → 5. Output structured analysis → 6. Cache for reuse

<details>
<summary><strong>Example output</strong></summary>

```markdown
# Today's Design — 2026-03-26

## Award Winner
- Site: Corentin Bernadou Portfolio
- Award: Awwwards SOTD
- URL: https://corentinbernadou.com/

## Color Palette
| Role       | Hex     |
|------------|---------|
| Primary    | #FF6B00 |
| Background | #FFFFFF |
| Text       | #000000 |

## Typography
- Font: Inter Variable (100-900)
- Style: Swiss-inspired, typography-driven

## Key Design Techniques
1. Swiss Style typography with strong graphic systems
2. Restrained 3-color palette with single accent
3. GSAP + WebGL for intentional, noise-free motion
```

</details>

---

### `/design-init`

Create a `DESIGN.md` for your project.

프로젝트에 `DESIGN.md` 디자인 시스템을 생성합니다.

| Source | Description |
|--------|-------------|
| Today's Design | Base on today's award winner (recommended) |
| Existing Code | Extract from your CSS / Tailwind / theme files |
| Blank Template | Start clean |
| Custom URL | Use any website as reference |

Auto-detects your framework: Next.js, React, Vue, Svelte, Angular, React Native, Flutter.

---

### `/design-apply`

Generate styled code using `DESIGN.md` + today's design.

`DESIGN.md`와 오늘의 디자인을 기반으로 스타일된 코드를 생성합니다.

```
> /design-apply
> "Create a hero section and pricing cards"
```

Supports: **Tailwind** · **CSS Variables** · **styled-components / emotion** · **shadcn/ui** · **React Native** · **Plain CSS/SCSS**

---

### `/design-system`

Update `DESIGN.md` tokens without rewriting the file.

`DESIGN.md`의 디자인 토큰을 부분 수정합니다.

```
> "Change primary color to purple"
> "Switch heading font to Poppins"
> "Make it more minimal"
> "Use this site's colors: https://linear.app"
```

---

## DESIGN.md

Follows [Google Stitch](https://stitch.withgoogle.com/) format — natural language descriptions that AI agents understand, not just raw CSS values.

Google Stitch 형식을 따릅니다 — CSS 값이 아닌 AI가 이해할 수 있는 자연어 기반 디자인 시스템입니다.

```
DESIGN.md
├── 1. Visual Theme & Atmosphere
├── 2. Color Palette & Roles
├── 3. Typography Rules
├── 4. Component Stylings  (Buttons, Cards, Forms, Nav, Icons)
├── 5. Layout Principles   (Breakpoints, Motion, Accessibility)
└── 6. Today's Reference   (Daily award-winning design)
```

Single template for both web and mobile — platform-specific sections activate based on your project.

웹과 모바일 모두 단일 템플릿 — 프로젝트 타입에 따라 플랫폼별 섹션이 활성화됩니다.

---

## Workflows

**New project with today's design:**
```
/todays-design           # See today's winner
/design-init             # Choose "Today's Design"
/design-apply            # "Build a landing page"
```

**Add to existing project:**
```
/design-init             # Choose "Existing Code"
/todays-design           # Get fresh inspiration
/design-system           # "Adopt today's color approach"
```

**Custom reference:**
```
/design-init             # Choose "Custom URL" → https://linear.app
/design-apply            # "Create a dashboard layout"
```

---

## Design Sources

| Source | Method | Status |
|--------|--------|--------|
| [Awwwards](https://www.awwwards.com/) | RSS Feed | v1 |
| [CSS Design Awards](https://www.cssdesignawards.com/) | Web Scraping | v1 |
| [CSS Winner](https://www.csswinner.com/) | — | v2 |
| [FWA](https://thefwa.com/) | — | v2+ |

---

## Project Structure

```
todays-design/
├── skills/
│   ├── todays-design/       # Fetch & analyze daily winner
│   ├── design-init/         # Generate DESIGN.md
│   ├── design-apply/        # Apply design to code
│   └── design-system/       # Update design tokens
├── templates/
│   └── DESIGN.md            # Universal template
├── examples/
│   ├── example-design.md    # Sample output
│   └── workflow.md          # Usage guide
├── .claude-plugin/
│   └── plugin.json
├── LICENSE                   # MIT
└── README.md
```

---

## Contributing

PRs welcome. Some ideas:

- New design sources (CSS Winner, FWA, Behance, Dribbble)
- Better token extraction from JS-heavy sites
- More framework-specific patterns
- Example `DESIGN.md` files for different design styles

---

## License

[MIT](LICENSE)
