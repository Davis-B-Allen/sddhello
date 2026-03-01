# UI Contract: Getting Started Steps

**Feature**: `002-site-readme-ghpages`  
**Date**: 2026-03-01  
**Applies to**: `site/index.html` (Getting Started section) and `README.md` (Getting Started section)

## Overview

The Getting Started section is the primary user-facing interface for onboarding new contributors. It must present a numbered, ordered sequence of steps that takes a user from zero (no GitHub account) to a fully functional development and publishing workflow. Both the site and the README must present the same steps in the same order.

## Step Sequence Contract

The Getting Started section MUST contain exactly the following steps, in this order:

| Step | Title | Required Elements |
|------|-------|-------------------|
| 1 | Create a GitHub account | Link to `https://github.com/signup` |
| 2 | Sign up for GitHub Copilot Pro free trial | Link to `https://github.com/github-copilot/signup` |
| 3 | Fork the repository | Direct link to the public repository page; instructions to click "Fork"; explanation of what forking means |
| 4 | Open your fork in GitHub Codespaces | Instructions to navigate to fork, click Code → Codespaces → Create codespace on main |
| 5 | Preview the site locally | Command: `npx serve site -p 8080`; Codespaces port-forwarding instructions; Note/aside for local development (localhost:8080) |
| 6 | Publish your site with GitHub Pages | Instructions to enable Actions on fork; Instructions to set Pages source to GitHub Actions (Settings → Pages); Expected URL format: `https://<username>.github.io/<repo>/`; Note about the workflow file needing to be present |

### Removed Steps

The following step from the previous version is **removed**:

- ~~**Step 3 (old)**: Contact the project owner for repository access~~ — Removed because the repository is now public.

### Step Details

#### Step 5: Preview the Site Locally

**Primary (Codespaces) instructions**:
1. Open the Terminal in VS Code (Terminal → New Terminal, or `` Ctrl+` ``)
2. Run: `npx serve site -p 8080`
3. When the notification popup appears saying "Your application running on port 8080 is available," click **Open in Browser** — OR open the **Ports** panel (bottom bar) and click the globe icon next to port 8080

**Secondary (local development) aside/note**:
> **Note**: If you're developing locally (not in a Codespace), you can open `http://localhost:8080` directly in your browser after running the serve command.

#### Step 6: Publish Your Site with GitHub Pages

1. In your fork on GitHub, go to the **Actions** tab
2. If prompted, click **"I understand my workflows, go ahead and enable them"**
3. Go to **Settings → Pages** (in the left sidebar under "Code and automation")
4. Under **Build and deployment**, set **Source** to **GitHub Actions**
5. Push a commit to `main` (or click **"Run workflow"** on the Actions tab) to trigger deployment
6. After a few minutes, your site will be live at `https://<username>.github.io/<repo>/`

## GitHub Actions Workflow Contract

**File**: `.github/workflows/deploy-pages.yml`

The workflow MUST:
- Trigger on push to `main` and on `workflow_dispatch`
- Use only official GitHub-provided actions (`actions/checkout@v4`, `actions/configure-pages@v5`, `actions/upload-pages-artifact@v4`, `actions/deploy-pages@v4`)
- Set permissions: `contents: read`, `pages: write`, `id-token: write`
- Deploy from `path: 'site/'`
- Use concurrency group `"pages"` with `cancel-in-progress: false`
- Declare environment `github-pages`

## README Contract

The README MUST contain:
1. Project title and one-line description
2. Link to the live GitHub Pages site
3. "What is this?" section (matching site content)
4. "Key Concepts" section (brief — can be shorter than the site version)
5. "Getting Started" section (same 6 steps as the site, in Markdown)
6. "Next Steps" section (brief reference to the site's Next Steps)
7. "Reference Links" section

The README MUST NOT contain:
- The original brainstorming notes
- Implementation details about spec-kit internals
- Any step referencing requesting access to a private repository
