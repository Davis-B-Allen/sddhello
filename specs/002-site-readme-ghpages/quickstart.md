# Quickstart: Site & README Updates for Public Repo + GitHub Pages

**Feature**: `002-site-readme-ghpages`  
**Date**: 2026-03-01

## What This Feature Does

Updates the project for its public repository status: removes the access-request step from Getting Started, adds local preview and GitHub Pages publishing steps, creates a GitHub Actions deployment workflow, and rewrites the README to match the site.

## Files Changed

| File | Action | Description |
|------|--------|-------------|
| `site/index.html` | MODIFY | Remove access-request step (old step 3), renumber remaining steps, add step 5 (local preview) and step 6 (GitHub Pages setup) |
| `.github/workflows/deploy-pages.yml` | CREATE | GitHub Actions workflow to deploy `site/` to Pages on push to `main` |
| `.devcontainer/devcontainer.json` | MODIFY | Add `forwardPorts: [8080]` for local preview |
| `README.md` | REWRITE | Replace brainstorming notes with structured project documentation mirroring site content |

## How to Verify

### 1. Site Content (local preview)

```bash
npx serve site -p 8080
```

Open the forwarded port in your browser (Codespaces: click notification or Ports panel). Verify:
- Getting Started has 6 steps (no access-request step)
- Step 3 links directly to the public repository for forking
- Step 5 explains local preview with `npx serve`
- Step 6 explains GitHub Pages setup

### 2. GitHub Actions Workflow

After merging to `main`:
- Go to the Actions tab → verify "Deploy to GitHub Pages" workflow runs
- Go to Settings → Pages → verify source is "GitHub Actions"
- Visit `https://<username>.github.io/<repo>/` → verify site is live

### 3. README

Visit the repository page on GitHub. Verify:
- README describes the project and links to the live site
- Getting Started steps match the site's 6 steps
- No brainstorming notes remain

### 4. Devcontainer

Rebuild the devcontainer (or open a new Codespace). Verify:
- Port 8080 appears in the Ports panel before starting any server

## Implementation Order

1. **Devcontainer**: Add `forwardPorts` (smallest change, no dependencies)
2. **GitHub Actions workflow**: Create `deploy-pages.yml` (independent of content changes)
3. **Site content**: Update `site/index.html` Getting Started section
4. **README**: Rewrite to mirror site content (depends on site content being finalized)
