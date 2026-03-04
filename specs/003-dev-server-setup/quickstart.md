# Quickstart: Dev Server Setup with Live Reload

**Feature Branch**: `003-dev-server-setup`

## What This Feature Does

Configures the devcontainer to pre-install a live-reload development server (browser-sync), so you can preview the static site with automatic browser refresh — no setup steps required.

## After Implementation

### Starting the Dev Server

From the project root in the terminal:

```bash
browser-sync start --server site --port 8080 --no-open --no-notify --no-ui --watch
```

The site will be served at `http://localhost:8080`. In Codespaces, the port is automatically forwarded — click the "Open in Browser" notification or use the Ports tab.

### Development Workflow

1. Start the dev server with the command above
2. Open the forwarded port in your browser
3. Edit files in `site/` (e.g., `index.html`, `style.css`)
4. Save — the browser automatically refreshes with your changes
5. Stop the server with `Ctrl+C` when done

### What Changed

| File | Change |
|---|---|
| `.devcontainer/devcontainer.json` | Added `postCreateCommand` to globally install `browser-sync` |

### Verification

After rebuilding the devcontainer, verify the tool is installed:

```bash
which browser-sync
# Expected: /usr/local/bin/browser-sync (or similar global path)

browser-sync --version
# Expected: 3.x.x
```

## Key Decisions

- **browser-sync** chosen over live-server (abandoned), vite (overkill), serve (no live reload)
- **Global install** via `postCreateCommand` — no `package.json` needed, keeps project simple
- **Port 8080** — matches existing `forwardPorts` in devcontainer config
