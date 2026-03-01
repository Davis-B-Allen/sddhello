# Quickstart: Static Landing Page

**Feature Branch**: `001-static-landing-page`

## Prerequisites

- A GitHub Codespace running the project devcontainer (or any
  environment with Node.js available for the static server).
- Alternatively, any web browser — the page can be opened
  directly as a local file.

## Development

### 1. Preview the site (static server)

From the repo root:

```bash
npx serve site -p 8080
```

Then open via the **Ports** tab in Codespaces, or visit
`http://localhost:8080` if running locally.

### 2. Preview the site (direct file)

Open `site/index.html` directly in your browser (double-click
the file, or use `File → Open` in the browser). All relative
paths are designed to work with the `file://` protocol.

### 3. Files to edit

| File | Purpose |
|------|---------|
| `site/index.html` | Page content and structure |
| `site/style.css` | All styles (responsive, mobile-first) |

JavaScript (if any) is inline in `index.html` — no separate JS
file unless the scope grows.

### 4. Editing workflow

1. Edit `site/index.html` or `site/style.css`.
2. Save the file.
3. Refresh the browser tab to see changes.

No build step, no compilation, no hot-reload setup needed.

## Validation Checks

- [ ] Page loads in Chrome/Firefox/Safari/Edge without errors.
- [ ] Page loads via `file://` protocol (no server).
- [ ] All external links open in a new tab and resolve (no 404).
- [ ] Page is readable at 375px viewport width (mobile).
- [ ] Copy button copies the `/speckit.specify` prompt text.
- [ ] Heading hierarchy is sequential (h1 → h2 → h3).
- [ ] All text uses second-person voice ("you").
