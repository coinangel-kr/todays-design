---
name: design-init
description: "Initialize a DESIGN.md design system for the current project. Use when user asks to 'create design system', 'design init', 'make DESIGN.md', 'set up design tokens', 'initialize design', or mentions 'DESIGN.md'. Also trigger when user says 'design system setup' or 'design configuration'."
argument-hint: "[web|app]"
allowed-tools: ["Read", "Write", "Edit", "Glob", "Grep", "Bash", "WebFetch", "AskUserQuestion", "Skill"]
---

# Design Init — Create DESIGN.md for Your Project

Generate a portable, machine-readable `DESIGN.md` design system file for the current project.

## Phase 1: Detect Project Context

1. **Check if DESIGN.md already exists** in the project root:
   - If exists → ask user: "DESIGN.md already exists. Overwrite, merge, or cancel?"
   - If not → proceed

2. **Detect project type** by scanning for framework indicators:
   - `package.json` → check for next, react, vue, svelte, angular, react-native, expo
   - `pubspec.yaml` → Flutter
   - `Podfile` or `*.xcodeproj` → iOS
   - `build.gradle` → Android
   - If unclear → ask user

3. **Determine platform** (used to customize `DESIGN.md` content):
   - Web frameworks → fill in web-specific sections (breakpoints, scroll, accessibility)
   - Mobile frameworks → fill in mobile-specific sections (safe areas, gestures, haptics) via the `<!-- FOR MOBILE APP -->` comment blocks in the template
   - Mixed/unclear → fill in both
   - User can override via argument: `/design-init web` or `/design-init app`
   - All platforms use the single `DESIGN.md` template with platform-specific sections marked by HTML comments

## Phase 2: Choose Design Source

Ask the user how they want to seed their design system:

### Option A: Today's Design (Recommended)
1. Run `/todays-design` skill to fetch today's award-winning design
2. Use the analysis results to populate DESIGN.md tokens:
   - Extract color palette from the winning site
   - Identify typography (fonts, scale)
   - Note layout patterns and component styles
3. Fill template with extracted values + today's reference section

### Option B: Existing Project Code
1. Scan the project for existing design tokens:
   - CSS/SCSS files: look for `--custom-properties`, color values, font declarations
   - Tailwind config: `tailwind.config.{js,ts}` → extract theme values
   - Theme files: `theme.{js,ts}`, `tokens.{js,ts}`, `styles/`
   - Component libraries: check for MUI, Chakra, shadcn/ui theme configs
2. Map found tokens to DESIGN.md structure
3. Fill gaps with sensible defaults

### Option C: Blank Template
1. Use the `DESIGN.md` template as-is
2. Replace placeholders with minimal defaults
3. User fills in values manually

### Option D: Custom URL Reference
1. Ask user for the reference site URL
2. Use `WebFetch` to retrieve the site
3. Analyze the HTML/CSS for:
   - `<meta name="theme-color">` and color values in CSS
   - Font declarations (`font-family`, Google Fonts links)
   - Layout structure (grid, flexbox patterns)
   - Component patterns (buttons, cards, forms)
4. Populate DESIGN.md from analysis

## Phase 3: Generate DESIGN.md

1. Read the appropriate template from the plugin's `templates/` directory:
   - Find the plugin directory by checking common locations:
     - `~/.claude/plugins/todays-design/templates/`
     - Glob for `**/todays-design/templates/DESIGN*.md`
   - Fallback: use the embedded template structure from this skill

2. Fill in the template with gathered values:
   - Replace all `{placeholder}` tokens with actual values
   - Remove unused optional sections
   - Ensure all color values are valid hex codes
   - Validate font names are real fonts

3. Write `DESIGN.md` to the project root

4. Output summary:
   ```
   ✅ DESIGN.md created at ./DESIGN.md

   Design System Summary:
   - Platform: Web / Mobile / Both
   - Source: Today's Design / Existing Code / Blank / Custom URL
   - Primary Color: #XXXXXX
   - Heading Font: {font}
   - Body Font: {font}

   Next steps:
   - Review and customize: edit DESIGN.md directly
   - Apply to code: run /design-apply
   - Update later: run /design-system
   ```

## Template Reference (Embedded Fallback)

If templates directory is not found, use this minimal structure:

```markdown
# Design System

## Brand
- **Name**: {project-name}
- **Style**: modern

## Colors
### Primary
- Primary: #3B82F6
- Primary Light: #60A5FA
- Primary Dark: #2563EB

### Neutral
- Background: #FFFFFF
- Surface: #F8FAFC
- Text Primary: #0F172A
- Text Secondary: #64748B
- Border: #E2E8F0

## Typography
- **Heading Font**: Inter
- **Body Font**: Inter
- **Base Size**: 16px

## Spacing
- **Base Unit**: 4px
- **Scale**: 4, 8, 12, 16, 24, 32, 48, 64

## Components
- **Border Radius**: sm: 4px, md: 8px, lg: 16px
- **Shadow**: sm: 0 1px 2px rgba(0,0,0,0.05), md: 0 4px 6px rgba(0,0,0,0.1)

## Layout
- **Max Width**: 1280px
- **Breakpoints**: sm: 640px, md: 768px, lg: 1024px, xl: 1280px
```

## Important Notes

- Always write DESIGN.md in the **project root** (same level as package.json, etc.)
- Do NOT overwrite without user confirmation
- If the project uses Tailwind, suggest mapping DESIGN.md tokens to `tailwind.config`
- If the project uses CSS-in-JS, note that tokens can be imported as constants
