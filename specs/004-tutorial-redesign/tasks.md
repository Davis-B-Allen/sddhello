# Tasks: Tutorial Site Redesign — Step-by-Step Copilot-Assisted Format

**Input**: Design documents from `/specs/004-tutorial-redesign/`
**Prerequisites**: plan.md, spec.md, research.md, data-model.md, contracts/ui-contract.md, quickstart.md

**Tests**: No automated tests requested. Verification is manual browser testing per quickstart.md.

**Organization**: Tasks are grouped by user story. Since all stories modify the same HTML file, they must execute sequentially in priority order. CSS work is parallelizable with early HTML tasks.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (e.g., US1, US2, US3)
- Include exact file paths in descriptions

## Path Conventions

- Static site files: `site/index.html`, `site/style.css`
- No other source files are created or modified

---

## Phase 1: Setup

**Purpose**: Add CSS rules needed by subsequent phases before modifying HTML

- [X] T001 [P] Add `.objectives`, `.objectives-heading`, `.keywords` CSS rules to `site/style.css` per the New CSS Rules Required section in contracts/ui-contract.md

---

## Phase 2: Foundational — Remove old sections (Blocking Prerequisites)

**Purpose**: Remove obsolete `#concepts` and `#getting-started` sections from `site/index.html` to clear the way for new step sections

**⚠️ CRITICAL**: New step sections cannot be inserted until old wrapper sections are removed

- [X] T002 Delete the entire `<section id="concepts">` block (Key Concepts) from `site/index.html`
- [X] T003 Delete the entire `<section id="getting-started">` block (Getting Started) from `site/index.html`, preserving the substantive content from each `<li>` for reuse in subsequent tasks

**Checkpoint**: Page loads with no "Key Concepts" and no "Getting Started" sections. Only `#what-is-this`, `#next-steps`, and `#reference-links` remain.

---

## Phase 3: User Story 1 — Restructure into individual step sections (Priority: P1) 🎯 MVP

**Goal**: Insert seven `<section>` elements (`#step-1` through `#step-7`) between `#what-is-this` and `#next-steps` in `site/index.html`, each with its own `<h2>` heading. Content for each step is adapted from the original Getting Started list items, with the new Step 3 as a placeholder to be fleshed out in Phase 4.

**Independent Test**: Load the page. Confirm seven step sections appear with correct titles ("Step 1: Create a GitHub account" through "Step 7: Publish your site with GitHub Pages"), no "Key Concepts" section, and no "Getting Started" wrapper.

### Implementation for User Story 1

- [X] T004 [US1] Insert `<section id="step-1">` with `<h2>Step 1: Create a GitHub account</h2>` and adapted content from original list item 1 (brief GitHub explanation + signup link) in `site/index.html`, placed after `</section><!-- end what-is-this -->`
- [X] T005 [US1] Insert `<section id="step-2">` with `<h2>Step 2: Sign up for the GitHub Copilot Pro free trial</h2>` and adapted content from original list item 2 (Copilot Pro explanation + signup link) in `site/index.html`, placed after `#step-1`
- [X] T006 [US1] Insert `<section id="step-3">` with `<h2>Step 3: Meet your AI assistant</h2>` and placeholder paragraph in `site/index.html`, placed after `#step-2` (full content added in Phase 4)
- [X] T007 [US1] Insert `<section id="step-4">` with `<h2>Step 4: Fork the repository</h2>` and adapted content from original list item 3 (forking explanation + repo link) in `site/index.html`, placed after `#step-3`
- [X] T008 [US1] Insert `<section id="step-5">` with `<h2>Step 5: Open your fork in GitHub Codespaces</h2>` and adapted content from original list item 4 (Codespaces explanation) in `site/index.html`, placed after `#step-4`
- [X] T009 [US1] Insert `<section id="step-6">` with `<h2>Step 6: Preview the site locally</h2>` and adapted content from original list item 5 (terminal + npx serve instructions) in `site/index.html`, placed after `#step-5`
- [X] T010 [US1] Insert `<section id="step-7">` with `<h2>Step 7: Publish your site with GitHub Pages</h2>` and adapted content from original list item 6 (GitHub Pages + Actions instructions) in `site/index.html`, placed after `#step-6`
- [X] T011 [US1] Remove the CSS rule `#getting-started > ol > li > strong` from `site/style.css` since the `#getting-started` section no longer exists

**Checkpoint**: All seven step sections render with correct headings and adapted content. Page structure matches data-model.md section ordering.

---

## Phase 4: User Story 2 — Step 3 Copilot onboarding content (Priority: P1)

**Goal**: Replace the Step 3 placeholder with full onboarding content: explain Copilot, link to github.com/copilot, explain Ask Mode, introduce the repo-linking pattern, and add the verification prompt block with follow-up confirmation text.

**Independent Test**: Load the page and read Step 3. Confirm it explains Copilot, links to github.com/copilot, explains Ask Mode, contains a copy-enabled prompt block with the specified verification text, and has follow-up confirmation text. Confirm NO Objectives block is present.

### Implementation for User Story 2

- [X] T012 [US2] Replace Step 3 placeholder content in `site/index.html` with full onboarding text: beginner-friendly explanation of GitHub Copilot, instructions to navigate to github.com/copilot, explanation of Ask Mode, and introduction of the repo-linking interaction pattern per FR-008 through FR-012
- [X] T013 [US2] Add the verification Copilot prompt `code-block` to Step 3 in `site/index.html` with the exact prompt text from contracts/ui-contract.md Template B, using the existing `.code-block` / `.copy-btn` markup pattern per FR-013
- [X] T014 [US2] Add follow-up confirmation paragraph after the Step 3 prompt block: "If your Copilot assistant confirmed that the next step is 'Step 4: Fork the repository', you're ready to move on. And your Copilot is ready to help you!" per FR-014

**Checkpoint**: Step 3 is complete with onboarding content and a working copy-enabled prompt block. No Objectives block present.

---

## Phase 5: User Story 3 — Objectives blocks and Copilot prompts for Steps 4–7 (Priority: P1)

**Goal**: Add an Objectives `<aside>` block and a Copilot prompt `code-block` to each of Steps 4, 5, 6, and 7. Ensure walkthrough content is in a friendly, colloquial tone. Introduce key concepts inline (forking, Codespaces, GitHub Pages, etc.) rather than referencing a separate section.

**Independent Test**: For each of Steps 4–7, verify: (a) Objectives block with ≥2 goals and ≥2 keywords, (b) copy-enabled prompt block with correct step number, (c) walkthrough text in friendly tone, (d) concepts introduced inline.

### Implementation for User Story 3

- [X] T015 [US3] Add Objectives block `<aside class="objectives">` to top of `#step-4` in `site/index.html` with goals (create personal copy, understand forking) and keywords (repository, fork, GitHub, personal copy, upstream) per contracts/ui-contract.md
- [X] T016 [US3] Add colloquial intro paragraph and Copilot prompt instruction + `code-block` with step 4 prompt text to `#step-4` in `site/index.html`, placed after the Objectives block and before the walkthrough content per FR-018 through FR-020
- [X] T017 [US3] Rewrite `#step-4` walkthrough content in `site/index.html` in colloquial tone, introducing "forking" and "repository" concepts inline per FR-023 and FR-024
- [X] T018 [US3] Add Objectives block `<aside class="objectives">` to top of `#step-5` in `site/index.html` with goals (launch cloud dev environment, get familiar with VS Code in browser) and keywords (Codespaces, cloud development environment, VS Code, browser IDE, devcontainer) per contracts/ui-contract.md
- [X] T019 [US3] Add colloquial intro paragraph and Copilot prompt instruction + `code-block` with step 5 prompt text to `#step-5` in `site/index.html`, placed after the Objectives block and before the walkthrough content per FR-018 through FR-020
- [X] T020 [US3] Rewrite `#step-5` walkthrough content in `site/index.html` in colloquial tone, introducing "Codespaces" and "cloud development environment" concepts inline per FR-023 and FR-024
- [X] T021 [US3] Add Objectives block `<aside class="objectives">` to top of `#step-6` in `site/index.html` with goals (run local web server, understand terminal and preview tools) and keywords (terminal, local server, npx serve, port forwarding, preview) per contracts/ui-contract.md
- [X] T022 [US3] Add colloquial intro paragraph and Copilot prompt instruction + `code-block` with step 6 prompt text to `#step-6` in `site/index.html`, placed after the Objectives block and before the walkthrough content per FR-018 through FR-020
- [X] T023 [US3] Rewrite `#step-6` walkthrough content in `site/index.html` in colloquial tone, introducing "terminal" and "local server" concepts inline per FR-023 and FR-024
- [X] T024 [US3] Add Objectives block `<aside class="objectives">` to top of `#step-7` in `site/index.html` with goals (enable GitHub Pages, deploy to public URL, understand GitHub Actions) and keywords (GitHub Pages, deployment, GitHub Actions, workflow, static hosting, public URL) per contracts/ui-contract.md
- [X] T025 [US3] Add colloquial intro paragraph and Copilot prompt instruction + `code-block` with step 7 prompt text to `#step-7` in `site/index.html`, placed after the Objectives block and before the walkthrough content per FR-018 through FR-020
- [X] T026 [US3] Rewrite `#step-7` walkthrough content in `site/index.html` in colloquial tone, introducing "GitHub Pages" and "GitHub Actions" concepts inline per FR-023 and FR-024

**Checkpoint**: Steps 4–7 each have an Objectives block with goals and keywords, a copy-enabled prompt block, and colloquial walkthrough text with inline concept introductions.

---

## Phase 6: User Story 4 — Preserve existing content and verify (Priority: P2)

**Goal**: Verify that sections outside the redesign scope are unchanged and all copy buttons work.

**Independent Test**: Load page. Confirm "What is this?" text is identical to original. Confirm "Next Steps" and "Reference Links" are unchanged. Click every Copy button — all should work.

### Implementation for User Story 4

- [X] T027 [US4] Verify `#what-is-this` section content in `site/index.html` is unchanged from the original (no edits should have touched it — this is a manual/diff check)
- [X] T028 [US4] Verify `#next-steps` and `#reference-links` sections in `site/index.html` are unchanged from the original
- [X] T029 [US4] Verify all `.copy-btn` buttons work on the page (Steps 3–7 prompt blocks + Next Steps block) by testing in browser
- [X] T030 [US4] Verify the page renders correctly at 375px width (responsive check in browser dev tools)

**Checkpoint**: All out-of-scope content preserved. All copy buttons functional. Responsive layout intact.

---

## Phase 7: Polish & Cross-Cutting Concerns

**Purpose**: Final validation and cleanup

- [X] T031 Run `npx serve site -p 8080` and perform full walkthrough verification per quickstart.md checklist
- [X] T032 Validate HTML structure matches data-model.md section ordering (10 sections, correct IDs, correct types)
- [X] T033 Validate all 7 step headings match FR-004 exact titles

---

## Dependencies & Execution Order

### Phase Dependencies

- **Phase 1 (Setup/CSS)**: No dependencies — can start immediately
- **Phase 2 (Remove old sections)**: No dependency on Phase 1 (different file), but logically should happen after CSS is ready
- **Phase 3 (US1 — Restructure)**: Depends on Phase 2 (old sections must be removed first)
- **Phase 4 (US2 — Step 3 content)**: Depends on Phase 3 (Step 3 section must exist)
- **Phase 5 (US3 — Steps 4–7 enhancements)**: Depends on Phase 3 (step sections must exist)
- **Phase 6 (US4 — Verification)**: Depends on Phases 3, 4, 5 (all content changes complete)
- **Phase 7 (Polish)**: Depends on Phase 6

### User Story Dependencies

- **US1 (Restructure)**: Foundational — all other stories depend on this
- **US2 (Step 3)**: Depends on US1 (needs Step 3 section to exist)
- **US3 (Steps 4–7)**: Depends on US1 (needs step sections to exist). Independent of US2.
- **US4 (Verification)**: Depends on US1, US2, US3 all being complete

### Parallel Opportunities

- **T001** (CSS) can run in parallel with **T002–T003** (removing old HTML sections) since they touch different files
- **Phase 4 (US2)** and **Phase 5 (US3)** can start concurrently after Phase 3, since US2 edits `#step-3` while US3 edits `#step-4` through `#step-7` (different sections of the same file)
- Within Phase 5, Steps 4–7 are conceptually independent, but since they modify the same file, tasks within each step should be done sequentially

---

## Parallel Example: Phase 1 + Phase 2

```text
# These can run simultaneously (different files):
T001: Add .objectives CSS rules to site/style.css
T002: Delete #concepts section from site/index.html
T003: Delete #getting-started section from site/index.html
```

## Parallel Example: Phase 4 + Phase 5

```text
# After Phase 3 is complete, these can start concurrently (different sections):
T012–T014: Step 3 onboarding content (US2)
T015–T017: Step 4 objectives + prompt + walkthrough (US3)
```

---

## Implementation Strategy

### MVP First (User Story 1 Only)

1. Complete Phase 1: CSS setup (T001)
2. Complete Phase 2: Remove old sections (T002–T003)
3. Complete Phase 3: User Story 1 — all 7 step sections with adapted content (T004–T011)
4. **STOP and VALIDATE**: Page has 7 step sections, no Key Concepts, no Getting Started wrapper
5. This is a deployable MVP — the page structure is correct even without Objectives blocks

### Incremental Delivery

1. Phase 1 + Phase 2 → Old sections removed, CSS ready
2. Phase 3 (US1) → 7 step sections with content → **MVP deployed**
3. Phase 4 (US2) → Step 3 has full onboarding content
4. Phase 5 (US3) → Steps 4–7 have Objectives blocks and prompt blocks → **Full feature**
5. Phase 6 (US4) → All verifications pass
6. Phase 7 → Polish complete

---

## Notes

- All tasks modify only 2 files: `site/index.html` and `site/style.css`
- No automated tests — verification is manual browser testing
- The existing copy-to-clipboard `<script>` block is NOT modified
- New `.code-block` elements automatically get copy functionality from the existing script
- Content tone: informal, friendly, second-person ("you") throughout Steps 3–7
- Concepts are introduced inline, NOT in a separate section
