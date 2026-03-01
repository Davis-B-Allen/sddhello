# Data Model: Site & README Updates for Public Repo + GitHub Pages

**Feature**: `002-site-readme-ghpages`  
**Date**: 2026-03-01

## Overview

This feature involves no persistent data storage or relational entities. The "data model" describes the static content structures and configuration files that are created or modified.

## Entities

### 1. Site Content (`site/index.html`)

**What it represents**: The primary user-facing HTML page containing project information and Getting Started instructions.

**Key attributes (content sections)**:
- Header (title, subtitle)
- "What is this?" section (project description)
- "Key Concepts" section (Codespaces, Copilot, SDD/spec-kit)
- "Getting Started" section (ordered steps — the primary entity modified in this feature)
- "Next Steps" section (suggested first feature)
- "Reference Links" section (consolidated external links)
- Footer

**Relationships**: Content mirrors → README.md (Getting Started steps and project description must stay in sync)

**Validation rules**:
- Getting Started steps must be a numbered `<ol>` list
- No step may reference requesting access or being added as collaborator
- Must include steps for: GitHub account, Copilot Pro trial, fork, Codespace, local preview, GitHub Pages setup
- All external links must use `target="_blank" rel="noopener noreferrer"`

**State transitions**: N/A (static content)

### 2. README (`README.md`)

**What it represents**: The project's root documentation file displayed on the GitHub repository page.

**Key attributes (content sections)**:
- Title and description
- Link to live site
- Key Concepts (brief)
- Getting Started (same steps as site, in Markdown)
- Next Steps (brief)
- Reference Links

**Relationships**: Content mirrors ← Site content (`site/index.html`)

**Validation rules**:
- Must be valid GitHub-Flavored Markdown
- Getting Started steps must match the site in number and order
- Must include a link to the live GitHub Pages URL

### 3. GitHub Actions Workflow (`.github/workflows/deploy-pages.yml`)

**What it represents**: CI/CD configuration that automates deployment of `site/` to GitHub Pages.

**Key attributes**:
- Trigger: push to `main` branch + `workflow_dispatch`
- Permissions: `contents: read`, `pages: write`, `id-token: write`
- Concurrency group: `"pages"` (no cancel-in-progress)
- Environment: `github-pages`
- Upload path: `site/`

**Relationships**: Deploys → Site content (`site/`)

**Validation rules**:
- Must use only official GitHub-provided actions
- Must specify `path: 'site/'` in the upload step
- Must trigger on push to `main`

### 4. Devcontainer Configuration (`.devcontainer/devcontainer.json`)

**What it represents**: Development environment configuration for VS Code devcontainers / Codespaces.

**Key attributes** (modified):
- `forwardPorts`: `[8080]` (added)

**Relationships**: Supports → local preview workflow (port 8080 for `npx serve`)

**Validation rules**:
- Must be valid JSONC
- Must include port 8080 in `forwardPorts` array
