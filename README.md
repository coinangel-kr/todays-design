# Today's Design

> AI design agent that brings today's award-winning designs to your code.
>
> 매일 수상하는 디자인을 당신의 코드로 가져오는 AI 디자인 에이전트.

<p align="center">
  <strong>/todays-design</strong> &rarr; <strong>/design-init</strong> &rarr; <strong>/design-apply</strong> &rarr; Your beautiful app!
</p>

---

## What is Today's Design? | Today's Design이란?

**Today's Design** is a [Claude Code](https://claude.ai/claude-code) skill set that fetches daily award-winning website designs from platforms like [Awwwards](https://www.awwwards.com/) and [CSS Design Awards](https://www.cssdesignawards.com/), analyzes their UI/UX patterns, and helps you apply those design trends to your projects through a `DESIGN.md` design system file.

**Today's Design**은 [Claude Code](https://claude.ai/claude-code) 스킬 세트로, [Awwwards](https://www.awwwards.com/)와 [CSS Design Awards](https://www.cssdesignawards.com/) 같은 플랫폼에서 매일 수상하는 웹사이트 디자인을 가져와 UI/UX 패턴을 분석하고, `DESIGN.md` 디자인 시스템 파일을 통해 프로젝트에 적용할 수 있도록 도와줍니다.

### Why? | 왜 만들었나?

Inspired by [Google Stitch](https://stitch.withgoogle.com/)'s `DESIGN.md` concept — a portable, machine-readable design system file that AI agents can understand. But with a unique twist: **your design reference updates every day** based on real award-winning sites.

[Google Stitch](https://stitch.withgoogle.com/)의 `DESIGN.md` 컨셉에서 영감을 받았습니다 — AI 에이전트가 이해할 수 있는 이동식 디자인 시스템 파일이죠. 하지만 핵심 차별점이 있습니다: **매일 실제 수상작을 기반으로 디자인 레퍼런스가 업데이트됩니다.**

### Key Features | 주요 특징

| Feature | Description |
|---------|-------------|
| **Daily Design Fetching** | Automatically pulls today's award-winning site from Awwwards RSS & CSSDA |
| **Design Analysis** | Extracts colors, typography, layout, components, and interaction patterns |
| **DESIGN.md Generation** | Creates a Stitch-compatible design system file for your project |
| **Framework-Aware Code Gen** | Generates styled code matching your stack (Next.js, React, Vue, Svelte, etc.) |
| **Smart Caching** | Same-day requests use cached results — no redundant fetching |
| **Web & Mobile** | Single `DESIGN.md` template with platform-specific sections for both web and mobile |
| **Skill Chaining** | Works with `frontend-design`, `vercel-react-best-practices`, `web-design-guidelines` |

| 기능 | 설명 |
|------|------|
| **일일 디자인 가져오기** | Awwwards RSS & CSSDA에서 오늘의 수상작 자동 추출 |
| **디자인 분석** | 컬러, 타이포그래피, 레이아웃, 컴포넌트, 인터랙션 패턴 추출 |
| **DESIGN.md 생성** | Stitch 호환 디자인 시스템 파일 프로젝트에 생성 |
| **프레임워크 인식 코드 생성** | 프로젝트 스택에 맞는 스타일 코드 생성 (Next.js, React, Vue, Svelte 등) |
| **스마트 캐싱** | 같은 날 요청 시 캐시 사용 — 중복 요청 없음 |
| **웹 & 모바일** | 단일 `DESIGN.md` 템플릿에 플랫폼별 섹션 포함 |
| **스킬 체이닝** | `frontend-design`, `vercel-react-best-practices`, `web-design-guidelines`와 연동 |

---

## Installation | 설치

### Option 1: Symlink to Skills (Recommended)

```bash
git clone https://github.com/coinangel-kr/todays-design.git ~/todays-design

# Symlink each skill to Claude Code skills directory
ln -s ~/todays-design/skills/todays-design ~/.claude/skills/todays-design
ln -s ~/todays-design/skills/design-init ~/.claude/skills/design-init
ln -s ~/todays-design/skills/design-apply ~/.claude/skills/design-apply
ln -s ~/todays-design/skills/design-system ~/.claude/skills/design-system
```

### Option 2: Plugin Install

```bash
git clone https://github.com/coinangel-kr/todays-design.git ~/.claude/plugins/todays-design
```

After installation, restart Claude Code. The 4 skills will be automatically recognized.

설치 후 Claude Code를 재시작하면 4개 스킬이 자동 인식됩니다.

---

## Skills | 스킬 목록

### `/todays-design` — Fetch Today's Award Winner

Fetches and analyzes today's award-winning website design.

오늘의 수상작 웹사이트 디자인을 가져와 분석합니다.

**What it does:**
1. Checks local cache (`.todays-design/cache/YYYY-MM-DD.md`)
2. Fetches from Awwwards RSS feed (primary) or CSS Design Awards (fallback)
3. Visits the actual winning site and extracts design tokens
4. Presents a structured analysis: colors, typography, layout, components, techniques
5. Caches the result for same-day reuse

**동작 순서:**
1. 로컬 캐시 확인 (`.todays-design/cache/YYYY-MM-DD.md`)
2. Awwwards RSS 피드(1순위) 또는 CSS Design Awards(fallback)에서 가져오기
3. 실제 수상 사이트 방문, 디자인 토큰 추출
4. 구조화된 분석 결과 출력: 컬러, 타이포, 레이아웃, 컴포넌트, 기법
5. 같은 날 재사용을 위해 캐싱

**Example output:**
```
# Today's Design — 2026-03-26

## Award Winner
- Site: Corentin Bernadou Portfolio
- Award: Awwwards SOTD
- URL: https://corentinbernadou.com/

## Design Analysis
### Color Palette
| Role    | Hex     |
|---------|---------|
| Primary | #FF6B00 |
| Background | #FFFFFF |
| Text    | #000000 |

### Typography
- Font: Inter Variable (100-900)
- Style: Swiss-inspired, typography-driven

### Key Design Techniques
1. Swiss Style typography with strong graphic systems
2. Restrained 3-color palette with single accent
3. GSAP + WebGL for intentional, noise-free motion
```

---

### `/design-init` — Create DESIGN.md

Generates a `DESIGN.md` design system file for your project.

프로젝트를 위한 `DESIGN.md` 디자인 시스템 파일을 생성합니다.

**Options when creating:**

| Option | Description |
|--------|-------------|
| **Today's Design** | Seed your design system from today's award winner |
| **Existing Code** | Extract tokens from your current CSS/Tailwind/theme files |
| **Blank Template** | Start from a clean template |
| **Custom URL** | Use any website as your design reference |

| 옵션 | 설명 |
|------|------|
| **오늘의 디자인** | 오늘의 수상작 기반으로 디자인 시스템 생성 |
| **기존 코드** | 현재 CSS/Tailwind/테마 파일에서 토큰 추출 |
| **빈 템플릿** | 깨끗한 템플릿에서 시작 |
| **커스텀 URL** | 원하는 웹사이트를 레퍼런스로 지정 |

**Auto-detects your framework**: Next.js, React, Vue, Svelte, Angular, React Native, Expo, Flutter

---

### `/design-apply` — Apply Design to Code

Generates styled frontend code using your `DESIGN.md` + today's design reference.

`DESIGN.md` + 오늘의 디자인 레퍼런스를 사용해 스타일된 프론트엔드 코드를 생성합니다.

**Supports:**
- Tailwind CSS (utility classes)
- CSS Variables (custom properties)
- CSS-in-JS (styled-components, emotion)
- shadcn/ui (CSS variables + Tailwind)
- React Native / Expo (StyleSheet)
- Plain CSS / SCSS

**Example:**
```
> /design-apply
> "Create a hero section and pricing cards"
```
The skill reads your `DESIGN.md`, checks today's design cache, detects your framework, and generates production-ready styled components.

---

### `/design-system` — Update DESIGN.md

Modify your design system without rewriting the whole file.

전체 파일을 다시 작성하지 않고 디자인 시스템을 수정합니다.

**Examples:**
```
> /design-system
> "Change primary color to purple"
> "Switch heading font to Poppins"
> "Make the design more minimal"
> "Use this site's colors: https://linear.app"
```

---

## DESIGN.md

The `DESIGN.md` file follows [Google Stitch's design system format](https://stitch.withgoogle.com/) — descriptive natural language that AI agents can understand, not just raw CSS tokens.

`DESIGN.md` 파일은 [Google Stitch의 디자인 시스템 형식](https://stitch.withgoogle.com/)을 따릅니다 — CSS 토큰이 아닌, AI 에이전트가 이해할 수 있는 자연어 기반 설명입니다.

### Structure | 구조

```
DESIGN.md
├── 1. Visual Theme & Atmosphere    # 시각적 테마 & 분위기
├── 2. Color Palette & Roles        # 컬러 팔레트 & 역할
├── 3. Typography Rules             # 타이포그래피 규칙
├── 4. Component Stylings           # 컴포넌트 스타일링
│   ├── Buttons
│   ├── Cards & Containers
│   ├── Inputs & Forms
│   ├── Navigation
│   └── Icons
├── 5. Layout Principles            # 레이아웃 원칙
│   ├── Breakpoints
│   ├── Scroll & Motion
│   └── Accessibility
└── 6. Today's Reference            # 오늘의 레퍼런스
```

Platform-specific sections (mobile safe areas, gestures, haptics) are included as HTML comments that activate based on your project type.

플랫폼별 섹션(모바일 세이프 에어리어, 제스처, 햅틱)은 프로젝트 타입에 따라 활성화되는 HTML 주석으로 포함됩니다.

---

## Design Sources | 디자인 소스

| Source | Method | Status |
|--------|--------|--------|
| [Awwwards](https://www.awwwards.com/) | RSS Feed (`/feed/`) | v1 |
| [CSS Design Awards](https://www.cssdesignawards.com/) | Web Scraping | v1 |
| [CSS Winner](https://www.csswinner.com/) | Web Scraping | Planned (v2) |
| [FWA](https://thefwa.com/) | Headless Browser | Planned (v2+) |

---

## Workflow Examples | 워크플로우 예시

### Start a new project with today's design | 오늘의 디자인으로 새 프로젝트 시작

```
/todays-design              # See today's award winner
/design-init                 # Choose "Today's Design" → creates DESIGN.md
/design-apply                # "Build a landing page hero section"
```

### Add design system to existing project | 기존 프로젝트에 디자인 시스템 추가

```
/design-init                 # Choose "Existing Code" → extracts current tokens
/todays-design               # See what's trending today
/design-system               # "Adopt the color approach from today's reference"
```

### Use any site as reference | 원하는 사이트를 레퍼런스로 사용

```
/design-init                 # Choose "Custom URL" → enter https://linear.app
/design-apply                # "Create a dashboard sidebar and main content area"
```

### Daily design refresh | 매일 디자인 리프레시

```
/todays-design               # Check today's winner
/design-system               # "Update our palette with today's color approach"
```

---

## Compatibility | 호환성

| Framework | Styling Output |
|-----------|---------------|
| Next.js / React | Tailwind, CSS Modules, styled-components, emotion |
| Vue / Nuxt | Tailwind, Scoped CSS |
| Svelte / SvelteKit | Tailwind, Scoped CSS |
| Angular | SCSS, Angular Material |
| React Native / Expo | StyleSheet, styled-components |
| Plain HTML | CSS Custom Properties |
| shadcn/ui | CSS Variables + Tailwind |

---

## File Structure | 파일 구조

```
todays-design/
├── .claude-plugin/
│   └── plugin.json              # Plugin metadata
├── skills/
│   ├── todays-design/
│   │   ├── SKILL.md             # Main skill: fetch & analyze
│   │   └── references/
│   │       ├── sources.md       # Source parsing guide
│   │       └── analysis-guide.md
│   ├── design-init/
│   │   ├── SKILL.md             # Initialize DESIGN.md
│   │   └── references/
│   │       └── design-md-template.md
│   ├── design-apply/
│   │   ├── SKILL.md             # Apply design to code
│   │   └── references/
│   │       └── apply-patterns.md
│   └── design-system/
│       └── SKILL.md             # Update DESIGN.md
├── templates/
│   └── DESIGN.md                # Universal template (web + mobile)
├── examples/
│   ├── example-design.md        # Example generated DESIGN.md
│   └── workflow.md              # Workflow guide
├── README.md
└── LICENSE
```

---

## Contributing | 기여

Contributions are welcome! 기여를 환영합니다!

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/new-source`)
3. Add new design sources, improve analysis, or enhance templates
4. Submit a Pull Request

### Ideas for contribution | 기여 아이디어
- Add new design award sources (CSS Winner, FWA, Behance, Dribbble)
- Improve design token extraction from JS-heavy sites
- Add more framework-specific apply patterns
- Create example DESIGN.md files for popular design styles
- Localization (more languages in README)

---

## License

[MIT](LICENSE)

---

<p align="center">
  <sub>Built for the Claude Code community. Made with AI.</sub>
</p>
