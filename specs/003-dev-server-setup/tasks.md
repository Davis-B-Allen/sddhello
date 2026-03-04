# Tasks: Dev Server Setup with Live Reload

**Input**: Design documents from `/specs/003-dev-server-setup/`
**Prerequisites**: plan.md (required), spec.md (required for user stories), research.md, data-model.md, contracts/

**Tests**: Not requested — no test tasks included.

**Organization**: Tasks are grouped by user story to enable independent implementation and testing of each story.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (e.g., US1, US2, US3)
- Include exact file paths in descriptions

---

## Phase 1: Setup

**Purpose**: No project scaffolding needed — this feature modifies an existing config file. Phase is empty.

*(No tasks — the project structure already exists.)*

---

## Phase 2: Foundational (Pre-Installed Tooling — US3)

**Purpose**: Ensure browser-sync is pre-installed in the devcontainer so that all user stories can function. This maps to User Story 3 (Pre-Installed Tooling in Devcontainer, P1), which is the foundational prerequisite for Stories 1 and 2.

**⚠️ CRITICAL**: The dev server cannot launch (US1) or live-reload (US2) unless the tool is pre-installed (US3). This phase MUST complete first.

- [x] T001 Add `postCreateCommand` to install browser-sync globally in .devcontainer/devcontainer.json
- [x] T002 Verify browser-sync is available on PATH after devcontainer rebuild (run `which browser-sync` and `browser-sync --version`)

**Checkpoint**: After rebuilding the devcontainer, `browser-sync` should be globally available without any manual install steps. Satisfies US3 acceptance scenarios.

---

## Phase 3: User Story 1 — Zero-Setup Dev Server Launch (Priority: P1) 🎯 MVP

**Goal**: A developer runs a single command and the site is served on port 8080 — no install prompts, no errors.

**Independent Test**: Open a fresh devcontainer, run the browser-sync command, verify site is accessible at `http://localhost:8080` with clean output.

### Implementation for User Story 1

- [x] T003 [US1] Run `browser-sync start --server site --port 8080 --no-open --no-notify --no-ui --watch` and verify site serves correctly on port 8080
- [x] T004 [US1] Verify no error messages or install prompts appear in server output
- [x] T005 [US1] Verify site content from site/index.html is displayed when accessing http://localhost:8080 in browser

**Checkpoint**: User Story 1 is fully functional — site serves instantly with clean output. This is the MVP.

---

## Phase 4: User Story 2 — Live Reload During Development (Priority: P1)

**Goal**: Changes to HTML/CSS files in `site/` are automatically reflected in the browser without manual refresh.

**Independent Test**: Start the dev server, open the site in a browser, edit `site/style.css` or `site/index.html`, save, and observe automatic browser refresh.

### Implementation for User Story 2

- [x] T006 [US2] Verify live reload works: edit site/style.css while server is running and confirm browser updates automatically
- [x] T007 [US2] Verify live reload works: edit site/index.html while server is running and confirm browser updates automatically
- [x] T008 [US2] Verify new files added to site/ are accessible via the dev server without restart

**Checkpoint**: User Stories 1 AND 2 are both working — site serves and live-reloads on file changes.

---

## Phase 5: Polish & Cross-Cutting Concerns

**Purpose**: Documentation and discoverability improvements

- [x] T009 [P] Update README.md to document the dev server command and development workflow
- [x] T010 Run quickstart.md validation — verify all steps in specs/003-dev-server-setup/quickstart.md work as documented

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: Empty — no setup needed
- **Foundational (Phase 2)**: No dependencies — can start immediately. BLOCKS all user stories.
- **User Story 1 (Phase 3)**: Depends on Phase 2 completion (browser-sync must be installed)
- **User Story 2 (Phase 4)**: Depends on Phase 2 completion (browser-sync must be installed). Can run in parallel with Phase 3 since it uses the same command.
- **Polish (Phase 5)**: Depends on Phases 3 and 4 being verified

### User Story Dependencies

- **User Story 3 (Pre-Installed Tooling)**: Foundational — Phase 2. No dependencies on other stories.
- **User Story 1 (Zero-Setup Launch)**: Depends on US3 (tooling must be pre-installed). No dependency on US2.
- **User Story 2 (Live Reload)**: Depends on US3 (tooling must be pre-installed). No dependency on US1.

### Within Each User Story

- US3 (Phase 2): Config change → Rebuild → Verify
- US1 (Phase 3): Run command → Verify output → Verify browser access
- US2 (Phase 4): Run command → Edit file → Verify auto-refresh

### Parallel Opportunities

- T003, T004, T005 (US1 verification steps) are sequential (each depends on the server running)
- T006, T007, T008 (US2 verification steps) are sequential (each depends on the server running)
- T009 (README update) can run in parallel with any verification phase
- US1 (Phase 3) and US2 (Phase 4) can run in parallel — they use the same server instance

---

## Parallel Example: Phases 3 & 4

```text
# After Phase 2 completes (browser-sync installed), start the dev server once:
browser-sync start --server site --port 8080 --no-open --no-notify --no-ui --watch

# Then verify BOTH user stories against the running server:
# US1: Verify clean startup, no errors, site accessible on port 8080
# US2: Edit site/style.css, verify auto-refresh; edit site/index.html, verify auto-refresh

# In parallel, update documentation:
# T009: Update README.md with dev server command
```

---

## Implementation Strategy

### MVP First (User Story 3 + User Story 1)

1. Complete Phase 2: Add `postCreateCommand` to devcontainer.json (T001)
2. Rebuild devcontainer to apply changes (T002)
3. Complete Phase 3: Verify zero-setup serve works (T003–T005)
4. **STOP and VALIDATE**: Site serves on port 8080 with no prompts or errors
5. This is the MVP — immediate value delivered

### Incremental Delivery

1. T001–T002 → Tooling pre-installed (US3 complete)
2. T003–T005 → Zero-setup launch verified (US1 complete) → **MVP!**
3. T006–T008 → Live reload verified (US2 complete) → Full feature
4. T009–T010 → Documentation updated → Polish complete

---

## Notes

- This is a minimal-change feature: only `.devcontainer/devcontainer.json` is modified (1 line added)
- US1 and US2 verification tasks (Phases 3–4) are validation steps, not code changes — they confirm browser-sync's built-in behavior works as expected in the devcontainer environment
- The README update (T009) is the only other file change
- No `package.json` is introduced — keeping project structure simple per constitution
- After T001, the devcontainer must be rebuilt for changes to take effect (T002 captures this)
