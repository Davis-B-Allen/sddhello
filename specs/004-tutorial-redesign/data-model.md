# Data Model: Tutorial Site Redesign

**Feature**: 004-tutorial-redesign  
**Date**: 2026-03-04

## Overview

This feature modifies a static HTML page. There is no database, API, or persistent state. The "data model" describes the structural entities in the HTML document and their relationships.

## Entities

### 1. Page

The single HTML document (`site/index.html`).

| Attribute | Type | Description |
|-----------|------|-------------|
| title | string | Page `<title>` — unchanged |
| sections | Section[] | Ordered list of top-level content sections |

### 2. Section

A top-level `<section>` element within `<main>`.

| Attribute | Type | Description |
|-----------|------|-------------|
| id | string | Unique anchor ID (e.g., `what-is-this`, `step-1`, `next-steps`) |
| heading | string | `<h2>` text content |
| type | enum | `intro` · `step-unaided` · `step-onboarding` · `step-assisted` · `info` |
| content | HTML | Section body content |

**Ordering** (top to bottom):
1. `what-is-this` — type `intro` (unchanged)
2. `step-1` — type `step-unaided`
3. `step-2` — type `step-unaided`
4. `step-3` — type `step-onboarding`
5. `step-4` — type `step-assisted`
6. `step-5` — type `step-assisted`
7. `step-6` — type `step-assisted`
8. `step-7` — type `step-assisted`
9. `next-steps` — type `info` (unchanged)
10. `reference-links` — type `info` (unchanged)

**Removed sections**: `concepts` (Key Concepts), `getting-started` (Getting Started wrapper)

### 3. Objectives Block

An `<aside class="objectives">` element inside a `step-assisted` section. Present only in Steps 4–7.

| Attribute | Type | Description |
|-----------|------|-------------|
| heading | string | Always "Objectives for this step" |
| goals | string[] | Bulleted list of goals (≥2 items) |
| keywords | string[] | "Topics you may need help with" terms (≥2 items) |

### 4. Copilot Prompt Block

A `<div class="code-block">` element containing a copy-enabled prompt. Present in Steps 3–7.

| Attribute | Type | Description |
|-----------|------|-------------|
| prompt_text | string | Pre-written text for the user to paste into Copilot |
| step_number | integer | The step number referenced in the prompt (3–7) |
| repo_url | string | Always `https://github.com/Davis-B-Allen/sddhello` |
| copy_button | boolean | Always `true` — rendered as `.copy-btn` |

## Relationships

```
Page
 └── Section[] (ordered, 10 sections total)
      ├── type: step-assisted (Steps 4–7)
      │    ├── Objectives Block (exactly 1)
      │    │    ├── goals[] (≥2)
      │    │    └── keywords[] (≥2)
      │    └── Copilot Prompt Block (exactly 1)
      ├── type: step-onboarding (Step 3)
      │    └── Copilot Prompt Block (exactly 1, no Objectives Block)
      └── type: step-unaided | intro | info
           └── (no Objectives Block, no Copilot Prompt Block)
```

## Validation Rules

- Every `step-assisted` section MUST contain exactly one Objectives Block and exactly one Copilot Prompt Block.
- Every `step-onboarding` section MUST contain exactly one Copilot Prompt Block and MUST NOT contain an Objectives Block.
- Every `step-unaided` section MUST NOT contain an Objectives Block or a Copilot Prompt Block.
- Every Objectives Block MUST have ≥2 goal items and ≥2 keyword items.
- Every Copilot Prompt Block MUST reference the repo URL and the correct step number.
- Section IDs MUST be unique across the page.
- The `concepts` and `getting-started` section IDs MUST NOT exist in the final page.

## State Transitions

N/A — static page with no runtime state changes.
