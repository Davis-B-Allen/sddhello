# Data Model: Dev Server Setup with Live Reload

**Feature Branch**: `003-dev-server-setup`  
**Date**: 2026-03-04

## Overview

This feature modifies configuration files rather than introducing application data. The "entities" below are the configuration structures that are created or modified.

## Entities

### Devcontainer Configuration

**What it represents**: The JSON configuration that defines the development container environment.

**File**: `.devcontainer/devcontainer.json`

**Key attributes**:
- `image`: Base container image (unchanged: `mcr.microsoft.com/devcontainers/javascript-node:4-24-trixie`)
- `forwardPorts`: Array of ports to forward (unchanged: `[8080]`)
- `postCreateCommand`: Shell command to run after container creation (new: `npm install -g browser-sync`)

**Validation rules**:
- `postCreateCommand` must be a valid shell command
- The installed package (`browser-sync`) must be available on `PATH` after the command completes
- The command must complete without errors in the devcontainer environment

**State transitions**:
- Container created → `postCreateCommand` executes → browser-sync globally installed → Container ready

### Dev Server Process

**What it represents**: The running browser-sync process that serves the static site.

**Key attributes**:
- Server root directory: `site/`
- Listening port: `8080`
- File watch scope: all files in `site/` (recursive)
- Browser interaction: disabled (`--no-open`, `--no-notify`, `--no-ui`)

**State transitions**:
- Idle → Command executed → Server listening on port 8080 + file watcher active → File change detected → Browser reload triggered → Watching again (loop)
- Server running → Ctrl+C → Server stopped → Idle

### Site Directory

**What it represents**: The static files served by the dev server.

**File**: `site/` directory

**Key attributes**:
- Contains HTML, CSS, and any future static assets
- No build step — files are served directly as-is
- Changes are detected by browser-sync's file watcher

**Relationships**:
- Served by: Dev Server Process
- Unchanged by this feature (content is not modified)
