<!--
  Sync Impact Report
  Version: 1.0.0 (initial draft, pre-ratification)
  Added sections: Core Principles (5), Technology Stack, Development Workflow, Governance
  Templates requiring updates: ✅ No updates needed (templates are generic)
  Follow-up TODOs: None
-->

# SDD Hello Constitution

## Core Principles

### I. Simplicity-First

This project MUST remain a simple, static, single-page website.
No server-side logic, databases, or complex build pipelines.
The site MUST be viewable by opening an HTML file directly or via
a trivial static file server (e.g. `npx serve`). Every feature
addition MUST justify its complexity — prefer plain HTML/CSS/JS
over frameworks unless a clear, documented need arises.

### II. Novice-Accessible

All tooling, documentation, and workflow choices MUST prioritize
accessibility for non-technical contributors. Instructions MUST
assume zero prior development experience. Jargon MUST be defined
on first use. The "Get Started" guide on the site MUST be
end-to-end testable by someone with no coding background using
only a browser and a GitHub account.

### III. Spec-Driven Development

All non-trivial changes MUST follow the spec-driven development
workflow using GitHub spec-kit. The project is bootstrapped once
with the `specify init` CLI; ongoing development uses `/speckit.*`
slash commands inside the AI agent (Copilot agent mode):
1. `/speckit.specify` — write or update a specification.
2. `/speckit.clarify` — clarify underspecified areas (optional).
3. `/speckit.plan` — derive a technical implementation plan.
4. `/speckit.tasks` — generate an actionable task list.
5. `/speckit.implement` — execute tasks per the plan.
Skipping the spec step is only acceptable for typo fixes,
formatting, or single-line content corrections.

### IV. Devcontainer & Codespaces as the Primary Environment

The canonical development environment is the project devcontainer
running in GitHub Codespaces. All setup instructions, scripts,
and tooling MUST work inside this environment without additional
manual configuration. Contributors SHOULD NOT need to install
anything locally.

### V. Iterative & Incremental

Deliver working increments. Each feature branch SHOULD produce a
deployable (or at least previewable) improvement to the site.
Avoid large, multi-feature branches. Prefer small pull requests
that can be reviewed and merged independently.

## Technology Stack

- **Runtime**: Node.js (as provided by the devcontainer image)
- **Languages**: HTML, CSS, JavaScript (vanilla to start)
- **Hosting**: Static files only — no server-side rendering
- **Dev environment**: VS Code devcontainer (Node.js base image),
  GitHub Codespaces
- **AI tooling**: GitHub Copilot (agent mode)
- **SDD tooling**: GitHub spec-kit — bootstrapped via `specify`
  CLI; day-to-day workflow via `/speckit.*` slash commands in
  agent mode
- **Version control**: Git, hosted on GitHub

Introducing a new dependency or build tool MUST be justified in a
spec and approved before implementation.

## Development Workflow

1. **Branch**: Create a feature branch from `main`.
2. **Specify**: In Copilot agent mode, use `/speckit.specify`,
   `/speckit.plan`, and `/speckit.tasks` to draft specs, plans,
   and tasks for the change.
3. **Implement**: Use `/speckit.implement` (or work through tasks
   manually) in Copilot agent mode.
4. **Preview**: Start a local static server, verify via the
   Codespaces Ports tab.
5. **Commit & PR**: Push the branch and open a pull request.
6. **Review**: Ensure the PR aligns with the spec and this
   constitution.
7. **Merge**: Squash-merge into `main`.

## Governance

This constitution is the highest-authority document for project
decisions. All specifications, plans, and pull requests MUST be
consistent with these principles.

Amendments to this constitution MUST be proposed via a spec-kit
specification, reviewed, and merged through the standard PR
process. Each amendment MUST include a version bump following
semantic versioning (MAJOR for principle removals/redefinitions,
MINOR for additions, PATCH for clarifications).

**Version**: 1.0.0 | **Ratified**: 2026-03-01 | **Last Amended**: 2026-03-01
