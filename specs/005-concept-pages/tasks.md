# Tasks: Concept Pages — Multi-Page Beginner Concept Explanations

**Input**: Design documents from `/specs/005-concept-pages/`
**Prerequisites**: plan.md, spec.md, research.md, data-model.md, contracts/ui-contract.md, quickstart.md

**Tests**: No automated tests requested. Verification is manual browser testing per quickstart.md.

**Organization**: Tasks are grouped by user story. All 7 concept page files are independent (different files), so creation tasks within each story phase are parallelizable. The navigation section on index.html depends on concept pages existing but can be written first since links are static.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (e.g., US1, US2, US3)
- Include exact file paths in descriptions

## Path Conventions

- Static site files: `site/index.html`, `site/style.css`, `site/*.html`
- No other source directories are created or modified

---

## Phase 1: Setup

**Purpose**: Add CSS rules needed by concept pages before creating HTML files

- [X] T001 [P] Add `.breadcrumb` CSS rules to `site/style.css` per the New CSS Rules Required section in contracts/ui-contract.md

---

## Phase 3: User Story 1 — Browse Concept Pages from Home (Priority: P1) 🎯 MVP

**Goal**: Create all 7 concept page files using the template structure from contracts/ui-contract.md and add a "Concepts" navigation section to the main page linking to each page. Every concept page includes breadcrumb nav, heading, subtitle, four content sections (What is it?, Think of it like..., Why does it matter?, Learn more), and a footer.

**Independent Test**: Open main page, locate the Concepts section, click each of the 7 concept links. Verify each page loads with a heading, content, and a working "← Home" breadcrumb link that returns to the main page.

### Implementation for User Story 1

- [X] T002 [P] [US1] Create `site/git.html` with concept page template: breadcrumb nav, heading "Git & Version Control", subtitle, 4 content sections (what/analogy/why/learn-more), and footer per contracts/ui-contract.md
- [X] T003 [P] [US1] Create `site/github.html` with concept page template: breadcrumb nav, heading "GitHub", subtitle, 4 content sections (what/analogy/why/learn-more), and footer per contracts/ui-contract.md
- [X] T004 [P] [US1] Create `site/copilot.html` with concept page template: breadcrumb nav, heading "GitHub Copilot & AI Agents", subtitle, 4 content sections (what/analogy/why/learn-more), and footer per contracts/ui-contract.md
- [X] T005 [P] [US1] Create `site/speckit.html` with concept page template: breadcrumb nav, heading "Spec-Driven Development & spec-kit", subtitle, 4 content sections (what/analogy/why/learn-more), and footer per contracts/ui-contract.md
- [X] T006 [P] [US1] Create `site/devcontainers.html` with concept page template: breadcrumb nav, heading "Devcontainers", subtitle, 4 content sections (what/analogy/why/learn-more), and footer per contracts/ui-contract.md
- [X] T007 [P] [US1] Create `site/codespaces.html` with concept page template: breadcrumb nav, heading "GitHub Codespaces", subtitle, 4 content sections (what/analogy/why/learn-more), and footer per contracts/ui-contract.md
- [X] T008 [P] [US1] Create `site/ghpages.html` with concept page template: breadcrumb nav, heading "GitHub Pages", subtitle, 4 content sections (what/analogy/why/learn-more), and footer per contracts/ui-contract.md
- [X] T009 [US1] Add `<section id="concepts">` navigation section with heading, intro text, and links to all 7 concept pages to `site/index.html`, placed between `#step-7` and `#next-steps` per contracts/ui-contract.md

**Checkpoint**: All 7 concept pages load via links from the main page Concepts section. "← Home" breadcrumb on every concept page navigates back to index.html.

---

## Phase 4: User Story 2 — Learn a Concept in Depth (Priority: P1)

**Goal**: Ensure every concept page has high-quality, beginner-friendly content: plain language, second-person voice ("you"), at least one practical analogy, and at least one external documentation link. Content must not assume prior technical knowledge.

**Independent Test**: Have a non-technical person read any concept page. They should understand the concept, identify the analogy, and find the documentation link without confusion.

### Implementation for User Story 2

- [X] T010 [P] [US2] Refine content in `site/git.html`: ensure "saving drafts / undo history" analogy, plain language throughout, second-person voice, no unexplained jargon, and link to https://docs.github.com/en/get-started/using-git per FR-005, FR-006, FR-007
- [X] T011 [P] [US2] Refine content in `site/github.html`: ensure "Google Drive for code" analogy, plain language throughout, second-person voice, no unexplained jargon, and link to https://docs.github.com/en/get-started per FR-005, FR-006, FR-007
- [X] T012 [P] [US2] Refine content in `site/copilot.html`: ensure "knowledgeable coding buddy" analogy, plain language throughout, second-person voice, no unexplained jargon, and link to https://docs.github.com/en/copilot per FR-005, FR-006, FR-007
- [X] T013 [P] [US2] Refine content in `site/speckit.html`: ensure "architectural blueprint" analogy, plain language throughout, second-person voice, no unexplained jargon, and link to https://github.com/github/spec-kit per FR-005, FR-006, FR-007
- [X] T014 [P] [US2] Refine content in `site/devcontainers.html`: ensure "fully furnished apartment" analogy, plain language throughout, second-person voice, no unexplained jargon, and link to https://containers.dev/ per FR-005, FR-006, FR-007
- [X] T015 [P] [US2] Refine content in `site/codespaces.html`: ensure "virtual workshop in the cloud" analogy, plain language throughout, second-person voice, no unexplained jargon, and link to https://docs.github.com/en/codespaces per FR-005, FR-006, FR-007
- [X] T016 [P] [US2] Refine content in `site/ghpages.html`: ensure "one-click publishing" analogy, plain language throughout, second-person voice, no unexplained jargon, and link to https://docs.github.com/en/pages per FR-005, FR-006, FR-007

**Checkpoint**: Every concept page uses plain, jargon-free language in second-person voice, includes a relatable analogy, and links to official documentation.

---

## Phase 5: User Story 3 — Consistent Page Design (Priority: P2)

**Goal**: Verify all concept pages share the same visual styling as the main page — same CSS, fonts, colors, heading hierarchy, and responsive layout.

**Independent Test**: Open each concept page side-by-side with the main page. Styling should be visually consistent. Test at both desktop and 375px mobile width.

### Implementation for User Story 3

- [X] T017 [P] [US3] Verify all 7 concept pages link to `style.css` and render with consistent heading styles, fonts, colors, and layout matching `site/index.html` per FR-009
- [X] T018 [US3] Verify all concept pages and the Concepts navigation section on the main page are readable and usable at 375px viewport width per FR-010

**Checkpoint**: Visual consistency confirmed across all pages at both desktop and mobile widths.

---

## Phase 6: Polish & Cross-Cutting Concerns

**Purpose**: Final validation and cleanup

- [X] T019 Run `npx serve site -p 8080` and perform full walkthrough verification per quickstart.md checklist
- [X] T020 Verify `#what-is-this`, tutorial steps (`#step-1` through `#step-7`), `#next-steps`, and `#reference-links` sections are unchanged in `site/index.html`
- [X] T021 Validate all 7 concept page `<title>` elements match the format "{Topic} – Mike's AI Journey" per FR-012 and data-model.md

---

## Dependencies & Execution Order

### Phase Dependencies

- **Phase 1 (Setup/CSS)**: No dependencies — can start immediately
- **Phase 3 (US1 — Create pages + navigation)**: Depends on Phase 1 (breadcrumb CSS must exist before concept pages are created)
- **Phase 4 (US2 — Content quality)**: Depends on Phase 3 (pages must exist before content can be refined)
- **Phase 5 (US3 — Visual consistency)**: Depends on Phase 3 and Phase 4 (all content and styling in place)
- **Phase 6 (Polish)**: Depends on all previous phases

### User Story Dependencies

- **US1 (Browse from Home)**: Foundational — US2 and US3 depend on pages existing
- **US2 (Learn in Depth)**: Depends on US1 (needs concept pages to exist for content refinement)
- **US3 (Consistent Design)**: Depends on US1 (pages must exist to verify styling). Independent of US2.

### Parallel Opportunities

- **T002–T008** (7 concept pages) are all [P] — they create different files with no interdependencies
- **T010–T016** (7 content refinements) are all [P] — they edit different files with no interdependencies
- **Phase 4 (US2)** and **Phase 5 (US3)** can start concurrently after Phase 3, since US2 edits page content while US3 checks styling

---

## Parallel Example: Phase 3 — Concept Page Creation

```text
# All 7 pages can be created simultaneously (different files):
T002: Create site/git.html
T003: Create site/github.html
T004: Create site/copilot.html
T005: Create site/speckit.html
T006: Create site/devcontainers.html
T007: Create site/codespaces.html
T008: Create site/ghpages.html
```

## Parallel Example: Phase 4 — Content Refinement

```text
# All 7 refinements can run simultaneously (different files):
T010: Refine content in site/git.html
T011: Refine content in site/github.html
T012: Refine content in site/copilot.html
T013: Refine content in site/speckit.html
T014: Refine content in site/devcontainers.html
T015: Refine content in site/codespaces.html
T016: Refine content in site/ghpages.html
```

---

## Implementation Strategy

### MVP First (User Story 1 Only)

1. Complete Phase 1: Add breadcrumb CSS (T001)
2. Complete Phase 3: Create all 7 concept pages + navigation section (T002–T009)
3. **STOP and VALIDATE**: All pages load, navigation works, back links work
4. This is a deployable MVP — the site has 7 concept pages accessible from the main page

### Incremental Delivery

1. Phase 1 → CSS ready
2. Phase 3 (US1) → 7 pages + navigation → **MVP deployed**
3. Phase 4 (US2) → Content quality verified/refined → **Full content quality**
4. Phase 5 (US3) → Visual consistency confirmed
5. Phase 6 → Polish complete

---

## Notes

- All tasks modify files in `site/` only: `index.html`, `style.css`, and 7 new `.html` files
- No automated tests — verification is manual browser testing
- Concept page template is defined in contracts/ui-contract.md (HTML boilerplate + content structure)
- Content per page is specified in contracts/ui-contract.md (Content Requirements per Page table)
- The existing copy-to-clipboard script in `index.html` is NOT modified or needed on concept pages
- Content tone: informal, friendly, second-person ("you") throughout
- Analogies per page are specified in contracts/ui-contract.md Analogy Theme column
