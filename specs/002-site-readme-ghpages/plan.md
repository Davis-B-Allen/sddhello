# Implementation Plan: Site & README Updates for Public Repo + GitHub Pages

**Branch**: `002-site-readme-ghpages` | **Date**: 2026-03-01 | **Spec**: [spec.md](spec.md)
**Input**: Feature specification from `/specs/002-site-readme-ghpages/spec.md`

**Note**: This template is filled in by the `/speckit.plan` command. See `.specify/templates/plan-template.md` for the execution workflow.

## Summary

Update the static site and README for a now-public repository: remove the access-request step from Getting Started, add local preview instructions (with `npx serve` and Codespaces port forwarding), deploy the `site/` folder to GitHub Pages via a GitHub Actions workflow, document GitHub Pages setup for forks, and rewrite the root README to mirror the site content.

## Technical Context

**Language/Version**: HTML, CSS, JavaScript (vanilla); Node.js (devcontainer-provided, currently v24)  
**Primary Dependencies**: None beyond built-in Node.js; `serve` (via `npx`, no install needed); GitHub Actions (built-in CI/CD)  
**Storage**: N/A (static files only)  
**Testing**: Manual browser verification (open site in Codespace, check GitHub Pages URL)  
**Target Platform**: Web browser (GitHub Pages hosting); GitHub Codespaces for development  
**Project Type**: Static website  
**Performance Goals**: N/A (static HTML served by GitHub Pages CDN)  
**Constraints**: No build pipeline; no server-side logic; site must remain viewable by opening HTML directly or via trivial static server  
**Scale/Scope**: Single-page static site; ~5 files modified/created

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

| # | Principle | Status | Notes |
|---|-----------|--------|-------|
| I | Simplicity-First | ✅ PASS | No frameworks, no build pipelines. GitHub Actions workflow is minimal config (not a build tool). Site remains viewable via `npx serve` or direct file open. |
| II | Novice-Accessible | ✅ PASS | All changes improve novice accessibility: removing the access-request barrier, adding explicit preview instructions, documenting GitHub Pages setup step-by-step. |
| III | Spec-Driven Development | ✅ PASS | This change follows the full SDD workflow: `/speckit.specify` → `/speckit.plan` → `/speckit.tasks` → `/speckit.implement`. |
| IV | Devcontainer & Codespaces | ✅ PASS | Devcontainer updated with `forwardPorts: [8080]`. All instructions target Codespaces. No local installs required. |
| V | Iterative & Incremental | ✅ PASS | Single feature branch producing a deployable improvement. All changes are related (site content, README, deployment) and form a cohesive increment. |
| — | Technology Stack | ✅ PASS | No new dependencies introduced. `serve` is used via `npx` (already available in Node.js devcontainer). GitHub Actions is a GitHub-native feature, not a new dependency. |
| — | New dependency justification | ✅ PASS | No new dependencies. GitHub Actions workflow uses only official GitHub-provided actions (`actions/checkout`, `actions/configure-pages`, `actions/upload-pages-artifact`, `actions/deploy-pages`). |

**Gate result**: ALL PASS — proceed to Phase 0.

## Project Structure

### Documentation (this feature)

```text
specs/002-site-readme-ghpages/
├── plan.md              # This file
├── research.md          # Phase 0 output
├── data-model.md        # Phase 1 output
├── quickstart.md        # Phase 1 output
├── contracts/           # Phase 1 output
│   └── ui-contract.md   # Site content contract (Getting Started steps)
└── tasks.md             # Phase 2 output (/speckit.tasks command)
```

### Source Code (repository root)

```text
.devcontainer/
└── devcontainer.json        # MODIFY: add forwardPorts [8080]

.github/
└── workflows/
    └── deploy-pages.yml     # CREATE: GitHub Actions workflow for Pages

site/
├── index.html               # MODIFY: update Getting Started section
└── style.css                # NO CHANGE

README.md                    # REWRITE: mirror site content
```

**Structure Decision**: Flat static site structure preserved. Only addition is `.github/workflows/deploy-pages.yml` for deployment automation — this is a GitHub-native configuration file, not a build tool.

## Complexity Tracking

No constitution violations detected — this section is not applicable.

## Constitution Re-Check (Post-Design)

*Gate re-evaluated after Phase 1 design completion.*

| # | Principle | Status | Post-Design Notes |
|---|-----------|--------|-------------------|
| I | Simplicity-First | ✅ PASS | Workflow YAML is ~30 lines of config using official GitHub actions — no build step, no bundlers, no compilation. Site remains viewable by opening HTML directly. `npx serve` is a trivial one-command server. |
| II | Novice-Accessible | ✅ PASS | All new Getting Started steps explain what they do and why. Commands are provided verbatim. Port-forwarding instructions include both the notification popup and the Ports panel. Local dev note included. |
| III | Spec-Driven Development | ✅ PASS | Full SDD workflow followed (specify → plan → tasks → implement). |
| IV | Devcontainer & Codespaces | ✅ PASS | `forwardPorts: [8080]` added. All instructions assume Codespaces. No local installs needed. |
| V | Iterative & Incremental | ✅ PASS | Single feature branch, 4 files modified/created, cohesive increment. |
| — | Technology Stack | ✅ PASS | No new dependencies. `serve` via `npx`. GitHub Actions is GitHub-native. |

**Post-design gate result**: ALL PASS — ready for Phase 2 (`/speckit.tasks`).
