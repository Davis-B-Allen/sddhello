# CLI Contract: Dev Server Command

**Feature Branch**: `003-dev-server-setup`  
**Date**: 2026-03-04

## Command Interface

The primary user-facing interface for this feature is a CLI command that starts the development server.

### Command

```bash
browser-sync start --server site --port 8080 --no-open --no-notify --no-ui --watch
```

### Inputs

| Parameter | Value | Purpose |
|---|---|---|
| `--server site` | Directory path | Serve static files from the `site/` directory |
| `--port 8080` | Port number | Listen on port 8080 (matches devcontainer forwarding) |
| `--no-open` | Flag | Suppress browser auto-open (required in container environments) |
| `--no-notify` | Flag | Suppress "Connected to BrowserSync" overlay in browser |
| `--no-ui` | Flag | Disable BrowserSync management UI (avoids extra port) |
| `--watch` | Flag | Watch all files in served directory for changes |

### Expected Output (Success)

The server starts and displays a message indicating the listening address. No error messages, no install prompts.

```
[Browsersync] Access URLs:
 -----------------------------------
       Local: http://localhost:8080
    External: http://172.17.0.2:8080
 -----------------------------------
[Browsersync] Serving files from: site
[Browsersync] Watching files...
```

### Expected Behavior: File Change

When any file in `site/` is modified and saved:

```
[Browsersync] Reloading Browsers...
```

CSS-only changes may trigger injection instead of full reload:

```
[Browsersync] File event [change] : site/style.css
```

### Error Scenarios

| Scenario | Expected Behavior |
|---|---|
| Port 8080 already in use | Error message: "Port 8080 is already in use" (server does not start) |
| `site/` directory missing | Error message indicating directory not found |
| Command not found | Error: "browser-sync: command not found" (indicates `postCreateCommand` failed) |
| Run from wrong directory | Works if `site/` exists relative to current directory; otherwise directory not found error |

### Exit

The server runs until interrupted with `Ctrl+C`, which cleanly shuts down the process.

## Devcontainer Configuration Contract

### Modified File: `.devcontainer/devcontainer.json`

The devcontainer configuration is updated to include a `postCreateCommand` that installs browser-sync globally.

### Configuration Change

```jsonc
{
  // ... existing config unchanged ...
  "postCreateCommand": "npm install -g browser-sync"
}
```

### Lifecycle Behavior

1. Container is created from the base image
2. Source code is cloned into the container
3. `postCreateCommand` runs: `npm install -g browser-sync`
4. Container is marked as ready
5. User can immediately run the dev server command

### Invariants

- `forwardPorts: [8080]` must remain in the configuration
- The `postCreateCommand` must complete without errors
- After `postCreateCommand` completes, `which browser-sync` must return a valid path
