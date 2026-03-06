# sddhello Development Guidelines

Auto-generated from all feature plans. Last updated: 2026-03-01

## Active Technologies
- HTML, CSS, JavaScript (vanilla); Node.js (devcontainer-provided, currently v24) + None beyond built-in Node.js; `serve` (via `npx`, no install needed); GitHub Actions (built-in CI/CD) (002-site-readme-ghpages)
- N/A (static files only) (002-site-readme-ghpages)
- HTML, CSS (static site content); Node.js 24.x (devcontainer runtime) + browser-sync v3.x (globally installed via `postCreateCommand`) (003-dev-server-setup)
- HTML5, CSS3, JavaScript (ES6+, vanilla) + None — vanilla HTML/CSS/JS only (004-tutorial-redesign)
- HTML5, CSS3, vanilla JavaScript (existing copy-button script) + None — static HTML/CSS site, no frameworks (005-concept-pages)
- N/A — static files only (005-concept-pages)

- HTML5, CSS3, JavaScript (ES6+, optional) + None — vanilla HTML/CSS/JS only (001-static-landing-page)

## Project Structure

```text
backend/
frontend/
tests/
```

## Commands

npm test && npm run lint

## Code Style

HTML5, CSS3, JavaScript (ES6+, optional): Follow standard conventions

## Recent Changes
- 005-concept-pages: Added HTML5, CSS3, vanilla JavaScript (existing copy-button script) + None — static HTML/CSS site, no frameworks
- 004-tutorial-redesign: Added HTML5, CSS3, JavaScript (ES6+, vanilla) + None — vanilla HTML/CSS/JS only
- 003-dev-server-setup: Added HTML, CSS (static site content); Node.js 24.x (devcontainer runtime) + browser-sync v3.x (globally installed via `postCreateCommand`)


<!-- MANUAL ADDITIONS START -->
<!-- MANUAL ADDITIONS END -->
