# UI Contract: Static Landing Page

**Feature Branch**: `001-static-landing-page`  
**Date**: 2026-03-01

## Overview

The project's external interface is a single HTML page served as
a static file. This contract defines the page structure, section
order, semantic HTML expectations, and accessibility baseline that
the implementation MUST satisfy.

## Page Structure

The page MUST contain the following sections in this order, each
as a `<section>` element with the specified `id`:

```text
┌─────────────────────────────────┐
│  <header>                       │
│    Site title / page heading    │
│  </header>                      │
├─────────────────────────────────┤
│  <section id="what-is-this">    │
│    "What is this?" — motivation │
│    and learn-by-making framing  │
│  </section>                     │
├─────────────────────────────────┤
│  <section id="concepts">        │
│    Key Concepts — 3+ entries    │
│    each with description + link │
│  </section>                     │
├─────────────────────────────────┤
│  <section id="getting-started"> │
│    Getting Started — 5 numbered │
│    steps (ordered list)         │
│  </section>                     │
├─────────────────────────────────┤
│  <section id="next-steps">      │
│    Next Steps — feature idea,   │
│    /speckit.specify prompt +    │
│    copy button, ask-mode tip    │
│  </section>                     │
├─────────────────────────────────┤
│  <section id="reference-links"> │
│    Reference Links — 5+ items   │
│  </section>                     │
├─────────────────────────────────┤
│  <footer>                       │
│    Minimal footer (optional)    │
│  </footer>                      │
└─────────────────────────────────┘
```

## Semantic HTML Requirements

| Element | Usage |
|---------|-------|
| `<header>` | Page-level header with `<h1>` site title |
| `<main>` | Wraps all `<section>` elements |
| `<section>` | One per page section, with `id` attribute |
| `<h2>` | Section headings |
| `<h3>` | Concept entry headings (inside `#concepts`) |
| `<ol>` | Getting Started steps (ordered list) |
| `<li>` | Each Getting Started step |
| `<a>` | All external links |
| `<pre><code>` | The `/speckit.specify` command prompt block |
| `<button>` | Copy-to-clipboard button |
| `<footer>` | Optional page footer |

## Link Behavior

All external links (`<a>` pointing to external URLs) MUST have:
- `target="_blank"`
- `rel="noopener noreferrer"`

This ensures links open in a new tab (FR-015) and follows
security best practice.

## Copy-to-Clipboard Block

The `/speckit.specify` prompt in the Next Steps section MUST be
wrapped in a `.code-block` container:

```html
<div class="code-block">
  <button class="copy-btn" type="button"
          aria-label="Copy command to clipboard">Copy</button>
  <pre><code>...</code></pre>
</div>
```

Behavior:
- Click → copies `<code>` text content to clipboard.
- Button text changes to "Copied!" for 2 seconds, then reverts.
- Progressive enhancement: if JS fails, the text is still
  selectable and copyable manually.

## Responsive Layout Contract

| Viewport | Behavior |
|----------|----------|
| < 768px (mobile) | Single column, full width, compact spacing |
| ≥ 768px (tablet+) | Centered content column, `max-width: 42rem`, generous spacing |

The HTML MUST include:
```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

## Accessibility Baseline

- All interactive elements (`<a>`, `<button>`) MUST be keyboard
  accessible.
- The copy button MUST have an `aria-label`.
- Heading hierarchy MUST be sequential (`h1` → `h2` → `h3`),
  no skipped levels.
- Color contrast MUST meet WCAG 2.1 AA (4.5:1 for body text,
  3:1 for large text).
- The page MUST not rely solely on color to convey information.

## Tone & Voice

All visitor-facing text MUST use second-person voice ("you")
per FR-016.
