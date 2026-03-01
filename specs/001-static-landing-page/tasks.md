# Tasks: Static Landing Page

**Input**: Design documents from `/specs/001-static-landing-page/`
**Prerequisites**: plan.md (required), spec.md (required for user stories), research.md, data-model.md, contracts/

**Tests**: No tests requested — manual validation only (per quickstart.md checklist).

**Organization**: Tasks are grouped by user story to enable independent implementation and testing of each story.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (e.g., US1, US2, US3)
- Include exact file paths in descriptions

## Path Conventions

- **Static site**: `site/` at repository root
- `site/index.html` — page content and structure
- `site/style.css` — all styles (responsive, mobile-first)
- Inline `<script>` in index.html for copy-to-clipboard

---

## Phase 1: Setup

**Purpose**: Create the project directory and scaffold the HTML/CSS files with boilerplate

- [X] T001 Create `site/` directory and empty `site/index.html` and `site/style.css` files
- [X] T002 Add HTML5 boilerplate to `site/index.html` with `<meta charset>`, `<meta name="viewport" content="width=device-width, initial-scale=1">`, `<title>`, and `<link>` to `style.css` per ui-contract.md
- [X] T003 [P] Add CSS custom properties (`:root` variables for colors, fonts, spacing), minimal reset, and mobile-first base layout to `site/style.css` per research.md Topic 2 recommended outline
- [X] T004 Add semantic HTML skeleton to `site/index.html`: `<header>` with `<h1>`, `<main>` wrapping five empty `<section>` elements (`id="what-is-this"`, `id="concepts"`, `id="getting-started"`, `id="next-steps"`, `id="reference-links"`), each with an `<h2>` heading, and an optional `<footer>` per ui-contract.md

**Checkpoint**: Opening `site/index.html` in a browser shows a styled page skeleton with five section headings and no content yet.

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Responsive layout and link styling that ALL content sections depend on

**⚠️ CRITICAL**: Content sections will not render correctly without these base styles.

- [X] T005 Add responsive breakpoint styles (`@media (min-width: 768px)`) to `site/style.css` for centered content column (`max-width: 42rem`), larger headings, and generous spacing per research.md Topic 2
- [X] T006 [P] Add base typography and link styles to `site/style.css`: external link styling, `target="_blank"` visual indicator (optional), ordered list styling for Getting Started steps, heading styles for `h1`/`h2`/`h3`
- [X] T007 [P] Add `.code-block` container styles to `site/style.css`: positioned copy button (top-right), `<pre><code>` block styling with background color, padding, overflow-x scroll, and monospace font per ui-contract.md and research.md Topic 3

**Checkpoint**: Page skeleton is fully responsive (stacks on mobile, centered on desktop), links and code blocks are styled. Ready for content.

---

## Phase 3: User Story 1 — Understand What This Site Is (Priority: P1) 🎯 MVP

**Goal**: Visitor sees a "What is this?" section at the top of the page explaining the site's motivation and "learn by making" philosophy.

**Independent Test**: Open `site/index.html`, confirm the "What is this?" section appears first with plain-language motivational content in second-person voice ("you").

### Implementation for User Story 1

- [X] T008 [US1] Write content for `<section id="what-is-this">` in `site/index.html`: explain the site's purpose (practical guide for non-technical users to get started with AI-assisted development), frame the journey as ambitious but achievable, introduce GitHub Copilot as the AI assistant, emphasize "learn by making" philosophy. Use second-person voice per FR-002 and FR-016.

**Checkpoint**: "What is this?" section is complete and readable. Page delivers value as a motivational introduction even without the other sections.

---

## Phase 4: User Story 2 — Read About Key Concepts (Priority: P1)

**Goal**: Visitor reads plain-language introductions to GitHub Codespaces, GitHub Copilot/AI agents, and Spec-Driven Development/spec-kit, each with at least one external link.

**Independent Test**: Open `site/index.html`, scroll to "Key Concepts", confirm three concept entries each with a description and a working external link.

### Implementation for User Story 2

- [X] T009 [P] [US2] Add concept entry for GitHub Codespaces in `<section id="concepts">` of `site/index.html`: `<h3>` heading, plain-language description, external link to GitHub Codespaces docs (`https://docs.github.com/en/codespaces`) with `target="_blank" rel="noopener noreferrer"` per FR-003, FR-004, FR-015
- [X] T010 [P] [US2] Add concept entry for GitHub Copilot & AI Agents in `<section id="concepts">` of `site/index.html`: `<h3>` heading, plain-language description, external link to GitHub Copilot docs (`https://docs.github.com/en/copilot`) with `target="_blank" rel="noopener noreferrer"`
- [X] T011 [P] [US2] Add concept entry for Spec-Driven Development & spec-kit in `<section id="concepts">` of `site/index.html`: `<h3>` heading, plain-language description, external link to spec-kit repo (`https://github.com/github/spec-kit`) with `target="_blank" rel="noopener noreferrer"`

**Checkpoint**: "Key Concepts" section has three entries, each with description and working link. All links open in new tabs.

---

## Phase 5: User Story 3 — Follow Getting Started Steps (Priority: P1)

**Goal**: Visitor follows a 5-step numbered walkthrough from zero (no GitHub account) to a working Codespace with the project open.

**Independent Test**: Open `site/index.html`, scroll to "Getting Started", confirm 5 numbered steps with explanations. Click links in steps 1 and 2 to verify they open the correct pages.

### Implementation for User Story 3

- [X] T012 [US3] Write the 5-step Getting Started ordered list (`<ol>`) in `<section id="getting-started">` of `site/index.html` per FR-005, FR-006, FR-007: (1) Create a GitHub account — link to `https://github.com/signup`, explain what GitHub is; (2) Sign up for Copilot Pro free trial — link to `https://github.com/github-copilot/signup`, explain what Copilot provides; (3) Contact the project owner — explain why (private repo, need collaborator access to fork), keep contact method vague per spec assumptions; (4) Fork the repository — explain what "forking" means in plain language, describe how to do it; (5) Open your fork in GitHub Codespaces — explain what a Codespace is and how to launch one. Each step uses second-person voice. All links have `target="_blank" rel="noopener noreferrer"`.

**Checkpoint**: "Getting Started" section is a complete, self-contained 5-step guide. A novice can follow it end-to-end.

---

## Phase 6: User Story 4 — Read Next Steps Suggestion (Priority: P2)

**Goal**: Visitor reads a suggested first feature (multi-page "Concepts" section), finds a ready-to-copy `/speckit.specify` command prompt, and sees a reminder about "ask" mode.

**Independent Test**: Open `site/index.html`, scroll to "Next Steps", confirm feature suggestion with topic list, copy button works on the command prompt, and ask-mode reminder is visible.

### Implementation for User Story 4

- [X] T013 [US4] Write introductory content for `<section id="next-steps">` in `site/index.html`: describe the suggested feature idea (expand site to multi-page with individual concept/topic pages), list example topics (Git & version control, GitHub, GitHub Copilot & AI agents, SDD & spec-kit, Devcontainers, GitHub Codespaces, GitHub Pages), mention using `/speckit.specify`, `/speckit.plan`, `/speckit.tasks`, `/speckit.implement` commands per FR-008, FR-009
- [X] T014 [US4] Add the ready-to-copy `/speckit.specify` command prompt block in `<section id="next-steps">` of `site/index.html` using the `.code-block` pattern from ui-contract.md: `<div class="code-block">` with `<button class="copy-btn">` and `<pre><code>` containing a complete, well-crafted `/speckit.specify` prompt for the Concepts pages feature per FR-010
- [X] T015 [US4] Add inline `<script>` at the bottom of `<body>` in `site/index.html` implementing copy-to-clipboard: attach click handler to `.copy-btn`, use `navigator.clipboard.writeText()`, show "Copied!" feedback for 2 seconds per research.md Topic 3
- [X] T016 [US4] Add ask-mode reminder paragraph in `<section id="next-steps">` of `site/index.html`: remind the visitor they can switch their AI agent to "ask" mode at any time to ask about anything they don't understand per FR-011

**Checkpoint**: "Next Steps" section is complete. Copy button works. Ask-mode reminder is visible. The `/speckit.specify` prompt is ready to copy and paste.

---

## Phase 7: User Story 5 — Browse Reference Links (Priority: P3)

**Goal**: Visitor finds a consolidated list of at least 5 key external links at the bottom of the page.

**Independent Test**: Open `site/index.html`, scroll to "Reference Links", confirm at least 5 labeled links that open in new tabs and resolve to valid pages.

### Implementation for User Story 5

- [X] T017 [US5] Add reference links list in `<section id="reference-links">` of `site/index.html`: at least 5 labeled external links covering GitHub (`https://github.com`), GitHub Copilot (`https://github.com/features/copilot`), GitHub Codespaces (`https://github.com/features/codespaces`), spec-kit (`https://github.com/github/spec-kit`), and SDD methodology. All links have `target="_blank" rel="noopener noreferrer"` per FR-012, FR-015.

**Checkpoint**: "Reference Links" section complete. All links work and open in new tabs.

---

## Phase 8: Polish & Cross-Cutting Concerns

**Purpose**: Final validation and refinements across all sections

- [X] T018 [P] Review all visitor-facing text in `site/index.html` for consistent second-person voice ("you") per FR-016 — fix any third-person references
- [X] T019 [P] Verify all external links in `site/index.html` resolve to valid pages (no 404s) per SC-004 — update any broken URLs
- [X] T020 [P] Test responsive layout of `site/index.html` at 375px viewport width per SC-005 — fix any horizontal scrolling or overflow issues in `site/style.css`
- [X] T021 Verify `site/index.html` loads correctly via `file://` protocol (no server) in at least two browsers per SC-003
- [X] T022 Run quickstart.md validation checklist — confirm all items pass
- [X] T023 Verify heading hierarchy in `site/index.html` is sequential (h1 → h2 → h3, no skipped levels) per ui-contract.md accessibility baseline

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: No dependencies — start immediately
- **Foundational (Phase 2)**: Depends on T001–T004 (Setup) — BLOCKS all user story content
- **User Story 1 (Phase 3)**: Depends on Phase 2 — can start after foundational styles are in place
- **User Story 2 (Phase 4)**: Depends on Phase 2 — independent of US1, can run in parallel
- **User Story 3 (Phase 5)**: Depends on Phase 2 — independent of US1/US2, can run in parallel
- **User Story 4 (Phase 6)**: Depends on Phase 2 + T007 (code-block styles) — independent of US1/US2/US3
- **User Story 5 (Phase 7)**: Depends on Phase 2 — independent of all other stories
- **Polish (Phase 8)**: Depends on ALL user story phases being complete

### User Story Dependencies

- **User Story 1 (P1)**: No dependencies on other stories
- **User Story 2 (P1)**: No dependencies on other stories
- **User Story 3 (P1)**: No dependencies on other stories
- **User Story 4 (P2)**: No dependencies on other stories (code-block styles from Phase 2 are sufficient)
- **User Story 5 (P3)**: No dependencies on other stories

### Within Each User Story

- All [P]-marked tasks within a story can run in parallel
- Content tasks within a single HTML file must be applied sequentially (same file) unless modifying distinct `<section>` elements
- In practice, since all content goes into `site/index.html`, the agent should add sections in page order

### Parallel Opportunities

- T003 (CSS variables/reset) can run in parallel with T002/T004 (HTML boilerplate/skeleton) — different files
- T005, T006, T007 (foundational CSS tasks) are all [P] within `site/style.css` — can be parallelized if editing distinct CSS sections
- T009, T010, T011 (concept entries) are all [P] — different `<h3>` subsections within `#concepts`
- T018, T019, T020, T023 (polish tasks) are all [P] — independent validation passes

---

## Parallel Example: User Story 2

```text
# All three concept entries can be written in parallel
# (they are independent subsections within #concepts):
Task T009: "Add GitHub Codespaces concept entry"
Task T010: "Add GitHub Copilot concept entry"
Task T011: "Add SDD & spec-kit concept entry"
```

---

## Implementation Strategy

### MVP First (User Stories 1 + 2 + 3)

1. Complete Phase 1: Setup (T001–T004)
2. Complete Phase 2: Foundational CSS (T005–T007)
3. Complete Phase 3: US1 — "What is this?" section (T008)
4. Complete Phase 4: US2 — Key Concepts (T009–T011)
5. Complete Phase 5: US3 — Getting Started (T012)
6. **STOP and VALIDATE**: The page is a functional MVP — a visitor can understand the site, learn the key concepts, and follow the Getting Started steps.

### Incremental Delivery

1. Setup + Foundational → Page skeleton ready
2. Add US1 → Motivation section live
3. Add US2 → Concepts section live
4. Add US3 → Getting Started guide live → **MVP!**
5. Add US4 → Next Steps with copy-paste prompt live
6. Add US5 → Reference Links live
7. Polish → All validation checks pass → **Feature complete**

### Single-Developer Strategy (Recommended)

Since this is a single HTML page with one developer:
1. Complete Setup + Foundational sequentially
2. Add content sections in page order (US1 → US2 → US3 → US4 → US5)
3. Polish pass at the end
4. Total: 23 tasks, estimated single-sitting implementation

---

## Notes

- [P] tasks = different files or distinct sections, no dependencies
- [Story] label maps task to specific user story for traceability
- All content goes into `site/index.html` — tasks are organized by section but edit the same file
- No test tasks included — validation is manual per quickstart.md
- Commit after each phase or logical group
- Stop at any checkpoint to validate independently
