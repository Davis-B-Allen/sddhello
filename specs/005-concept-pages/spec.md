# Feature Specification: Concept Pages

**Feature Branch**: `005-concept-pages`  
**Created**: 2026-03-06  
**Status**: Draft  
**Input**: User description: "Add a Concepts section to the site with individual pages for key topics including Git & version control, GitHub, GitHub Copilot & AI agents, Spec-Driven Development & spec-kit, Devcontainers, GitHub Codespaces, and GitHub Pages. Each page should explain the concept in plain language, include an analogy or practical example, link to official documentation, and include a back-to-home link. The main page should be updated with navigation to each concept page."

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Browse Concept Pages from Home (Priority: P1)

A visitor lands on the main page and sees a clearly labeled "Concepts" navigation section listing all seven topic pages. They click on any topic and are taken to a dedicated page that explains that concept in plain, beginner-friendly language. After reading, they click a "back to home" link to return to the main page.

**Why this priority**: This is the core feature — without navigable concept pages, nothing else matters. It delivers the primary value of expanding the site into a multi-page learning resource.

**Independent Test**: Can be fully tested by opening the main page, clicking each of the seven concept links, confirming each page loads with content, and clicking back to home. Delivers a complete multi-page browsing experience.

**Acceptance Scenarios**:

1. **Given** a visitor is on the main page, **When** they look at the Concepts section, **Then** they see links to all seven concept pages with descriptive titles.
2. **Given** a visitor clicks a concept link on the main page, **When** the page loads, **Then** they see a beginner-friendly explanation of that topic with a heading, body text, and at least one practical example or analogy.
3. **Given** a visitor is reading a concept page, **When** they want to return to the main page, **Then** they click a clearly visible "back to home" link and are taken back to the main page.

---

### User Story 2 - Learn a Concept in Depth (Priority: P1)

A visitor with no technical background opens a concept page and reads through the explanation. The page uses second-person voice ("you"), avoids jargon without explanation, and includes at least one analogy or practical example that makes the concept relatable. Each page also links to official documentation for readers who want to go deeper.

**Why this priority**: The quality and clarity of each concept page is the heart of the feature — if the content is confusing or too technical, the pages fail their purpose.

**Independent Test**: Can be tested by having a non-technical person read any concept page and confirm they understand the topic, can identify the analogy/example, and can find the external documentation link.

**Acceptance Scenarios**:

1. **Given** a visitor with no technical background opens the "Git & Version Control" page, **When** they read the explanation, **Then** the page uses plain language, second-person voice, and includes an analogy (e.g., "like saving different drafts of a document") that makes the concept understandable.
2. **Given** a visitor finishes reading any concept page, **When** they look for more information, **Then** they find at least one link to official documentation or a reputable external reference.
3. **Given** a visitor opens any concept page, **When** they scan the page, **Then** the content uses "you" voice throughout and does not assume prior technical knowledge.

---

### User Story 3 - Consistent Page Design (Priority: P2)

All seven concept pages share a consistent visual layout — same header style, same font, same color scheme, same CSS file — so the site feels unified. The concept pages match the look and feel of the existing main page.

**Why this priority**: Visual consistency makes the site feel professional and trustworthy. It's important, but secondary to having the content exist and be clear.

**Independent Test**: Can be tested by opening each concept page side-by-side with the main page and verifying that heading styles, fonts, colors, and overall layout are consistent.

**Acceptance Scenarios**:

1. **Given** a visitor navigates between the main page and any concept page, **When** they compare the visual styling, **Then** both pages use the same CSS, fonts, colors, and layout patterns.
2. **Given** a visitor opens any concept page, **When** they view the page header, **Then** it includes the page title in a style consistent with the main site heading hierarchy.

---

### Edge Cases

- What happens when a visitor clicks a concept link but the page file is missing? The browser shows a standard 404 error (no custom handling required for a static site).
- What happens when a visitor is on a concept page and clicks "back to home" — does it work regardless of how they arrived? Yes, the link is a simple relative link to `index.html`, not browser-history dependent.
- What happens on very small screens (375px)? Concept pages and the navigation section on the main page should remain readable and usable at mobile widths.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: The main page (`index.html`) MUST include a "Concepts" section containing links to all seven concept pages.
- **FR-002**: The Concepts section on the main page MUST appear between the last tutorial step section and the "Next Steps" section.
- **FR-003**: Each concept link on the main page MUST display a descriptive title for the topic (e.g., "Git & Version Control", "GitHub Copilot & AI Agents").
- **FR-004**: The site MUST include seven individual concept pages, one for each of the following topics:
  1. Git & Version Control
  2. GitHub
  3. GitHub Copilot & AI Agents
  4. Spec-Driven Development & spec-kit
  5. Devcontainers
  6. GitHub Codespaces
  7. GitHub Pages
- **FR-005**: Each concept page MUST explain the topic in plain language using second-person voice ("you") and MUST NOT assume prior technical knowledge.
- **FR-006**: Each concept page MUST include at least one practical example or analogy to make the concept relatable.
- **FR-007**: Each concept page MUST include at least one link to official documentation or a reputable external reference for the topic.
- **FR-008**: Each concept page MUST include a clearly visible "back to home" link that navigates to the main page.
- **FR-009**: All concept pages MUST use the same CSS stylesheet as the main page to maintain visual consistency.
- **FR-010**: The Concepts section on the main page and all concept pages MUST be readable and usable at a viewport width of 375px (mobile).
- **FR-011**: Concept page files MUST be placed inside the `site/` directory.
- **FR-012**: Each concept page MUST include a page title (`<title>` element) that reflects the topic name.

### Key Entities

- **Concept Page**: A standalone HTML page covering one topic. Key attributes: topic title, plain-language explanation, analogy/example, external documentation link, back-to-home navigation link.
- **Concepts Navigation Section**: A section on the main page listing all concept pages with links. Key attributes: section heading, list of concept links with descriptive titles.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: All seven concept pages are reachable from the main page via working links, with zero broken links.
- **SC-002**: Each concept page contains a heading, at least two paragraphs of explanation, at least one analogy or example, and at least one external documentation link.
- **SC-003**: A non-technical reader can identify what each concept means after reading its page (content is written at a level accessible to someone with no programming experience).
- **SC-004**: Every concept page includes a working "back to home" link that returns the visitor to the main page.
- **SC-005**: All concept pages render correctly and are fully readable on a 375px-wide viewport.
- **SC-006**: Visual styling of concept pages is consistent with the existing main page (same fonts, colors, layout patterns).

## Assumptions

- The site remains a static HTML/CSS site with no build tools or frameworks required.
- Concept pages will be individual `.html` files in the `site/` directory (e.g., `site/git.html`, `site/github.html`).
- The existing CSS file (`site/style.css`) provides sufficient styling; minimal additions may be needed for the navigation section.
- No search functionality or inter-concept-page navigation (e.g., next/previous) is needed; the back-to-home link is sufficient for navigation.
- The "Concepts" section on the main page is a simple list of links, not a complex card grid or interactive component.
