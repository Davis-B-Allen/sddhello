# Quickstart: Tutorial Site Redesign

**Feature**: 004-tutorial-redesign  
**Date**: 2026-03-04

## What this feature does

Redesigns the tutorial page (`site/index.html`) from a single "Getting Started" numbered list + front-loaded "Key Concepts" section into seven individually titled step sections with Copilot-assisted guidance built in.

## Files to modify

| File | Change |
|------|--------|
| `site/index.html` | Remove `#concepts` and `#getting-started` sections; add `#step-1` through `#step-7` sections with new content structure |
| `site/style.css` | Add `.objectives`, `.objectives-heading`, `.keywords` CSS rules (~20 lines) |

## Implementation order

1. **CSS first**: Add the new `.objectives` styles to `site/style.css` so they're available when you start editing HTML.
2. **Remove old sections**: Delete the `<section id="concepts">` and `<section id="getting-started">` blocks from `index.html`.
3. **Add Steps 1–2**: Insert `<section id="step-1">` and `<section id="step-2">` with content adapted from the original list items (no Objectives block, no prompt block).
4. **Add Step 3**: Insert `<section id="step-3">` with Copilot onboarding content and the verification prompt block.
5. **Add Steps 4–7**: Insert `<section id="step-4">` through `<section id="step-7">`, each with Objectives block, prompt block, and walkthrough content adapted from the original steps 3–6.
6. **Verify**: Run `npx serve site -p 8080` and manually check all sections render correctly, all copy buttons work, and the page is responsive.

## How to verify

```bash
# Start the dev server
npx serve site -p 8080

# Open in browser and check:
# 1. No "Key Concepts" section visible
# 2. No single "Getting Started" list wrapper
# 3. Seven step sections with correct titles
# 4. Steps 4–7 have Objectives blocks with blue left border
# 5. Steps 3–7 have copy-enabled prompt blocks
# 6. All copy buttons work (click → text changes to "Copied!")
# 7. "What is this?", "Next Steps", "Reference Links" unchanged
# 8. Page is responsive at 375px width
```

## Key decisions from research

- **Objectives block**: `<aside class="objectives">` with left accent border — see [research.md](research.md#1-objectives-block--htmlcss-pattern)
- **Section IDs**: `step-1` through `step-7` — see [research.md](research.md#3-section-id-scheme)
- **Copy buttons**: Reuse existing `.code-block` / `.copy-btn` pattern unchanged
- **No new dependencies**: Pure HTML/CSS/JS, no frameworks
