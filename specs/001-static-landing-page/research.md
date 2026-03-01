# Phase 0 Research: Static Landing Page

**Feature Branch**: `001-static-landing-page`  
**Date**: 2026-03-01  
**Spec**: [spec.md](spec.md) | **Plan**: [plan.md](plan.md)

---

## Topic 1: File structure — `site/` subdirectory vs repo root

### Decision

Place all deliverable files in a **`site/` subdirectory** at the repo root, containing `index.html` and `style.css`.

### Rationale

1. **Separation of concerns.** The repo root already contains `README.md`, `.specify/`, `.devcontainer/`, `.github/`, `.vscode/`, and `specs/`. Placing `index.html` at the root would mix the deliverable product with project meta-files, making the repo harder to navigate — especially for the non-technical audience this project targets.

2. **Deployment readiness.** A dedicated `site/` directory maps directly to a deployment root. GitHub Pages can be configured to serve from a subdirectory (e.g. `/docs` or a custom path via GitHub Actions). Having a clean directory with only web assets simplifies any future static hosting setup without needing to add ignore rules or restructure.

3. **`file://` protocol compatibility.** A `site/` subdirectory does not break `file://` access. The user simply opens `site/index.html` in their browser. Relative asset paths (e.g. `<link href="style.css">`) resolve correctly because `style.css` sits alongside `index.html` in the same directory. No build step or path rewriting is needed.

4. **Scalability.** If assets are added later (images, a favicon, additional CSS files, or a small JS file), the `site/` directory provides a natural home without cluttering the repo root.

5. **Convention alignment.** Many static-site projects (Jekyll uses `_site/`, Hugo uses `public/`, common GitHub Pages repos use `docs/`) use a dedicated output or source directory. `site/` is a clear, self-documenting name.

### Alternatives considered

| Alternative | Why rejected |
|---|---|
| **Repo root** (`index.html` next to `README.md`) | Mixes deliverable with meta-files. As the repo grows, the root becomes cluttered. Also complicates GitHub Pages config if you want to serve only web files. |
| **`docs/` subdirectory** | A common GitHub Pages convention, but semantically misleading — this directory would contain the site itself, not documentation. Could confuse contributors. |
| **`public/` subdirectory** | Associated with build-tool output (Create React App, Vite, Hugo). Implies a build step exists, which contradicts this project's no-build-tools constraint. |

---

## Topic 2: Responsive CSS approach for a single page with no build tools

### Decision

Use a **mobile-first** CSS strategy with a single `style.css` file containing:
- A minimal CSS reset (box-sizing, margin/padding normalization).
- CSS custom properties (variables) for theming (colors, spacing, font sizes, max-widths).
- Base styles targeting the smallest viewport (375px+) by default.
- One or two `min-width` media queries to enhance layout for wider screens (e.g. `@media (min-width: 768px)`).
- The standard `<meta name="viewport" content="width=device-width, initial-scale=1">` tag in the HTML `<head>`.

### Rationale

1. **Mobile-first is simpler for a content-heavy single page.** The page is primarily text content in a single column. A single-column layout is already the correct mobile layout, so starting there means the base CSS is minimal. Wider viewports only need small adjustments (wider max-width, larger font sizes, more padding) — these are additive enhancements, not overrides.

2. **`min-width` queries produce less CSS than `max-width`.** Desktop-first (`max-width`) would require writing full desktop styles as the base, then overriding them downward for mobile — more code, more specificity to manage, more chances for bugs. Mobile-first means the simple layout is the default and complexity is only added when the viewport can support it.

3. **Viewport meta tag is required.** Without `<meta name="viewport" content="width=device-width, initial-scale=1">`, mobile browsers render the page at a virtual ~980px width and zoom out, making text unreadably small. This tag is not optional for any responsive page.

4. **CSS custom properties reduce repetition and enable easy theming.** Defining colors, spacing, and font sizes as `--variable` values in `:root` means changes propagate everywhere instantly. This is especially useful for a project where a non-technical contributor might want to tweak the look — they only need to edit a few lines at the top of the file. Custom properties work in all modern browsers (the project's target) and require no build step.

5. **Minimal reset over a full reset library.** A full reset (Eric Meyer's, Normalize.css) is overkill for a single page. A targeted reset covers the essentials:
   ```css
   *, *::before, *::after { box-sizing: border-box; }
   body { margin: 0; font-family: system-ui, sans-serif; line-height: 1.6; }
   img { max-width: 100%; display: block; }
   ```
   This handles the main cross-browser inconsistencies without adding unnecessary rules.

6. **One breakpoint is likely sufficient.** The page is a single column of text. For a content page like this, one breakpoint around 768px is enough: below that, everything stacks and uses full width; above that, content gets a comfortable max-width and centered layout with more generous spacing. A second breakpoint (e.g. 1024px) can be added if needed but is unlikely for this scope.

### Alternatives considered

| Alternative | Why rejected |
|---|---|
| **Desktop-first (`max-width` queries)** | Produces more CSS for this use case. Base styles would include layout rules that then need to be overridden for mobile. More code = more maintenance for a project targeting simplicity. |
| **CSS framework (Tailwind, Bootstrap, etc.)** | Explicitly prohibited by the spec (FR-014). Also violates the constitution's simplicity-first principle and would require a build step (Tailwind) or a large dependency (Bootstrap). |
| **No media queries (fluid-only with `clamp()`)** | `clamp()` for font sizes and widths is a valid modern approach, but it is harder to reason about for a novice contributor. A single `min-width` breakpoint is more readable and debuggable. `clamp()` can be used selectively (e.g. for font sizes) alongside a breakpoint if desired. |
| **Separate CSS files per breakpoint** | Unnecessary complexity for a single page. Multiple `<link>` tags with `media` attributes are harder to maintain and add HTTP requests (irrelevant for `file://`, but still adds cognitive overhead). One file is simpler. |
| **Normalize.css or full CSS reset** | Adds an external dependency or a large block of reset rules. For a single page targeting only modern browsers, a 3–5 line targeted reset covers all practical needs. |

### Recommended CSS file structure (outline)

```css
/* ── Custom Properties ── */
:root {
  --color-bg: #ffffff;
  --color-text: #1a1a1a;
  --color-accent: #0969da;
  --color-surface: #f6f8fa;
  --font-body: system-ui, -apple-system, sans-serif;
  --font-mono: ui-monospace, 'Cascadia Code', 'Consolas', monospace;
  --max-width: 42rem;
  --space-sm: 0.5rem;
  --space-md: 1rem;
  --space-lg: 2rem;
  --space-xl: 3rem;
}

/* ── Reset ── */
*, *::before, *::after { box-sizing: border-box; }
body { margin: 0; font-family: var(--font-body); line-height: 1.6; color: var(--color-text); background: var(--color-bg); }
img { max-width: 100%; display: block; }

/* ── Base (mobile-first, 375px+) ── */
/* ... single-column layout, full-width, compact spacing ... */

/* ── Breakpoint: tablets and up ── */
@media (min-width: 768px) {
  /* ... centered content, wider spacing, larger headings ... */
}
```

---

## Topic 3: Copy-to-clipboard for a code block without a framework

### Decision

**Add a small vanilla JS snippet** that attaches a "Copy" button to the `/speckit.specify` command prompt block. The script should be inline in the HTML (or in a small `<script>` tag at the bottom of the page) — no external JS file needed for this scope.

### Rationale

1. **The target audience is non-technical.** Asking a novice to manually select a multi-line text block and copy it is error-prone — they may miss text, accidentally include surrounding whitespace, or not know the keyboard shortcut. A one-click "Copy" button dramatically reduces friction for the most important call-to-action on the page.

2. **The `navigator.clipboard.writeText()` API is trivial.** The entire implementation is ~15 lines of JS:
   ```js
   document.querySelectorAll('.copy-btn').forEach(btn => {
     btn.addEventListener('click', () => {
       const code = btn.closest('.code-block').querySelector('code').textContent;
       navigator.clipboard.writeText(code).then(() => {
         btn.textContent = 'Copied!';
         setTimeout(() => btn.textContent = 'Copy', 2000);
       });
     });
   });
   ```
   No dependencies, no build step, fully vanilla. The visual feedback ("Copied!") confirms the action, which is important for users who may not trust that a button click did something.

3. **`navigator.clipboard.writeText()` has universal modern browser support.** It works in Chrome 66+, Firefox 63+, Safari 13.1+, Edge 79+ — well within the "modern browsers" target. It requires a secure context (HTTPS or `localhost`), but it **also works on `file://`** in all major browsers. No fallback needed for the project's target audience.

4. **Progressive enhancement.** The prompt block is always visible as selectable text regardless of JS. The copy button is an enhancement — if JS is disabled or fails, the user can still manually copy. The button can be added to the DOM via JS itself (so it doesn't appear if JS is broken), or it can be in the HTML with a `<noscript>`-aware approach.

5. **No external JS file needed.** For a single button on a single page, an inline `<script>` at the bottom of the HTML body is appropriate. Adding a separate `.js` file would be over-engineering. If more JS is added later, it can be extracted to a file at that point.

### Alternatives considered

| Alternative | Why rejected |
|---|---|
| **No copy button (manual select + copy only)** | Workable but creates unnecessary friction for the target audience (non-technical users). The `/speckit.specify` prompt is a multi-line block — selecting it precisely is fiddly on both desktop and mobile. The copy button is specifically called for by the spec (FR-010: "ready-to-copy" prompt). |
| **`document.execCommand('copy')` fallback** | Deprecated API. Still works in browsers but is officially removed from the spec. Not needed since `navigator.clipboard.writeText()` covers all target browsers. Adding it would be dead code for the target audience. |
| **Third-party clipboard library (clipboard.js, etc.)** | Adds an external dependency for a trivial task. Violates the no-frameworks/no-dependencies constraint. The native API is just as simple and has no bundle size. |
| **Separate `script.js` file** | For a single event handler (~15 lines), a separate file adds an extra HTTP request and an extra file to maintain. Not justified until there is more JS on the page. The plan already notes: "No JavaScript file unless a clear need emerges." A `<script>` block at the bottom of `index.html` is sufficient. |
| **CSS-only approach (invisible textarea hack)** | Fragile, accessibility-unfriendly, and more complex than the native Clipboard API. Not a real option for production. |

### Recommended HTML pattern

```html
<div class="code-block">
  <button class="copy-btn" type="button" aria-label="Copy command to clipboard">Copy</button>
  <pre><code>/speckit.specify

I'd like to add a "Concepts" section to the site...
(full prompt text here)</code></pre>
</div>
```

The button is placed before the `<pre>` to allow CSS positioning (e.g. top-right corner of the block) without needing absolute positioning hacks. The `aria-label` ensures screen readers announce the button's purpose.

---

## Summary of decisions

| # | Topic | Decision |
|---|---|---|
| 1 | File structure | `site/` subdirectory with `index.html` and `style.css` |
| 2 | Responsive CSS | Mobile-first, single `style.css`, CSS custom properties, minimal reset, one `min-width` breakpoint |
| 3 | Copy-to-clipboard | Vanilla JS `navigator.clipboard.writeText()` in an inline `<script>`, progressive enhancement |
