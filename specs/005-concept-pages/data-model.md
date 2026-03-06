# Data Model: Concept Pages

**Feature**: 005-concept-pages  
**Date**: 2026-03-06

## Entities

### Concept Page

A standalone HTML page covering one topic.

| Attribute | Description |
|-----------|-------------|
| `filename` | URL-friendly `.html` filename (e.g., `git.html`) |
| `title` | Display title used in `<h1>` and nav links (e.g., "Git & Version Control") |
| `page_title` | Browser tab title, format: "{title} – Mike's AI Journey" |
| `subtitle` | One-line plain-language summary shown in `<header>` |
| `what_section` | 2–3 paragraphs explaining the concept in plain language, second-person voice |
| `analogy_section` | A concrete, relatable analogy or practical example |
| `why_section` | 1–2 paragraphs connecting the concept to the learner's goals |
| `learn_more_links` | One or more links to official documentation or reputable references |
| `back_link` | Relative link to `index.html` ("← Home") |

### Concept Page Instances

| Filename | Title | External Doc Link(s) |
|----------|-------|---------------------|
| `git.html` | Git & Version Control | https://docs.github.com/en/get-started/using-git |
| `github.html` | GitHub | https://docs.github.com/en/get-started |
| `copilot.html` | GitHub Copilot & AI Agents | https://docs.github.com/en/copilot |
| `speckit.html` | Spec-Driven Development & spec-kit | https://github.com/github/spec-kit |
| `devcontainers.html` | Devcontainers | https://containers.dev/ |
| `codespaces.html` | GitHub Codespaces | https://docs.github.com/en/codespaces |
| `ghpages.html` | GitHub Pages | https://docs.github.com/en/pages |

### Concepts Navigation Section

A section added to `index.html` linking to all concept pages.

| Attribute | Description |
|-----------|-------------|
| `section_id` | `concepts` |
| `heading` | "Concepts" |
| `intro_text` | Brief sentence explaining what the section contains |
| `link_list` | Unordered list of links, one per concept page, using descriptive titles |
| `placement` | After the last step section (`#step-7`), before `#next-steps` |

## Relationships

```text
index.html (Concepts Section)
  ├── links to → git.html
  ├── links to → github.html
  ├── links to → copilot.html
  ├── links to → speckit.html
  ├── links to → devcontainers.html
  ├── links to → codespaces.html
  └── links to → ghpages.html

Each concept page:
  └── links back to → index.html (via breadcrumb "← Home")
```

## Page Ordering on Main Page

The concept links appear in this order (matching the spec's topic list):

1. Git & Version Control
2. GitHub
3. GitHub Copilot & AI Agents
4. Spec-Driven Development & spec-kit
5. Devcontainers
6. GitHub Codespaces
7. GitHub Pages

## Section Ordering within index.html

```text
#what-is-this
#step-1
#step-2
#step-3
#step-4
#step-5
#step-6
#step-7
#concepts        ← NEW
#next-steps
#reference-links
```
