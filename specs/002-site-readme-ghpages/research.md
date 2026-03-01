# Research: Site & README Updates for Public Repo + GitHub Pages

**Feature**: `002-site-readme-ghpages`  
**Date**: 2026-03-01

## Research Area 1: GitHub Actions Workflow for Pages Deployment from `site/`

### Decision
Use the official GitHub starter workflow pattern for static HTML, modified to deploy from `site/` instead of the repository root. The workflow uses four official GitHub-provided actions: `actions/checkout@v4`, `actions/configure-pages@v5`, `actions/upload-pages-artifact@v4`, and `actions/deploy-pages@v4`.

### Rationale
- GitHub Pages natively supports only root (`/`) or `docs/` as publish sources when using "Deploy from a branch." Since the project uses `site/`, the "GitHub Actions" source method is required.
- The `actions/upload-pages-artifact@v4` action accepts a `path` input parameter (default: `_site/`). Setting `path: 'site/'` deploys only the site directory.
- This is the officially recommended pattern from GitHub's own starter-workflows repository.
- Single-job workflow (no separate build step) because the site is pre-built static HTML/CSS — no compilation or bundling needed.

### Alternatives Considered
1. **Move site content to `docs/`**: Would allow "Deploy from a branch" without Actions. Rejected because it changes the established project structure and `site/` is a more intuitive directory name for novice contributors.
2. **Move site content to root (`/`)**: Would allow default Pages deployment. Rejected because mixing site files with project config files (devcontainer.json, README, specs/) is messy and violates the project's organizational convention.
3. **Third-party action (`peaceiris/actions-gh-pages`)**: Deploys to a `gh-pages` branch instead of using the official Pages API. Rejected because official GitHub-maintained actions are more appropriate for a project that teaches GitHub workflows, and the official path avoids maintaining a separate orphan branch.

### Key Workflow Details

```yaml
permissions:
  contents: read    # checkout
  pages: write      # Pages API
  id-token: write   # OIDC verification
```

- `workflow_dispatch` enables manual re-deployment from the Actions tab.
- Concurrency group `"pages"` prevents parallel deployments.
- Environment `github-pages` auto-creates and provides the deployment URL.

## Research Area 2: GitHub Pages Setup for Forked Repositories

### Decision
Document a three-step process for fork owners: (1) enable GitHub Actions on the fork, (2) set Pages source to "GitHub Actions" in Settings → Pages, (3) push a commit or manually trigger the workflow.

### Rationale
- **Actions are disabled by default on forks** as a security measure. Users must explicitly enable them via the Actions tab.
- **Pages must be enabled per-repository** — the settings are not inherited from the upstream repository.
- The `GITHUB_TOKEN` is automatically provided; no secrets configuration is needed.
- Free GitHub plans support Pages on public repositories (forks of public repos are public by default).

### Alternatives Considered
None — this is the only supported process for forked repositories using GitHub Actions for Pages.

## Research Area 3: Local Site Preview with `npx serve` in Codespaces

### Decision
Use `npx serve site -p 8080` as the recommended preview command. Document Codespaces port forwarding (automatic popup or Ports panel) as the primary way to view the site.

### Rationale
- `serve` is available via `npx` in the devcontainer Node.js image — no installation step needed.
- The `serve` package supports serving a subdirectory directly (`serve site`), avoiding the need to `cd` into the directory.
- Port 8080 is specified explicitly (vs the default 3000) for consistency with the devcontainer `forwardPorts` configuration and to be a well-known, memorable port.
- In Codespaces, when a server starts on a forwarded port, VS Code shows a notification with an "Open in Browser" button. The port also appears in the Ports panel (bottom bar).

### Alternatives Considered
1. **`python -m http.server`**: Available on most systems but serves from the current directory only (would need `cd site` first) and doesn't support clean URLs. Rejected because `npx serve` is more idiomatic for a Node.js devcontainer.
2. **VS Code Live Server extension**: Requires installing an extension. Rejected because it adds a dependency and the constitution prefers minimal tooling.
3. **Default port 3000**: Would work, but 8080 is more conventional for development servers and avoids confusion with other Node.js defaults.

## Research Area 4: Devcontainer Port Forwarding Configuration

### Decision
Add `"forwardPorts": [8080]` to `.devcontainer/devcontainer.json`.

### Rationale
- The `forwardPorts` property in devcontainer.json tells VS Code / Codespaces to automatically forward the specified port from the container to the host.
- This ensures the port is forwarded even before the server starts, making the Ports panel pre-populated.
- It also makes the port visible in the Codespaces Ports tab by default, so users can find it easily.

### Alternatives Considered
1. **Rely on automatic port detection**: Codespaces detects listening ports automatically. However, pre-declaring the port makes the experience more predictable and discoverable for novice users.
2. **`appPort` in docker-compose**: Not applicable — the project uses a simple devcontainer, not docker-compose.

## Research Area 5: README Content Mirroring Strategy

### Decision
Rewrite README.md in Markdown to mirror the site's structure: project description, key concepts (brief), Getting Started steps (same sequence as site), link to live site, reference links. The README should be a Markdown equivalent of the site content, not a separate document.

### Rationale
- The README is the first thing visitors see on the GitHub repository page.
- Keeping content consistent between site and README avoids confusion and drift.
- Markdown is the natural format for GitHub READMEs and renders well on the repository page.

### Alternatives Considered
1. **Minimal README that just links to the site**: Too sparse — would not help users who find the repo before the site. Rejected.
2. **Generate README from HTML automatically**: Adds build-step complexity. Rejected per Simplicity-First principle.
3. **Single source (README only, no site)**: Eliminates the HTML site entirely. Rejected because the site is the primary user-facing artifact with better styling and UX.
