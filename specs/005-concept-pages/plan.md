# Implementation Plan: Concept Pages

**Branch**: `005-concept-pages` | **Date**: 2026-03-06 | **Spec**: [spec.md](spec.md)
**Input**: Feature specification from `/specs/005-concept-pages/spec.md`

## Summary

Expand the existing single-page static site into a multi-page site by adding seven concept pages (Git, GitHub, GitHub Copilot, spec-kit, Devcontainers, Codespaces, GitHub Pages). Each page provides a beginner-friendly explanation with analogies, external documentation links, and a back-to-home link. The main page gets a new "Concepts" navigation section linking to all seven pages. No new dependencies or build tools — pure HTML/CSS using the existing stylesheet.

## Technical Context

**Language/Version**: HTML5, CSS3, vanilla JavaScript (existing copy-button script)
**Primary Dependencies**: None — static HTML/CSS site, no frameworks
**Storage**: N/A — static files only
**Testing**: Manual browser testing (no automated test framework)
**Target Platform**: Modern browsers, GitHub Pages static hosting
**Project Type**: Static website
**Performance Goals**: N/A — static pages, instant load
**Constraints**: Must work at 375px viewport width (mobile). No build tools. No server-side logic.
**Scale/Scope**: 7 new HTML pages + 1 modified HTML page + possible minor CSS additions

## Constitution Check (Pre-Phase 0)

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

| Principle | Status | Notes |
|-----------|--------|-------|
| I. Simplicity-First | ✅ PASS | Pure HTML/CSS, no frameworks, no build tools. Static files viewable via `npx serve`. |
| II. Novice-Accessible | ✅ PASS | Content written for zero prior experience. Second-person voice, plain language, analogies. |
| III. Spec-Driven Development | ✅ PASS | Full spec-kit workflow: specify → plan → tasks → implement. |
| IV. Devcontainer & Codespaces | ✅ PASS | No new tooling required. All work happens in existing devcontainer. |
| V. Iterative & Incremental | ✅ PASS | Single feature branch. Each concept page is independently previewable. |

**Gate result**: All principles satisfied. No violations. Proceeding to Phase 0.

## Project Structure

### Documentation (this feature)

```text
specs/005-concept-pages/
├── plan.md              # This file
├── research.md          # Phase 0 output
├── data-model.md        # Phase 1 output
├── quickstart.md        # Phase 1 output
├── contracts/           # Phase 1 output
│   └── ui-contract.md
└── tasks.md             # Phase 2 output (/speckit.tasks)
```

### Source Code (repository root)

```text
site/
├── index.html           # Modified: add Concepts navigation section
├── style.css            # Modified: minor additions for nav section and concept page layout
├── git.html             # New: Git & Version Control concept page
├── github.html          # New: GitHub concept page
├── copilot.html         # New: GitHub Copilot & AI Agents concept page
├── speckit.html         # New: Spec-Driven Development & spec-kit concept page
├── devcontainers.html   # New: Devcontainers concept page
├── codespaces.html      # New: GitHub Codespaces concept page
└── ghpages.html         # New: GitHub Pages concept page
```

**Structure Decision**: All concept pages live as sibling `.html` files alongside `index.html` in the `site/` directory. This keeps the project flat and simple — no subdirectories, no routing, no build step. Relative links work naturally between pages.

## Constitution Check (Post-Phase 1 Re-evaluation)

| Principle | Status | Notes |
|-----------|--------|-------|
| I. Simplicity-First | ✅ PASS | 7 new HTML files + ~15 lines of CSS. No frameworks, no build tools, no server logic. All pages viewable via `npx serve`. |
| II. Novice-Accessible | ✅ PASS | Content structure uses plain language, second-person voice, analogies. Back-to-home breadcrumb with `aria-label` for accessibility. |
| III. Spec-Driven Development | ✅ PASS | Full spec-kit workflow followed. All artifacts generated. |
| IV. Devcontainer & Codespaces | ✅ PASS | No new tooling. Static files work in existing devcontainer. |
| V. Iterative & Incremental | ✅ PASS | Single feature branch. Each concept page is independently previewable. |

**Gate result**: All principles satisfied post-design. No violations. Ready for `/speckit.tasks`.

## Complexity Tracking

No constitution violations. Table not needed.
