# UI Contract: Concept Pages

**Feature**: 005-concept-pages  
**Date**: 2026-03-06

## Main Page: Concepts Navigation Section

### Section Placement

Insert `<section id="concepts">` in `index.html` between `</section><!-- end step-7 -->` and `<section id="next-steps">`.

### HTML Structure

```html
<section id="concepts">
  <h2>Concepts</h2>
  <p>
    Want to understand the tools you're using? These pages explain each
    concept in plain language.
  </p>
  <ul>
    <li><a href="git.html">Git & Version Control</a></li>
    <li><a href="github.html">GitHub</a></li>
    <li><a href="copilot.html">GitHub Copilot & AI Agents</a></li>
    <li><a href="speckit.html">Spec-Driven Development & spec-kit</a></li>
    <li><a href="devcontainers.html">Devcontainers</a></li>
    <li><a href="codespaces.html">GitHub Codespaces</a></li>
    <li><a href="ghpages.html">GitHub Pages</a></li>
  </ul>
</section>
```

### Styling

No new CSS required — the existing `section h2`, `p`, `ul`, `ul li`, and `a` rules apply.

---

## Concept Page Template

### HTML Boilerplate

Every concept page follows this structure:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>{Topic Title} – Mike's AI Journey</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <nav class="breadcrumb" aria-label="Back to home">
    <a href="index.html">← Home</a>
  </nav>

  <header>
    <h1>{Topic Title}</h1>
    <p>{One-line plain-language summary}</p>
  </header>

  <main>
    <section id="what-is-it">
      <h2>What is {topic}?</h2>
      <p>{2–3 paragraphs, plain language, second-person voice}</p>
    </section>

    <section id="analogy">
      <h2>Think of it like...</h2>
      <p>{Concrete, relatable analogy or practical example}</p>
    </section>

    <section id="why-it-matters">
      <h2>Why does it matter?</h2>
      <p>{1–2 paragraphs connecting concept to learner's goals}</p>
    </section>

    <section id="learn-more">
      <h2>Learn more</h2>
      <ul>
        <li><a href="{official-doc-url}" target="_blank" rel="noopener noreferrer">{Link text} →</a></li>
      </ul>
    </section>
  </main>

  <footer>
    <p>Built with curiosity and a little help from AI.</p>
  </footer>
</body>
</html>
```

### Content Requirements per Page

| Page | `<h1>` Title | Subtitle | Analogy Theme | Primary Doc Link |
|------|-------------|----------|---------------|------------------|
| `git.html` | Git & Version Control | Track changes to your code like saving drafts of a document. | Saving drafts / undo history | https://docs.github.com/en/get-started/using-git |
| `github.html` | GitHub | A home for your code — and a place to collaborate with others. | Google Drive for code | https://docs.github.com/en/get-started |
| `copilot.html` | GitHub Copilot & AI Agents | An AI assistant that helps you write code and learn along the way. | A knowledgeable coding buddy | https://docs.github.com/en/copilot |
| `speckit.html` | Spec-Driven Development & spec-kit | A structured way to plan before you build — like a blueprint for software. | Architectural blueprint | https://github.com/github/spec-kit |
| `devcontainers.html` | Devcontainers | A pre-configured workspace so you don't have to set anything up yourself. | Moving into a fully furnished apartment | https://containers.dev/ |
| `codespaces.html` | GitHub Codespaces | Your development environment, running in the cloud, right in your browser. | A virtual workshop in the cloud | https://docs.github.com/en/codespaces |
| `ghpages.html` | GitHub Pages | Publish a website for free, straight from your code repository. | One-click publishing | https://docs.github.com/en/pages |

### New CSS Rules Required

Add to `site/style.css`:

```css
/* ── Breadcrumb Navigation ── */
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

### Responsive Behavior

- All concept pages inherit the existing responsive rules for `header`, `main`, `footer` (centered at `max-width: 42rem` on screens ≥768px).
- The `.breadcrumb` responsive rule mirrors the existing pattern.
- At 375px, all content is single-column with `var(--space-md)` padding — no overflow.

### Accessibility

- `<nav class="breadcrumb" aria-label="Back to home">` provides screen reader context.
- All external links use `target="_blank" rel="noopener noreferrer"`.
- Semantic section IDs (`what-is-it`, `analogy`, `why-it-matters`, `learn-more`) for in-page structure.
- All pages use `<html lang="en">`.
