<p align="center">
  <h1 align="center">Today's Design</h1>
  <p align="center">
    <strong><a href="https://claude.ai/claude-code">Claude Code</a>를 위한 AI 디자인 에이전트</strong><br>
    오늘의 수상작 디자인을 가져와서 코드에 적용하세요.
  </p>
  <p align="center">
    <a href="#설치">설치</a> &middot;
    <a href="#스킬">스킬</a> &middot;
    <a href="#designmd-1">DESIGN.md</a> &middot;
    <a href="#워크플로우">워크플로우</a>
  </p>
  <p align="center">
    <a href="README.md">English</a> | <b>한국어</b>
  </p>
</p>

---

[Awwwards](https://www.awwwards.com/), [CSS Design Awards](https://www.cssdesignawards.com/) 같은 플랫폼은 매일 최고의 웹사이트를 선정합니다. **Today's Design**은 이 수상작을 개발 워크플로우로 가져옵니다 — 수상 사이트를 분석해서 컬러, 타이포그래피, 레이아웃, 컴포넌트 패턴을 추출하고, `DESIGN.md` 파일을 통해 프로젝트에 적용할 수 있게 해줍니다.

[Google Stitch](https://stitch.withgoogle.com/)의 `DESIGN.md` 컨셉에서 영감을 받았습니다 — AI 에이전트가 이해할 수 있는 이동식 디자인 시스템 파일이죠. 핵심 차별점: **매일 실제 수상작을 기반으로 디자인 레퍼런스가 자동 갱신됩니다.**

```
/todays-design  →  /design-init  →  /design-apply  →  완성된 앱!
```

---

## 설치

```bash
git clone https://github.com/coinangel-kr/todays-design.git ~/todays-design

# Claude Code 스킬 디렉토리에 링크
ln -s ~/todays-design/skills/todays-design ~/.claude/skills/todays-design
ln -s ~/todays-design/skills/design-init   ~/.claude/skills/design-init
ln -s ~/todays-design/skills/design-apply  ~/.claude/skills/design-apply
ln -s ~/todays-design/skills/design-system ~/.claude/skills/design-system
```

Claude Code를 재시작하면 4개 스킬이 자동으로 인식됩니다.

> **다른 방법:** `~/.claude/plugins/todays-design`에 직접 clone하면 플러그인 방식으로 설치됩니다.

---

## 스킬

### `/todays-design`

오늘의 수상작 웹사이트를 가져와 분석합니다.

1. 캐시 확인 → 2. Awwwards RSS 가져오기 (실패 시 CSSDA) → 3. 수상 사이트 방문 → 4. 디자인 토큰 추출 → 5. 구조화된 분석 결과 출력 → 6. 캐싱

<details>
<summary><strong>출력 예시</strong></summary>

```markdown
# Today's Design — 2026-03-26

## 수상작
- 사이트: Corentin Bernadou Portfolio
- 수상: Awwwards SOTD
- URL: https://corentinbernadou.com/

## 컬러 팔레트
| 역할       | Hex     |
|------------|---------|
| Primary    | #FF6B00 |
| Background | #FFFFFF |
| Text       | #000000 |

## 타이포그래피
- 폰트: Inter Variable (100-900)
- 스타일: 스위스 스타일, 타이포그래피 중심

## 핵심 디자인 기법
1. 스위스 스타일 타이포그래피 — 인쇄물에서 가져온 강한 그래픽 시스템
2. 3색 팔레트 — 오렌지 하나만 액센트로 극도의 절제
3. GSAP + WebGL — 의도적이면서 노이즈 없는 모션
```

</details>

---

### `/design-init`

프로젝트에 `DESIGN.md` 디자인 시스템을 생성합니다. 소스를 선택할 수 있습니다:

| 소스 | 설명 |
|------|------|
| **오늘의 디자인** | 오늘의 수상작 기반으로 생성 (권장) |
| **기존 코드** | 현재 CSS / Tailwind / 테마 파일에서 토큰 추출 |
| **빈 템플릿** | 깨끗한 상태에서 시작 |
| **커스텀 URL** | 원하는 웹사이트를 레퍼런스로 지정 |

프레임워크를 자동 감지합니다: Next.js, React, Vue, Svelte, Angular, React Native, Flutter.

---

### `/design-apply`

`DESIGN.md`와 오늘의 디자인을 기반으로 스타일된 코드를 생성합니다.

```
> /design-apply
> "히어로 섹션이랑 가격표 카드 만들어줘"
```

지원 스타일링: **Tailwind** · **CSS Variables** · **styled-components / emotion** · **shadcn/ui** · **React Native** · **Plain CSS/SCSS**

---

### `/design-system`

`DESIGN.md`의 디자인 토큰을 부분적으로 수정합니다. 파일 전체를 다시 쓸 필요 없이 원하는 부분만 변경합니다.

```
> "프라이머리 색상 보라색으로 바꿔줘"
> "헤딩 폰트 Poppins로 변경"
> "좀 더 미니멀하게 만들어줘"
> "이 사이트 색상 가져와: https://linear.app"
```

---

## DESIGN.md

[Google Stitch](https://stitch.withgoogle.com/) 형식을 따릅니다 — CSS 값 나열이 아닌, AI 에이전트가 이해할 수 있는 자연어 기반 디자인 시스템입니다.

```
DESIGN.md
├── 1. Visual Theme & Atmosphere    시각적 테마 & 분위기
├── 2. Color Palette & Roles        컬러 팔레트 & 역할
├── 3. Typography Rules             타이포그래피 규칙
├── 4. Component Stylings           컴포넌트 스타일링 (버튼, 카드, 폼, 네비게이션, 아이콘)
├── 5. Layout Principles            레이아웃 원칙 (브레이크포인트, 모션, 접근성)
└── 6. Today's Reference            오늘의 레퍼런스 (매일 갱신되는 수상작 디자인)
```

웹과 모바일 모두 단일 템플릿으로 지원 — 프로젝트 타입에 따라 플랫폼별 섹션이 자동 활성화됩니다.

---

## 워크플로우

**오늘의 디자인으로 새 프로젝트 시작:**
```
/todays-design           # 오늘의 수상작 확인
/design-init             # "오늘의 디자인" 선택
/design-apply            # "랜딩 페이지 만들어줘"
```

**기존 프로젝트에 디자인 시스템 추가:**
```
/design-init             # "기존 코드" 선택 → 현재 토큰 추출
/todays-design           # 오늘의 트렌드 확인
/design-system           # "오늘의 컬러 방식 적용해줘"
```

**원하는 사이트를 레퍼런스로:**
```
/design-init             # "커스텀 URL" 선택 → https://linear.app
/design-apply            # "대시보드 레이아웃 만들어줘"
```

---

## 디자인 소스

| 소스 | 방법 | 상태 |
|------|------|------|
| [Awwwards](https://www.awwwards.com/) | RSS 피드 | v1 |
| [CSS Design Awards](https://www.cssdesignawards.com/) | 웹 스크래핑 | v1 |
| [CSS Winner](https://www.csswinner.com/) | — | v2 예정 |
| [FWA](https://thefwa.com/) | — | v2+ 예정 |

---

## 프로젝트 구조

```
todays-design/
├── skills/
│   ├── todays-design/       # 매일 수상작 가져오기 & 분석
│   ├── design-init/         # DESIGN.md 생성
│   ├── design-apply/        # 디자인 기반 코드 생성
│   └── design-system/       # 디자인 토큰 수정
├── templates/
│   └── DESIGN.md            # 통합 템플릿 (웹 + 모바일)
├── examples/
│   ├── example-design.md    # 생성 예시
│   └── workflow.md          # 사용 가이드
├── .claude-plugin/
│   └── plugin.json
├── LICENSE                   # MIT
└── README.md
```

---

## 기여하기

PR을 환영합니다! 기여 아이디어:

- 새로운 디자인 소스 추가 (CSS Winner, FWA, Behance, Dribbble)
- JS 기반 사이트에서 디자인 토큰 추출 개선
- 프레임워크별 코드 생성 패턴 추가
- 다양한 디자인 스타일의 `DESIGN.md` 예시 제작

---

## 라이선스

[MIT](LICENSE)
