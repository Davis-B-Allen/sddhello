# Research: Dev Server Setup with Live Reload

**Feature Branch**: `003-dev-server-setup`  
**Date**: 2026-03-04

## Research Task 1: Live-Reload Static Server Tool Selection

### Decision: browser-sync (v3.x)

### Rationale

browser-sync is the only actively maintained Node.js package that provides both static file serving and built-in live reload without requiring a build tool or `package.json`. It is purpose-built for this exact use case.

### Candidates Evaluated

| Criteria | browser-sync | live-server | vite | http-server | serve |
|---|---|---|---|---|---|
| Live reload | Yes (built-in + CSS injection) | Yes (built-in) | Yes (HMR) | No | No |
| Actively maintained | Yes (v3.0.4, Apr 2025) | No (v1.2.2, Apr 2022 — abandoned) | Yes (v7.3.1) | Yes | Yes |
| Node 24 compat | Clean, zero warnings | 5 deprecation warnings | Works | Works | Works |
| Suited for no-package.json project | Yes (global install) | Yes | No (expects project setup) | Yes | Yes |
| Devcontainer-safe | Yes (`--no-open --no-notify --no-ui`) | Mostly (`--no-browser`) | Needs `--host 0.0.0.0` | Yes | Clipboard error |

### Alternatives Rejected

- **live-server**: Abandoned (4 years since last release). 5 deprecated dependencies. Could break on future Node versions with no maintainer to fix. Unacceptable risk.
- **vite**: Overkill. Designed as a build tool, not a trivial static server. Expects a `package.json` project structure. Would add unnecessary conceptual complexity for beginners.
- **http-server**: No live reload. Would need to be paired with a separate file-watching tool, increasing complexity.
- **serve** (current tool): No live reload. Also produces clipboard errors in devcontainers (`xsel` not found). The exact tool being replaced.

### Recommended Command

```bash
browser-sync start --server site --port 8080 --no-open --no-notify --no-ui --watch
```

Flags explained:
- `--server site`: Serve the `site/` directory as a static site
- `--port 8080`: Use port 8080 (matches devcontainer port forwarding)
- `--no-open`: Don't attempt to open a browser (essential in containers — avoids errors)
- `--no-notify`: Disable the "Connected to BrowserSync" overlay notification
- `--no-ui`: Disable the BrowserSync UI dashboard (saves a port, reduces confusion)
- `--watch`: Watch all files in the served directory and reload on changes

---

## Research Task 2: Devcontainer Pre-Install Approach

### Decision: `postCreateCommand` with global npm install

### Rationale

`postCreateCommand` is the simplest, most conventional approach for installing a single npm tool in a devcontainer. It requires changing one line in the existing config, adds no new files, and works with Codespaces prebuilds.

### Approaches Evaluated

| Approach | Simplicity | Files Added | Prebuild Support | Startup Impact |
|---|---|---|---|---|
| `postCreateCommand` (global) | Highest | 0 | Yes | ~5–10s first create only |
| `onCreateCommand` (global) | High | 0 | Yes | Same |
| Custom Dockerfile | Moderate | +1 Dockerfile | Yes (Docker layer cache) | None after build |
| Devcontainer Feature | N/A | N/A | N/A | N/A |
| `package.json` + `npm install` | Low | +3 files | Yes | ~5–10s |

### Alternatives Rejected

- **onCreateCommand**: Would work, but `postCreateCommand` is the documented convention (the devcontainer template actually shows this pattern in comments). `postCreateCommand` also runs on rebuild, making it more robust.
- **Custom Dockerfile**: Overkill for a single npm package. Adds a Dockerfile that beginners would need to understand. Appropriate if we had multiple system-level dependencies, but unnecessary here.
- **Devcontainer Feature**: No official or widely-used feature exists for browser-sync. Writing a custom feature is vastly more complex.
- **package.json approach**: Adds 3 files to the project (`package.json`, `package-lock.json`, `.gitignore` for `node_modules`). Signals "this is a Node.js project" — misleading for a static HTML/CSS learning project. Introduces npm concepts that the target audience (absolute beginners) shouldn't need to encounter.

### Recommended Configuration

```jsonc
"postCreateCommand": "npm install -g browser-sync"
```

- Installs globally so the `browser-sync` command is available on `PATH` without `npx`
- No `package.json` needed — keeps the project as "just HTML and CSS"
- With Codespaces prebuilds: runs ahead of time, users get instant startup
- Without prebuilds: adds ~5–10s during "Setting up your codespace" phase (before user gets a terminal)

---

## Research Task 3: Port Forwarding and Codespaces Compatibility

### Decision: Keep existing `forwardPorts: [8080]` — no changes needed

### Rationale

The current devcontainer.json already has `"forwardPorts": [8080]`. browser-sync's `--port 8080` flag matches this configuration. Codespaces and VS Code will automatically detect the port and offer to open it in a browser.

### Notes

- browser-sync normally also starts a UI server on port 3001. The `--no-ui` flag disables this, keeping port usage clean and predictable.
- The `--no-open` flag prevents browser-sync from trying to launch a browser, which would fail inside a container and potentially produce errors similar to the `xsel` issue being fixed.
