# Tasks: Site & README Updates for Public Repo + GitHub Pages

**Input**: Design documents from `/specs/002-site-readme-ghpages/`
**Prerequisites**: plan.md, spec.md, research.md, data-model.md, contracts/ui-contract.md, quickstart.md

**Tests**: Not requested — no test tasks included.

**Organization**: Tasks are grouped by user story. US1, US2, and US4 all modify the same file (`site/index.html` Getting Started section) and are sequenced within a single phase. US3 (Actions workflow) is independent and parallelizable. US5 (README) depends on finalized site content.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (e.g., US1, US2, US3)
- Include exact file paths in descriptions

---

## Phase 1: Setup

**Purpose**: Infrastructure changes that don't depend on content — devcontainer and deployment workflow

- [ ] T001 [P] Add forwardPorts configuration for port 8080 in .devcontainer/devcontainer.json
- [ ] T002 [P] Create GitHub Actions Pages deployment workflow in .github/workflows/deploy-pages.yml

**Checkpoint**: Devcontainer forwards port 8080; deployment workflow is ready to deploy `site/` on push to `main`.

---

## Phase 2: User Story 1 — Visitor Forks a Public Repository (Priority: P1) 🎯 MVP

**Goal**: Remove the access-request step (old step 3) and update the fork step to link directly to the public repository.

**Independent Test**: Open `site/index.html` in a browser. Verify Getting Started has no step mentioning requesting access or being added as a collaborator. Verify the fork step includes a direct link to the public repository.

### Implementation for User Story 1

- [ ] T003 [US1] Remove the "Contact the project owner for repository access" step (old step 3) from the Getting Started `<ol>` in site/index.html
- [ ] T004 [US1] Update the fork step to link directly to the public repository and remove the reference to "Once you've been added as a collaborator (step 3)" in site/index.html
- [ ] T005 [US1] Update the introductory paragraph in the Getting Started section to reflect the new step count in site/index.html

**Checkpoint**: Getting Started section no longer mentions requesting access. Fork step links directly to the public repo. Steps are renumbered (1–4 so far).

---

## Phase 3: User Story 2 — Contributor Previews the Site Locally (Priority: P1)

**Goal**: Add a Getting Started step that explains how to serve the site locally with `npx serve` and view it via Codespaces port forwarding.

**Independent Test**: Open the project in a Codespace. Follow the new local preview step. Run `npx serve site -p 8080`. Verify the site loads via the forwarded port.

### Implementation for User Story 2

- [ ] T006 [US2] Add a new "Preview the site locally" step to the Getting Started `<ol>` in site/index.html with the `npx serve site -p 8080` command, Codespaces port-forwarding instructions, and a local-development aside

**Checkpoint**: Getting Started now has 5 steps (1–5). Step 5 explains local preview with explicit command and Codespaces instructions.

---

## Phase 4: User Story 4 — Getting Started Explains GitHub Pages Publishing (Priority: P2)

**Goal**: Add a Getting Started step that explains how to enable GitHub Pages on a forked repository.

**Independent Test**: Read the new step. Verify it covers: enabling Actions on the fork, setting Pages source to GitHub Actions, the expected URL format.

### Implementation for User Story 4

- [ ] T007 [US4] Add a new "Publish your site with GitHub Pages" step to the Getting Started `<ol>` in site/index.html with instructions for enabling Actions, configuring Pages source, and the expected URL format

**Checkpoint**: Getting Started now has 6 steps (1–6), matching the UI contract. All site content changes are complete.

---

## Phase 5: User Story 3 — Site Published via GitHub Pages (Priority: P1)

**Goal**: Validate that the GitHub Actions workflow (created in T002) correctly deploys `site/` to GitHub Pages.

**Independent Test**: Push a change to `main`. Verify the Actions tab shows the workflow running. Verify the site is live at the GitHub Pages URL.

### Implementation for User Story 3

> Note: The workflow file was already created in T002 (Setup phase). This phase validates it against the contract and makes any adjustments.

- [ ] T008 [US3] Verify deploy-pages.yml matches the workflow contract in contracts/ui-contract.md (permissions, concurrency, path, environment, actions versions)

**Checkpoint**: Workflow is validated and ready. Deployment will occur automatically when changes are merged to `main`.

---

## Phase 6: User Story 5 — README Reflects the Site Content (Priority: P2)

**Goal**: Rewrite README.md to mirror the site content — project description, key concepts, Getting Started steps (same 6 steps), link to live site, reference links.

**Independent Test**: Visit the repository page on GitHub. Verify the README describes the project, includes consistent Getting Started steps, links to the live site, and contains no brainstorming notes.

### Implementation for User Story 5

- [ ] T009 [US5] Rewrite README.md with project title, description, live site link, What is this section, Key Concepts section, Getting Started section (same 6 steps as site), Next Steps, and Reference Links per contracts/ui-contract.md README Contract

**Checkpoint**: README mirrors site content. No brainstorming notes remain. Getting Started steps match the site.

---

## Phase 7: Polish & Cross-Cutting Concerns

**Purpose**: Final validation across all files

- [ ] T010 Verify site/index.html Getting Started steps match README.md Getting Started steps (same count, same order, consistent content)
- [ ] T011 Run quickstart.md validation: serve site locally with `npx serve site -p 8080` and verify all 6 Getting Started steps render correctly in the browser
- [ ] T012 Verify all external links in site/index.html use target="_blank" rel="noopener noreferrer"

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: No dependencies — T001 and T002 can start immediately and run in parallel
- **US1 (Phase 2)**: No dependencies on Phase 1 — can start immediately (but sequential after Phase 1 for clean ordering)
- **US2 (Phase 3)**: Depends on US1 (Phase 2) — both modify the same `<ol>` in site/index.html
- **US4 (Phase 4)**: Depends on US2 (Phase 3) — appends to the same `<ol>` in site/index.html
- **US3 (Phase 5)**: Depends on Phase 1 (T002 creates the workflow file)
- **US5 (Phase 6)**: Depends on Phases 2–4 (site content must be finalized before README mirrors it)
- **Polish (Phase 7)**: Depends on all prior phases

### User Story Dependencies

- **US1 (P1)**: Independent — can start after setup
- **US2 (P1)**: Depends on US1 completion (same file, same section)
- **US3 (P1)**: Independent of content changes — only depends on T002 existing
- **US4 (P2)**: Depends on US2 completion (same file, same section)
- **US5 (P2)**: Depends on US1 + US2 + US4 (mirrors finalized site content)

### Parallel Opportunities

- T001 and T002 can run in parallel (different files: devcontainer.json vs deploy-pages.yml)
- T008 (US3 validation) can run in parallel with Phases 2–4 (different file)
- Polish tasks T010, T011, T012 can run in parallel with each other

---

## Parallel Example: Setup Phase

```bash
# Launch both setup tasks together (different files):
Task T001: "Add forwardPorts in .devcontainer/devcontainer.json"
Task T002: "Create deploy-pages.yml in .github/workflows/"
```

## Parallel Example: Polish Phase

```bash
# Launch all polish tasks together:
Task T010: "Verify site/README consistency"
Task T011: "Run quickstart.md validation"
Task T012: "Verify external link attributes"
```

---

## Implementation Strategy

### MVP First (User Story 1 Only)

1. Complete Phase 1: Setup (T001, T002)
2. Complete Phase 2: US1 — Remove access step, update fork link (T003–T005)
3. **STOP and VALIDATE**: Open site in browser, verify no access-request step, fork link works
4. This alone delivers value — visitors can now fork without friction

### Incremental Delivery

1. Setup (T001–T002) → Infrastructure ready
2. US1 (T003–T005) → Public repo forking works (MVP!)
3. US2 (T006) → Local preview documented
4. US4 (T007) → GitHub Pages documented in Getting Started
5. US3 (T008) → Workflow validated
6. US5 (T009) → README mirrors site
7. Polish (T010–T012) → Cross-cutting validation
8. Each phase adds value without breaking previous work

---

## Notes

- T001 and T002 are independent and parallelizable (different files)
- T003–T007 are sequential because they all edit the same `<ol>` in site/index.html
- T009 (README) must come after all site/index.html changes are finalized
- No tests were requested — validation is manual per quickstart.md
- Total tasks: 12
- Commit after each phase or logical group
