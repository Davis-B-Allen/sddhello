# UI Contract: Tutorial Site Redesign

**Feature**: 004-tutorial-redesign  
**Date**: 2026-03-04

## Overview

This contract defines the HTML section structure, CSS class conventions, and content patterns for the redesigned tutorial page. It serves as the implementer's reference for what the final page must contain.

## Page Section Map

The `<main>` element contains the following sections in order. Sections marked ∅ are **removed** from the current page.

| # | Section ID | `<h2>` Heading | Type | Objectives Block | Prompt Block | Changed? |
|---|-----------|----------------|------|:---:|:---:|:---:|
| 1 | `what-is-this` | What is this? | intro | — | — | No |
| ∅ | ~~`concepts`~~ | ~~Key Concepts~~ | ~~removed~~ | — | — | **Deleted** |
| ∅ | ~~`getting-started`~~ | ~~Getting Started~~ | ~~removed~~ | — | — | **Deleted** |
| 2 | `step-1` | Step 1: Create a GitHub account | step-unaided | — | — | **New** |
| 3 | `step-2` | Step 2: Sign up for the GitHub Copilot Pro free trial | step-unaided | — | — | **New** |
| 4 | `step-3` | Step 3: Meet your AI assistant | step-onboarding | — | ✓ | **New** |
| 5 | `step-4` | Step 4: Fork the repository | step-assisted | ✓ | ✓ | **New** |
| 6 | `step-5` | Step 5: Open your fork in GitHub Codespaces | step-assisted | ✓ | ✓ | **New** |
| 7 | `step-6` | Step 6: Preview the site locally | step-assisted | ✓ | ✓ | **New** |
| 8 | `step-7` | Step 7: Publish your site with GitHub Pages | step-assisted | ✓ | ✓ | **New** |
| 9 | `next-steps` | Next Steps | info | — | — | No |
| 10 | `reference-links` | Reference Links | info | — | — | No |

## Section Templates

### Template A: Unaided Step (Steps 1–2)

```html
<section id="step-N">
  <h2>Step N: Title</h2>
  <p>Brief explanation in friendly tone...</p>
  <p><a href="URL" target="_blank" rel="noopener noreferrer">Call-to-action link →</a></p>
</section>
```

### Template B: Onboarding Step (Step 3)

```html
<section id="step-3">
  <h2>Step 3: Meet your AI assistant</h2>
  <p>Explanation of what GitHub Copilot is...</p>
  <p>How to access github.com/copilot...</p>
  <p>Explanation of Ask Mode...</p>
  <p>Explanation of pointing Copilot at the repo URL...</p>
  <p>Establishing the interaction pattern for remaining steps...</p>
  <p>Copy instruction text...</p>
  <div class="code-block">
    <button class="copy-btn" type="button" aria-label="Copy to clipboard">Copy</button>
    <pre><code>I am following along with a tutorial on a website I found. The repo for the site can be found at https://github.com/Davis-B-Allen/sddhello and the page with the tutorial is found in the site/ folder. I am currently working through step 3. I'd like you to read the tutorial so you understand its context. And then, just so I know you've understood it, can you please tell me the name of the next step of the tutorial? Once you confirm that, I'll be ready to move on to the next step (since I know you'll be here to help me).</code></pre>
  </div>
  <p>Confirmation text: "If your Copilot assistant confirmed that the next step is 'Step 4: Fork the repository', you're ready to move on..."</p>
</section>
```

### Template C: Copilot-Assisted Step (Steps 4–7)

```html
<section id="step-N">
  <h2>Step N: Title</h2>

  <!-- Objectives Block -->
  <aside class="objectives" aria-label="Objectives for this step">
    <p class="objectives-heading">Objectives for this step</p>
    <ul>
      <li>Goal 1</li>
      <li>Goal 2</li>
      <!-- ≥2 goal items -->
    </ul>
    <p class="keywords">
      <strong>Topics you may need help with:</strong> keyword1, keyword2
      <!-- ≥2 keywords -->
    </p>
  </aside>

  <!-- Friendly intro -->
  <p>Short colloquial intro paragraph...</p>

  <!-- Copilot prompt instruction -->
  <p>Copy the text block below and paste it into a new chat with your
  GitHub Copilot assistant, in "Ask Mode". You can access your Copilot
  at <a href="https://github.com/copilot" ...>github.com/copilot</a>.</p>

  <!-- Copilot prompt block -->
  <div class="code-block">
    <button class="copy-btn" type="button" aria-label="Copy to clipboard">Copy</button>
    <pre><code>I am following along with a tutorial on a website I found. The repo for the site can be found at https://github.com/Davis-B-Allen/sddhello and the page with the tutorial is found in the site/ folder. I am about to start step [N] and I would like you to advise me if I get stuck or need help. So I'd like you to read the tutorial in full, and step [N] in particular, and await any questions I might have. Can you please do that?</code></pre>
  </div>

  <!-- Walkthrough content -->
  <p>Expanded walkthrough text in colloquial tone...</p>
  <!-- Preserve substantive content from original step -->
</section>
```

## CSS Classes

| Class | Element | Purpose |
|-------|---------|---------|
| `.objectives` | `<aside>` | Objectives block container — surface bg, left accent border |
| `.objectives-heading` | `<p>` | Bold heading text "Objectives for this step" — accent colored |
| `.keywords` | `<p>` | Keywords sub-section — muted text, top border separator |
| `.code-block` | `<div>` | Copy-enabled block container (existing) |
| `.copy-btn` | `<button>` | Copy-to-clipboard button (existing) |

## New CSS Rules Required

```css
/* ── Objectives Callout ── */
.objectives {
  background: var(--color-surface);
  border: 1px solid var(--color-border);
  border-left: 4px solid var(--color-accent);
  border-radius: 6px;
  padding: var(--space-md);
  margin-bottom: var(--space-lg);
}

.objectives .objectives-heading {
  margin: 0 0 var(--space-sm);
  font-size: 1rem;
  font-weight: 600;
  color: var(--color-accent);
}

.objectives ul {
  margin: 0 0 var(--space-sm);
  padding-left: var(--space-lg);
}

.objectives ul li {
  margin-bottom: var(--space-xs);
}

.objectives .keywords {
  margin: var(--space-sm) 0 0;
  padding-top: var(--space-sm);
  border-top: 1px solid var(--color-border);
  font-size: 0.9rem;
  color: var(--color-muted);
}
```

## Content Mapping: Original Steps → New Steps

| Original Step | Original Title | New Step | New Title |
|:---:|---|:---:|---|
| 1 | Create a GitHub account | 1 | Step 1: Create a GitHub account |
| 2 | Sign up for the GitHub Copilot Pro free trial | 2 | Step 2: Sign up for the GitHub Copilot Pro free trial |
| — | *(new)* | 3 | Step 3: Meet your AI assistant |
| 3 | Fork the repository | 4 | Step 4: Fork the repository |
| 4 | Open your fork in GitHub Codespaces | 5 | Step 5: Open your fork in GitHub Codespaces |
| 5 | Preview the site locally | 6 | Step 6: Preview the site locally |
| 6 | Publish your site with GitHub Pages | 7 | Step 7: Publish your site with GitHub Pages |

## Objectives Block Content per Step

### Step 4: Fork the repository
- **Goals**: Create your own copy of the project on GitHub; Understand what "forking" means and why it's useful
- **Keywords**: repository, fork, GitHub, personal copy, upstream

### Step 5: Open your fork in GitHub Codespaces
- **Goals**: Launch a cloud development environment from your fork; Get familiar with the VS Code editor in the browser
- **Keywords**: Codespaces, cloud development environment, VS Code, browser IDE, devcontainer

### Step 6: Preview the site locally
- **Goals**: Run a local web server to see the tutorial site in action; Understand how to use the terminal and preview tools
- **Keywords**: terminal, local server, npx serve, port forwarding, preview

### Step 7: Publish your site with GitHub Pages
- **Goals**: Enable GitHub Pages on your fork; Deploy the site to a public URL; Understand the GitHub Actions workflow
- **Keywords**: GitHub Pages, deployment, GitHub Actions, workflow, static hosting, public URL

## Invariants

- The `<script>` block at the end of `<body>` MUST remain unchanged (copy-to-clipboard handler).
- The `<header>`, `<footer>`, and `#what-is-this` / `#next-steps` / `#reference-links` sections MUST remain unchanged.
- All new `.code-block` elements MUST use the same markup pattern as the existing one in `#next-steps`.
- The page MUST NOT reference a `#concepts` or `#getting-started` anchor after redesign.
