# Data Model: Static Landing Page

**Feature Branch**: `001-static-landing-page`  
**Date**: 2026-03-01

## Overview

This feature has no database, API, or persistent storage. The
"data model" describes the content entities rendered on the page
— the structured information that populates each section. These
entities are hard-coded in the HTML.

## Content Entities

### PageSection

Represents a top-level section of the single-page site.

| Field | Type | Description |
|-------|------|-------------|
| id | string | HTML `id` attribute for anchor linking (e.g. `what-is-this`, `concepts`, `getting-started`, `next-steps`, `reference-links`) |
| title | string | Section heading displayed to the visitor |
| order | integer | Display order on the page (1–5) |
| content | HTML | Section body content |

**Instances** (fixed for this feature):

| Order | ID | Title |
|-------|----|-------|
| 1 | `what-is-this` | What is this? |
| 2 | `concepts` | Key Concepts |
| 3 | `getting-started` | Getting Started |
| 4 | `next-steps` | Next Steps |
| 5 | `reference-links` | Reference Links |

---

### ConceptEntry

Represents a single concept in the "Key Concepts" section.

| Field | Type | Description |
|-------|------|-------------|
| name | string | Concept title (e.g. "GitHub Codespaces") |
| description | string | Plain-language explanation, jargon-free |
| externalUrl | URL | Link to an authoritative external reference |
| externalLabel | string | Display text for the link |

**Minimum instances** (per FR-003):

| Name | External reference target |
|------|--------------------------|
| GitHub Codespaces | GitHub Codespaces docs |
| GitHub Copilot & AI Agents | GitHub Copilot docs |
| Spec-Driven Development & spec-kit | spec-kit repo |

---

### GettingStartedStep

Represents one numbered step in the "Getting Started" section.

| Field | Type | Description |
|-------|------|-------------|
| stepNumber | integer | 1-based sequential order |
| title | string | Brief action label |
| explanation | string | What the user is doing and why (plain language) |
| linkUrl | URL (optional) | Action link for this step |
| linkLabel | string (optional) | Display text for the link |

**Instances** (per FR-005, FR-006):

| # | Title | Link target |
|---|-------|-------------|
| 1 | Create a GitHub account | github.com/signup |
| 2 | Sign up for GitHub Copilot Pro (free trial) | github.com/github-copilot/signup |
| 3 | Contact the project owner for repo access | (no link — text instruction) |
| 4 | Fork the repository | (instruction with explanation of "forking") |
| 5 | Open your fork in GitHub Codespaces | (instruction with explanation) |

---

### ReferenceLink

Represents one entry in the "Reference Links" section.

| Field | Type | Description |
|-------|------|-------------|
| label | string | Display text |
| url | URL | External target |
| opensInNewTab | boolean | Always `true` (per FR-015) |

**Minimum count**: 5 (per spec User Story 5).

---

## Relationships

```text
PageSection (1) ──contains──▸ ConceptEntry (3+)     [section: concepts]
PageSection (1) ──contains──▸ GettingStartedStep (5) [section: getting-started]
PageSection (1) ──contains──▸ ReferenceLink (5+)     [section: reference-links]
```

## Validation Rules

- All external URLs MUST use `https://` protocol.
- All external links MUST have `target="_blank"` and
  `rel="noopener noreferrer"` (per FR-015 and security best
  practice).
- GettingStartedStep instances MUST be rendered in `stepNumber`
  order.
- ConceptEntry descriptions MUST NOT contain unexplained jargon
  (per FR-004).

## State Transitions

N/A — all content is static. No user input, no state changes.
