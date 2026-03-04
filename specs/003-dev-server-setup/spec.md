# Feature Specification: Dev Server Setup with Live Reload

**Feature Branch**: `003-dev-server-setup`  
**Created**: 2026-03-04  
**Status**: Draft  
**Input**: User description: "Improve devcontainer with pre-installed live-reload dev server for static site serving. Eliminate manual package installation prompts and clipboard errors. Provide a seamless development experience where file changes are reflected in realtime in the browser."

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Zero-Setup Dev Server Launch (Priority: P1)

A developer opens the project in a Codespace (or other devcontainer environment) for the first time and wants to preview the static site locally. They run a single command and the site is immediately served on a known port — no installation prompts, no errors, no extra steps.

**Why this priority**: This is the core pain point. The current experience requires confirming a package install and produces a clipboard error, both of which are confusing for beginners. Eliminating friction at first launch is the highest-value improvement.

**Independent Test**: Can be fully tested by opening a fresh devcontainer and running the serve command — the site should be accessible immediately without any prompts or errors.

**Acceptance Scenarios**:

1. **Given** a freshly created devcontainer, **When** the developer runs the dev server command, **Then** the site is served on port 8080 without any installation prompts or errors.
2. **Given** a freshly created devcontainer, **When** the developer runs the dev server command, **Then** no error messages about missing system utilities (e.g., clipboard tools) are displayed.
3. **Given** a freshly created devcontainer, **When** the developer opens the forwarded port in a browser, **Then** the site content from the `site/` directory is displayed correctly.

---

### User Story 2 - Live Reload During Development (Priority: P1)

A developer is actively editing the site's HTML or CSS files and wants to see changes reflected in the browser in realtime, without manually refreshing the page.

**Why this priority**: Live reload is essential for a productive development workflow, especially for beginners who benefit from immediate visual feedback. This is equally critical to the zero-setup experience since "development mode" is the stated goal.

**Independent Test**: Can be fully tested by starting the dev server, opening the site in a browser, editing a file in the `site/` directory, and observing that the browser updates automatically.

**Acceptance Scenarios**:

1. **Given** the dev server is running and the site is open in a browser, **When** the developer edits and saves an HTML file in `site/`, **Then** the browser reflects the change without a manual page refresh.
2. **Given** the dev server is running and the site is open in a browser, **When** the developer edits and saves a CSS file in `site/`, **Then** the browser reflects the style change without a manual page refresh.
3. **Given** the dev server is running and the site is open in a browser, **When** the developer adds a new file to `site/`, **Then** the new file is accessible via the dev server without restarting it.

---

### User Story 3 - Pre-Installed Tooling in Devcontainer (Priority: P1)

When the devcontainer is built and started, all tools needed to serve the site with live reload are already installed and ready to use. The developer does not need to run any setup or install commands before they can begin working.

**Why this priority**: This underpins Stories 1 and 2. If the tooling isn't pre-installed, the zero-setup promise fails. The devcontainer definition must ensure all dependencies are present at container creation time.

**Independent Test**: Can be fully tested by building a fresh devcontainer and verifying the dev server tool is available on the PATH without any additional install steps.

**Acceptance Scenarios**:

1. **Given** a devcontainer is built from the project's devcontainer definition, **When** the container finishes starting, **Then** the dev server tool is installed and available on the PATH.
2. **Given** a devcontainer is built from the project's devcontainer definition, **When** the developer checks for the dev server tool, **Then** no additional packages need to be downloaded or confirmed.

---

### Edge Cases

- What happens when the developer tries to start the dev server while port 8080 is already in use? The server should fail with a clear error message indicating the port conflict.
- What happens when the developer deletes a file that is currently being served? The server should respond with a standard "not found" response for that path.
- What happens if the developer runs the serve command from a directory other than the project root? The command should still serve the correct `site/` directory (or provide clear instructions about the expected working directory).
- What happens if the `site/` directory is empty? The server should start successfully and serve an empty directory listing or a default page.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: The devcontainer definition MUST pre-install a static file server tool with live reload capability, so it is available immediately when the container starts.
- **FR-002**: The dev server MUST serve the contents of the `site/` directory on port 8080.
- **FR-003**: The dev server MUST support live reload — automatically refreshing connected browsers when files in the served directory change.
- **FR-004**: The dev server command MUST be runnable without any interactive prompts (no install confirmations, no permission dialogs).
- **FR-005**: The dev server MUST NOT produce error messages about missing system utilities (such as clipboard tools).
- **FR-006**: The dev server MUST watch for changes to HTML, CSS, and any other static files in the `site/` directory.
- **FR-007**: Port 8080 MUST be configured for automatic forwarding in the devcontainer definition so it is accessible from the host.

### Key Entities

- **Devcontainer Definition**: The configuration file(s) that define the development container environment, including pre-installed tools, forwarded ports, and post-creation setup commands.
- **Site Directory**: The `site/` folder containing the static website files (HTML, CSS, and any future assets) that are served by the dev server.
- **Dev Server**: The command-line tool that serves static files with live reload capability, pre-installed in the container.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: A developer can start serving the site with live reload using a single command, with zero installation prompts or errors, within 2 seconds of running the command.
- **SC-002**: Changes saved to any file in the `site/` directory are reflected in the browser within 2 seconds without manual page refresh.
- **SC-003**: A fresh devcontainer build results in all required dev server tooling being immediately available — no post-start package installations needed.
- **SC-004**: The dev server startup produces clean output with no error messages or warnings.

## Assumptions

- The project will continue to be a simple static site (HTML, CSS, and static assets) without a build step or server-side logic for the foreseeable future.
- The target audience is beginners who may not be familiar with package managers or terminal prompts, so zero-friction tooling is paramount.
- Port 8080 is the agreed-upon port for local development serving and is already configured for forwarding in the current devcontainer definition.
- The devcontainer is based on a Node.js image, so Node.js-based dev server tools are a natural fit, though the specification does not prescribe a specific tool.
- A `postCreateCommand` or similar devcontainer lifecycle hook is an acceptable mechanism for pre-installing tools during container build.
