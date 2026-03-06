# Quickstart: Concept Pages

**Feature**: 005-concept-pages  
**Date**: 2026-03-06

## What this feature does

Expands the existing single-page static site into a multi-page site by adding seven concept pages — each explaining a key tool or idea in plain language for complete beginners. Adds a "Concepts" navigation section to the main page linking to all seven pages.

## Files to modify

| File | Change |
|------|--------|
| `site/style.css` | Add `.breadcrumb` CSS rules (~15 lines) |
| `site/index.html` | Add `<section id="concepts">` with links to all 7 concept pages, placed between `#step-7` and `#next-steps` |

## Files to create

| File | Content |
|------|---------|
| `site/git.html` | Git & Version Control concept page |
| `site/github.html` | GitHub concept page |
| `site/copilot.html` | GitHub Copilot & AI Agents concept page |
| `site/speckit.html` | Spec-Driven Development & spec-kit concept page |
| `site/devcontainers.html` | Devcontainers concept page |
| `site/codespaces.html` | GitHub Codespaces concept page |
| `site/ghpages.html` | GitHub Pages concept page |

## Implementation order

1. **CSS first**: Add `.breadcrumb` styles to `site/style.css` so they're available for concept pages.
2. **Create concept pages**: Build all seven `.html` files using the template from `contracts/ui-contract.md`. Each page follows the same four-section content structure (What is it? → Analogy → Why it matters → Learn more).
3. **Update main page**: Add the `<section id="concepts">` navigation section to `site/index.html`.
4. **Verify**: Start dev server and manually check all pages.

## How to verify

```bash
# Start the dev server
npx serve site -p 8080

# Open in browser and check:
# 1. Main page has a "Concepts" section between Step 7 and Next Steps
# 2. All 7 concept links work (click each one)
# 3. Each concept page has: heading, subtitle, 4 content sections
# 4. Each concept page has a working "← Home" breadcrumb link
# 5. Each concept page has at least one external documentation link
# 6. Visual styling matches the main page (same fonts, colors, layout)
# 7. All pages are readable at 375px viewport width
# 8. "What is this?", tutorial steps, "Next Steps", "Reference Links" are unchanged
```

## Key decisions from research

- **Navigation pattern**: `<section id="concepts">` with `<ul>` of links — see [research.md](research.md#1-navigation-pattern-on-main-page)
- **Page template**: Breadcrumb nav above header + 4-section content structure — see [research.md](research.md#2-concept-page-html-template)
- **File naming**: Short, lowercase filenames (`git.html`, `github.html`, etc.) — see [research.md](research.md#3-file-naming-convention)
- **CSS**: Reuse existing `style.css` + add breadcrumb rules — see [research.md](research.md#4-css-reuse-and-additions)
- **Content structure**: What → Analogy → Why → Learn more — see [research.md](research.md#5-content-structure-per-concept-page)
