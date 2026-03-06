# Research: Concept Pages

**Feature**: 005-concept-pages  
**Date**: 2026-03-06

## 1. Navigation Pattern on Main Page

**Decision**: Use a `<section id="concepts">` with an `<h2>` heading and a `<ul>` of links — not a `<nav>`.

**Rationale**: The existing page structure uses `<section id="...">` with `<h2>` headings for every content block (step-1, step-2, etc.). A new `<section id="concepts">` keeps the page structurally consistent. `<nav>` is intended for major site-wide navigation blocks, not a single content section with links. Using it here would be semantically misleading and dilute its meaning for screen readers.

**Alternatives Considered**:
- `<nav>` element — more appropriate for persistent site-wide navigation; overkill for a content section
- Description list (`<dl>`) — adds complexity; a `<ul>` with descriptive link text is simpler

## 2. Concept Page HTML Template

**Decision**: Minimal boilerplate with a `<nav class="breadcrumb">` for the back-to-home link placed above `<header>`, followed by `<header>`, `<main>`, and `<footer>`.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>[Topic] – Mike's AI Journey</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <nav class="breadcrumb" aria-label="Back to home">
    <a href="index.html">← Home</a>
  </nav>
  <header>
    <h1>[Topic Title]</h1>
    <p>[One-line plain-language summary]</p>
  </header>
  <main>
    <!-- content sections -->
  </main>
  <footer>
    <p>Built with curiosity and a little help from AI.</p>
  </footer>
</body>
</html>
```

**Rationale**: The back-to-home link is navigational, so `<nav>` with `aria-label` is appropriate. Placing it above `<header>` follows the breadcrumb pattern. Using the same `<header>`/`<main>`/`<footer>` structure as the home page ensures CSS reuse. The `<title>` uses "Topic – Site Name" format for tab clarity.

**Alternatives Considered**:
- Back link inside `<header>` — muddies header purpose
- Back link inside `<main>` — buries navigation in content
- Standalone `<a>` without `<nav>` — functional but worse for screen readers

## 3. File Naming Convention

**Decision**: Short, lowercase, URL-friendly filenames as siblings of `index.html`:

| Topic | Filename |
|---|---|
| Git & Version Control | `git.html` |
| GitHub | `github.html` |
| GitHub Copilot & AI Agents | `copilot.html` |
| Spec-Driven Development & spec-kit | `speckit.html` |
| Devcontainers | `devcontainers.html` |
| GitHub Codespaces | `codespaces.html` |
| GitHub Pages | `ghpages.html` |

**Rationale**: URL-friendly, short, descriptive. `ghpages.html` avoids confusion with `github.html`. `speckit.html` keeps the branded name.

**Alternatives Considered**:
- Hyphenated full names (`git-and-version-control.html`) — unnecessarily long
- Subdirectory per concept — adds complexity for no benefit at this scale
- Numbered prefixes — implies ordering that isn't relevant

## 4. CSS Reuse and Additions

**Decision**: Reuse existing `style.css` via `<link rel="stylesheet" href="style.css">`. Add ~15 lines for breadcrumb nav styling.

**New CSS needed**:

```css
.breadcrumb {
  padding: var(--space-md);
  font-size: 0.9rem;
}

.breadcrumb a {
  color: var(--color-muted);
  text-decoration: none;
}

.breadcrumb a:hover,
.breadcrumb a:focus {
  color: var(--color-accent);
  text-decoration: underline;
}

@media (min-width: 768px) {
  .breadcrumb {
    max-width: var(--max-width);
    margin-left: auto;
    margin-right: auto;
    padding-left: var(--space-lg);
    padding-right: var(--space-lg);
  }
}
```

**Rationale**: All files are siblings in `site/`, so relative path works. The existing CSS handles all standard elements. Only the breadcrumb nav is new.

**Alternatives Considered**:
- Separate `concept.css` — unnecessary for ~15 lines
- Inline styles — violates external CSS pattern
- CSS `@import` — extra HTTP request, overkill

## 5. Content Structure per Concept Page

**Decision**: Consistent four-section structure for every concept page:

1. **"What is it?"** — 2–3 paragraphs, plain language, second-person voice
2. **"Think of it like..."** — concrete analogy or practical example
3. **"Why does it matter?"** — connect concept to learner's goals
4. **"Learn more"** — link(s) to official documentation

**Rationale**: Follows "What → Why → Resources" instructional design pattern. Analogies help learners build mental models of unfamiliar concepts. Short paragraphs and direct "you" address improve engagement for novice readers. Concept pages explain *what and why*, not step-by-step instructions (the tutorial handles that).

**Alternatives Considered**:
- FAQ format — presumes reader already has questions
- Long-form essay — too dense for beginners
- Interactive/accordion — adds JS complexity, violates simplicity principle
