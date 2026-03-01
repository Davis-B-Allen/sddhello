# Feature Specification: Site & README Updates for Public Repo + GitHub Pages

**Feature Branch**: `002-site-readme-ghpages`  
**Created**: 2026-03-01  
**Status**: Draft  
**Input**: User description: "Update site for public repo, rewrite README, deploy with GitHub Pages, enhance Getting Started with local preview and publishing instructions"

## User Scenarios & Testing *(mandatory)*

### User Story 1 — Visitor Forks a Public Repository (Priority: P1)

A first-time visitor arrives at the site with no coding experience. They follow the Getting Started steps and reach the step where they need to fork the repository. Since the repository is now public, they no longer need to request access or be added as a collaborator. The site simply links them to the repository page on GitHub where they can click "Fork" immediately.

**Why this priority**: This is the most fundamental user flow — getting a new user into their own copy of the project. Removing the access-request friction is the single biggest usability improvement for new visitors.

**Independent Test**: Visit the site, follow the Getting Started steps, and confirm that no step mentions requesting access. The fork step links directly to the GitHub repository and a user with a free GitHub account can fork it without any additional permissions.

**Acceptance Scenarios**:

1. **Given** a visitor is reading the Getting Started section, **When** they reach the fork step, **Then** they see a direct link to the public repository with instructions to click "Fork" — no mention of requesting access or being added as a collaborator.
2. **Given** the old "Contact the project owner for repository access" step existed, **When** the site is updated, **Then** that step is removed entirely and the remaining steps are renumbered.
3. **Given** a visitor with a free GitHub account clicks the repository link, **When** they click "Fork" on the GitHub page, **Then** they can successfully create their own copy without needing any special invitation.

---

### User Story 2 — Contributor Previews the Site Locally in Codespaces (Priority: P1)

A user has opened their fork in a GitHub Codespace and wants to see the site running in their browser. The Getting Started section includes a step that tells them how to start a local static file server and view the site. Since the primary workflow uses Codespaces, the instructions focus on how Codespaces handles port forwarding and the browser preview.

**Why this priority**: Without the ability to preview changes, users cannot verify that their work is correct. This is essential for the learning workflow.

**Independent Test**: Open the project in a Codespace, follow the local preview instructions, and verify that the site loads in a browser tab.

**Acceptance Scenarios**:

1. **Given** a user has the project open in a Codespace, **When** they follow the local preview step, **Then** a static file server starts serving content from the `site/` folder and the site is accessible in a browser tab via the Codespaces port-forwarding mechanism.
2. **Given** the local preview step is documented, **When** a user reads it, **Then** the command to run is explicitly provided (e.g., `npx serve site -p 8080`) and the instructions explain how to open the forwarded port in Codespaces.
3. **Given** a user is developing locally (not in Codespaces), **When** they read the local preview step, **Then** a note or aside explains they can visit `localhost` directly in their browser.

---

### User Story 3 — Site Published Automatically via GitHub Pages (Priority: P1)

The site owner (and anyone who forks the repo) wants the site content from `site/` to be automatically published to GitHub Pages whenever changes are pushed to `main`. Since GitHub Pages natively supports only root (`/`) or `docs/` as publish directories, and the project uses `site/`, a GitHub Actions workflow is needed to deploy the `site/` folder to GitHub Pages.

**Why this priority**: Publishing to the web is a core project goal. Without this, the site is only viewable locally. The GitHub Actions approach lets the project keep its current `site/` folder structure without restructuring.

**Independent Test**: Push a change to `main`, wait for the GitHub Actions workflow to complete, and verify the site is live at the GitHub Pages URL.

**Acceptance Scenarios**:

1. **Given** the repository contains a GitHub Actions workflow for Pages deployment, **When** a commit is pushed to `main`, **Then** the workflow runs and deploys the contents of the `site/` folder to GitHub Pages.
2. **Given** a user has forked the repository, **When** they enable GitHub Pages in their fork's settings (source: GitHub Actions), **Then** their fork's site is published at `https://<username>.github.io/<repo>/`.
3. **Given** the workflow is present in the repository, **When** a user views the Actions tab on GitHub, **Then** they can see the deployment status and any errors.

---

### User Story 4 — Getting Started Explains GitHub Pages Publishing (Priority: P2)

After setting up their Codespace and previewing the site locally, the user sees a Getting Started step that explains how to enable GitHub Pages on their fork. This step gives them clear instructions so that future changes they push will be published live on the web.

**Why this priority**: This completes the end-to-end flow from setup to live publishing. It depends on the GitHub Actions workflow (Story 3) being in place.

**Independent Test**: Follow the GitHub Pages step in Getting Started, enable Pages on a forked repo, push a change, and confirm the site goes live.

**Acceptance Scenarios**:

1. **Given** a user is reading the Getting Started section, **When** they reach the GitHub Pages step, **Then** they see clear instructions for enabling GitHub Pages in their fork's repository settings (Settings → Pages → Source: GitHub Actions).
2. **Given** a user has followed the GitHub Pages instructions, **When** they push a change to `main`, **Then** their updated site is published live within a few minutes.
3. **Given** a user is reading the GitHub Pages step, **When** they look for the expected URL, **Then** the instructions tell them their site will be at `https://<username>.github.io/<repo>/`.

---

### User Story 5 — README Reflects the Site Content (Priority: P2)

A developer or visitor landing on the GitHub repository page sees a README that clearly describes what the project is, how to get started, and links to the live site. The README content mirrors the site content so there is a single source of truth for the project's purpose and onboarding flow.

**Why this priority**: The README is the first thing visitors see on GitHub. The current README contains informal brainstorming notes. A proper README improves discoverability and professionalism, but the site itself is the primary user-facing artifact.

**Independent Test**: Visit the repository on GitHub and confirm the README clearly describes the project, includes Getting Started steps consistent with the site, and links to the live published site.

**Acceptance Scenarios**:

1. **Given** a visitor lands on the GitHub repository page, **When** they read the README, **Then** it describes what the project is, its purpose, and includes a clear Getting Started section.
2. **Given** the README has been rewritten, **When** compared to the site content, **Then** the project description, key concepts, and Getting Started steps are consistent between both.
3. **Given** the site is published via GitHub Pages, **When** a user reads the README, **Then** it includes a link to the live site URL.

---

### Edge Cases

- What happens if a user tries to enable GitHub Pages but hasn't pushed the Actions workflow yet? The Getting Started instructions should note that the workflow file must be present in the repository for Pages deployment to work.
- What happens if the static file server port (8080) is already in use in the Codespace? The instructions should mention that users can choose a different port if needed.
- What happens if a forked repository has a name that differs from the original? The GitHub Pages URL will reflect the fork's repository name, and the instructions should make this clear.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: The site's Getting Started section MUST NOT include any step asking users to contact the project owner or request repository access.
- **FR-002**: The site's Getting Started section MUST include a step with a direct link to the public repository on GitHub, encouraging users to fork it.
- **FR-003**: The Getting Started steps MUST be renumbered to account for the removal of the access-request step (currently step 3).
- **FR-004**: The Getting Started section MUST include a step explaining how to start a local static file server to preview the site in a Codespace, with an explicit command (e.g., `npx serve site -p 8080`).
- **FR-005**: The local preview step MUST explain how to open the forwarded port in GitHub Codespaces (via the Ports panel or the notification popup).
- **FR-006**: The local preview step MUST include a note or aside for users developing locally, explaining they can visit `localhost:8080` in their browser.
- **FR-007**: A GitHub Actions workflow MUST be added that deploys the `site/` folder to GitHub Pages on pushes to `main`.
- **FR-008**: The Getting Started section MUST include a step explaining how to enable GitHub Pages on a forked repository (Settings → Pages → Source: GitHub Actions).
- **FR-009**: The GitHub Pages step MUST tell users what URL their published site will be available at (`https://<username>.github.io/<repo>/`).
- **FR-010**: The root `README.md` MUST be rewritten to describe the project's purpose, key concepts, Getting Started steps, and a link to the live site — consistent with the site content.
- **FR-011**: The README MUST NOT contain the original informal brainstorming notes.
- **FR-012**: The devcontainer configuration MUST forward port 8080 so the local preview workflow works seamlessly in Codespaces.

### Key Entities

- **Site content** (`site/index.html`, `site/style.css`): The user-facing static site files, served from the `site/` directory.
- **README** (`README.md`): The project's root documentation file displayed on the GitHub repository page.
- **GitHub Actions workflow** (`.github/workflows/`): A CI/CD configuration file that automates deployment of `site/` to GitHub Pages.
- **Devcontainer configuration** (`.devcontainer/devcontainer.json`): Development environment configuration including port forwarding.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: A new user with a free GitHub account can go from the site's Getting Started section to a running Codespace with a local site preview in under 10 minutes, with no step requiring them to contact anyone or request access.
- **SC-002**: After pushing a change to `main`, the site is published live on GitHub Pages within 5 minutes without any manual deployment steps.
- **SC-003**: A user who forks the repository can enable GitHub Pages on their fork and see their site live by following the documented Getting Started step — no external knowledge required.
- **SC-004**: The README on the GitHub repository page clearly communicates the project's purpose and Getting Started flow to a non-technical visitor within 2 minutes of reading.
- **SC-005**: The site's Getting Started section and the README's Getting Started section are consistent — covering the same steps in the same order.

## Assumptions

- The repository is hosted on GitHub and is now public (the user confirmed this).
- GitHub Pages is available for public repositories on free GitHub plans.
- The project structure keeps site content in `site/` (no move to `docs/` or root).
- The GitHub Actions approach using `actions/deploy-pages` is the standard method for deploying a custom publish directory to GitHub Pages.
- Contributors primarily use GitHub Codespaces as their development environment; local development is secondary but acknowledged.
- Port 8080 is a reasonable default for local preview; it is commonly available and doesn't conflict with standard services.
- `npx serve` is available in the devcontainer Node.js image without additional installation.
