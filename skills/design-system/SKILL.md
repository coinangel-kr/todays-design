---
name: design-system
description: "Update and manage the DESIGN.md design system file. Use when user asks to 'update design', 'change colors', 'modify design system', 'update DESIGN.md', 'edit design tokens', 'change font', 'update typography', 'adjust spacing', 'tweak the design', 'swap the palette', or 'use this site's style'. Also trigger when user provides a URL and wants to adopt its colors/fonts into their existing DESIGN.md. Korean triggers: '디자인 시스템 수정', '디자인 변경', '색상 변경', '폰트 변경', '디자인 업데이트', '색깔 바꿔', '폰트 바꿔', '디자인 수정', '디자인 토큰 변경'."
---

# Design System — Manage DESIGN.md

Update, modify, and maintain the project's DESIGN.md design system file.

## Phase 1: Read Current State

1. Look for `DESIGN.md` in the project root
2. If not found → suggest `/design-init`:
   ```
   No DESIGN.md found. Run /design-init to create one first.
   ```
3. Parse the current design tokens and present a quick summary:
   ```
   Current Design System:
   - Primary: #3B82F6 | Secondary: #8B5CF6
   - Heading: Inter | Body: Inter
   - Style: Modern minimal
   - Reference: awwwards.com/sites/...
   ```

## Phase 2: Understand the Change

Listen for what the user wants to modify:

### Color Changes
- "Change primary to red" → Update `primary` and compute `primary-light` / `primary-dark`
- "Make it darker" → Shift neutral palette toward darker values
- "Use this site's colors" → Fetch site, extract palette, update colors section
- When changing primary, auto-suggest complementary adjustments to semantic and neutral colors

### Typography Changes
- "Use Poppins for headings" → Update heading font
- "Switch to serif" → Suggest serif fonts (Playfair Display, Lora, Merriweather)
- "Make text larger" → Increase base size and scale ratio
- Validate that requested fonts exist (Google Fonts, system fonts)

### Spacing & Layout Changes
- "Increase spacing" → Scale up spacing values
- "Make it more compact" → Scale down spacing values
- "Change to sidebar navigation" → Update Patterns > Navigation

### Component Changes
- "Rounder buttons" → Increase border radius values
- "Add more shadow" → Increase shadow values
- "Faster transitions" → Decrease transition durations

### Style Direction Changes
- "Make it more minimal" → Reduce colors, increase whitespace, simplify
- "Make it bolder" → Increase contrasts, bolder weights, stronger colors
- "Make it playful" → Rounded shapes, brighter colors, fun fonts

### Reference Changes
- "Use this site as reference" → Fetch new site, re-analyze, update Today's Reference section
- "Remove the reference" → Clear Today's Reference section

## Phase 3: Apply Changes

1. **Edit DESIGN.md** using the Edit tool (not full rewrite):
   - Only modify the specific sections that changed
   - Preserve all other tokens and formatting

2. **Ensure consistency**:
   - If primary color changes → verify it still has enough contrast with background (WCAG AA)
   - If font changes → verify the font exists and suggest installation method
   - If spacing changes → maintain proportional relationships

3. **Show diff summary**:
   ```
   DESIGN.md updated:
   - Colors > Primary: #3B82F6 → #EF4444
   - Colors > Primary Light: #60A5FA → #F87171
   - Colors > Primary Dark: #2563EB → #DC2626

   Run /design-apply to regenerate styled components with new tokens.
   ```

## Phase 4: Sync Downstream (Optional)

If the project has framework-specific token files, suggest updating them:

- Tailwind: "Update tailwind.config with new tokens? (y/n)"
- CSS Variables: "Update :root variables in globals.css? (y/n)"
- Theme file: "Update theme.ts with new tokens? (y/n)"

Only update if user confirms — DESIGN.md is the source of truth.

## Color Utilities

When computing color variations:

### Lighten/Darken
- **Light variant**: Mix with white at ~30% → lighter tint
- **Dark variant**: Mix with black at ~20% → darker shade

### Contrast Check
- Text on background: minimum 4.5:1 ratio (WCAG AA)
- Large text on background: minimum 3:1 ratio
- Interactive elements: minimum 3:1 against adjacent colors

### Palette Generation
From a single primary color, generate:
- Primary light (tint for hover/highlight)
- Primary dark (shade for active/pressed)
- Suggest complementary accent color
- Suggest neutral palette that harmonizes

## Notes

- DESIGN.md is the **single source of truth** for design tokens
- Always use Edit (not Write) to preserve formatting and unchanged sections
- Validate color hex codes are valid 6-digit hex
- Validate font names are real, available fonts
- Keep the file structure consistent with the original template
