# Research: Tutorial Site Redesign

**Feature**: 004-tutorial-redesign  
**Date**: 2026-03-04

## 1. Objectives Block — HTML/CSS Pattern

**Decision**: Use `<aside class="objectives" aria-label="Objectives for this step">` for each Objectives block.

**Rationale**: `<aside>` is the correct semantic element for supplementary/navigational callout content that is tangentially related to the main tutorial text. It provides proper semantics for screen readers and avoids polluting the document outline (unlike an extra `<h3>`). The `aria-label` attribute gives each block an explicit landmark label.

**Alternatives considered**:
- `<blockquote>` — semantically incorrect (intended for quoted text from another source)
- `<details>/<summary>` — implies collapsible/optional content, which is undesired
- `<div>` — semantically neutral; `<aside>` is more meaningful
- `<section>` — would imply a standalone document section, too heavyweight for a callout within a step

**CSS approach**: Left-accent border with surface background, matching existing design tokens:
- `background: var(--color-surface)` — matches `pre` and `.code-block`
- `border-left: 4px solid var(--color-accent)` — standard callout affordance
- `border-radius: 6px` — matches existing `pre` and `.code-block`
- Keywords sub-section separated by `border-top: 1px solid var(--color-border)`

**HTML structure**:
```html
<aside class="objectives" aria-label="Objectives for this step">
  <p class="objectives-heading">Objectives for this step</p>
  <ul>
    <li>Goal 1</li>
    <li>Goal 2</li>
  </ul>
  <p class="keywords">
    <strong>Topics you may need help with:</strong> keyword1, keyword2, keyword3
  </p>
</aside>
```

## 2. Copy-to-Clipboard Integration

**Decision**: Reuse the existing `.code-block` / `.copy-btn` pattern unchanged. No JS modifications needed.

**Rationale**: The existing script at the bottom of `index.html` uses `document.querySelectorAll('.copy-btn')` to attach click handlers to all copy buttons at page load. Any new `.code-block` containers with `.copy-btn` buttons added to the HTML will be picked up automatically as long as they use the same class names and structure.

**Alternatives considered**:
- Event delegation on a parent element — unnecessary since the script already handles all buttons at load time
- A separate JS module — violates Simplicity-First principle; current inline approach is sufficient

**Existing pattern** (from `site/index.html`):
```html
<div class="code-block">
  <button class="copy-btn" type="button" aria-label="Copy to clipboard">Copy</button>
  <pre><code>Text to copy</code></pre>
</div>
```

## 3. Section ID Scheme

**Decision**: Use `id="step-1"` through `id="step-7"` for each step section. Remove `id="concepts"` and `id="getting-started"`.

**Rationale**: Consistent, predictable, and allows direct linking (e.g., `index.html#step-3`). Numeric scheme mirrors the step numbering in the headings. Removing old IDs avoids stale anchor references.

**Alternatives considered**:
- Slug-based IDs (e.g., `id="create-github-account"`) — longer, harder to remember, and the step number is a more natural anchor for a sequential tutorial
- Keeping `id="getting-started"` on a wrapper — there is no wrapper in the new design

## 4. Copilot Web Chat Repo Access

**Decision**: Reference `https://github.com/Davis-B-Allen/sddhello` in prompt text and instruct users the Copilot can read the repo.

**Rationale**: GitHub Copilot's web chat at `github.com/copilot`, when in Ask Mode, can be directed to read public GitHub repositories by including the repo URL in the conversation. This is a documented capability. The prompt text instructs the user to mention the repo URL, which is sufficient for Copilot to access and understand the tutorial content.

**Alternatives considered**:
- Using `@github` mention syntax — this is a VS Code extension feature, not available in the web chat
- Providing the full tutorial text in the prompt — unnecessarily long; the repo URL approach is more elegant and scalable

## 5. Step Section HTML Pattern

**Decision**: Each step is a `<section id="step-N">` containing an `<h2>` heading. Steps 4–7 include the Objectives `<aside>` as the first child after the heading.

**Rationale**: Using `<section>` elements (rather than `<li>` elements inside an `<ol>`) matches the existing site pattern where each major content area is a `<section>` (e.g., `#what-is-this`, `#next-steps`, `#reference-links`). Each step is a first-class page section, not a list item.

**HTML skeleton for Steps 1–3 (unaided)**:
```html
<section id="step-N">
  <h2>Step N: Title</h2>
  <p>Friendly tutorial text...</p>
  <!-- Step 3 also includes a .code-block with prompt -->
</section>
```

**HTML skeleton for Steps 4–7 (Copilot-assisted)**:
```html
<section id="step-N">
  <h2>Step N: Title</h2>
  <aside class="objectives" aria-label="Objectives for this step">
    <p class="objectives-heading">Objectives for this step</p>
    <ul><li>...</li></ul>
    <p class="keywords"><strong>Topics you may need help with:</strong> ...</p>
  </aside>
  <p>Friendly intro paragraph...</p>
  <p>Copy the text block below and paste it into a new chat...</p>
  <div class="code-block">
    <button class="copy-btn" type="button" aria-label="Copy to clipboard">Copy</button>
    <pre><code>Copilot prompt text...</code></pre>
  </div>
  <p>Walkthrough text continues...</p>
</section>
```
