# Implementation Plan: Tutorial Site Redesign — Step-by-Step Copilot-Assisted Format

**Branch**: `004-tutorial-redesign` | **Date**: 2026-03-04 | **Spec**: [spec.md](spec.md)
**Input**: Feature specification from `/specs/004-tutorial-redesign/spec.md`

## Summary

Redesign the single-page tutorial site (`site/index.html`) to replace the front-loaded "Key Concepts" section and monolithic "Getting Started" numbered list with seven individually titled step sections ("Step 1" through "Step 7"). Insert a new "Step 3: Meet your AI assistant" that introduces GitHub Copilot, Ask Mode, and the repo-linking interaction pattern. Steps 4–7 each gain an "Objectives for this step" block and a copy-enabled Copilot prompt block. Steps 1–3 remain "unaided" (no Objectives block). The "What is this?", "Next Steps", and "Reference Links" sections are unchanged. Vanilla HTML/CSS only; no new dependencies.

## Technical Context

**Language/Version**: HTML5, CSS3, JavaScript (ES6+, vanilla)
**Primary Dependencies**: None — vanilla HTML/CSS/JS only
**Storage**: N/A
**Testing**: Manual browser testing (open file directly + `npx serve site`)
**Target Platform**: Modern browsers (Chrome, Firefox, Safari, Edge); responsive (375px+)
**Project Type**: Static website (single page)
**Performance Goals**: N/A — single static page, negligible load
**Constraints**: No frameworks, no build tools, no server-side logic (per constitution Principle I). Must work when opened as a local file (`file://` protocol) and via `npx serve`.
**Scale/Scope**: 1 HTML file, 1 CSS file. Change scope: ~200 lines of HTML modified/added, ~20 lines of CSS added for Objectives block styling.

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

| Principle | Status | Notes |
|-----------|--------|-------|
| I. Simplicity-First | ✅ PASS | No new dependencies, no build tools, no server-side logic. Changes are pure HTML content restructuring + minimal CSS. |
| II. Novice-Accessible | ✅ PASS | Redesign explicitly improves novice accessibility: removes front-loaded jargon, introduces concepts inline, adds AI-assisted guidance via Copilot prompts. |
| III. Spec-Driven Development | ✅ PASS | Following full SDD workflow: spec → plan → tasks → implement. |
| IV. Devcontainer & Codespaces | ✅ PASS | No environment changes. Static files work in the existing devcontainer. Preview via `npx serve site`. |
| V. Iterative & Incremental | ✅ PASS | Single feature branch delivering a complete, previewable redesign. No multi-feature scope creep. |

**Gate result: PASS** — no violations, no complexity justification needed.

## Project Structure

### Documentation (this feature)

```text
specs/004-tutorial-redesign/
├── plan.md              # This file
├── research.md          # Phase 0 output
├── data-model.md        # Phase 1 output
├── quickstart.md        # Phase 1 output
├── contracts/
│   └── ui-contract.md   # Phase 1 output — page section structure
├── checklists/
│   └── requirements.md  # Quality checklist
└── tasks.md             # Phase 2 output (/speckit.tasks)
```

### Source Code (repository root)

```text
site/
├── index.html           # Primary file modified — new section structure
└── style.css            # Minor additions — Objectives block styling
```

**Structure Decision**: No new files created. All changes are edits to the existing `site/index.html` and `site/style.css` files. The site remains a single static HTML page with one CSS file.
