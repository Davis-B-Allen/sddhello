# Feature Specification: Tutorial Site Redesign — Step-by-Step Copilot-Assisted Format

**Feature Branch**: `004-tutorial-redesign`  
**Created**: 2026-03-04  
**Status**: Draft  
**Input**: User description: "Redesign the tutorial site to replace the Key Concepts section and single Getting Started list with individual step sections, introduce a new Copilot onboarding step, and embed AI-assisted prompts into steps 4–7."

## Assumptions

- The tutorial site is a single static HTML page ([site/index.html](site/index.html)) with accompanying CSS ([site/style.css](site/style.css)).
- The "Next Steps" section and "Reference Links" section at the bottom of the page are out of scope for this feature and will remain unchanged.
- The site's existing visual styling (CSS) will be preserved; any new HTML elements (e.g., Objectives blocks, copy-enabled code blocks) will reuse existing styles or receive minimal new CSS that is consistent with the current design.
- The repository URL referenced in Copilot prompt blocks is `https://github.com/Davis-B-Allen/sddhello`.
- The Copilot web interface URL is `github.com/copilot`.
- "Ask Mode" refers to the default conversational mode when chatting with GitHub Copilot through the web UI.
- The copy-to-clipboard functionality for code blocks already exists on the page and will be reused for new prompt blocks.

## User Scenarios & Testing *(mandatory)*

### User Story 1 — Remove Key Concepts section and restructure Getting Started into individual steps (Priority: P1)

A first-time visitor arrives at the tutorial page. Instead of encountering a "Key Concepts" section that front-loads terminology, they see the tutorial proceed directly from the introductory "What is this?" section into clearly numbered step sections. Each step is its own titled section ("Step 1: …", "Step 2: …", etc.), replacing the single numbered list inside the old "Getting Started" section. The visitor can read through the steps sequentially, and concepts are introduced naturally within the step where they become relevant.

**Why this priority**: This is the foundational structural change. All other stories depend on the page being reorganized into individual step sections first.

**Independent Test**: Load the redesigned page and confirm that (a) no "Key Concepts" section is present, (b) no single "Getting Started" section wrapping a numbered list is present, and (c) the page contains seven individual step sections labeled "Step 1" through "Step 7" with appropriate titles.

**Acceptance Scenarios**:

1. **Given** a visitor loads the tutorial page, **When** they scroll past the introductory section, **Then** there is no "Key Concepts" section.
2. **Given** a visitor loads the tutorial page, **When** they look for the steps, **Then** they see seven individual sections titled "Step 1: Create a GitHub account", "Step 2: Sign up for the GitHub Copilot Pro free trial", "Step 3: Meet your AI assistant", "Step 4: Fork the repository", "Step 5: Open your fork in GitHub Codespaces", "Step 6: Preview the site locally", and "Step 7: Publish your site with GitHub Pages".
3. **Given** a visitor loads the tutorial page, **When** they view the page source or rendered content, **Then** there is no `<section id="concepts">` element and no `<section id="getting-started">` wrapping a single ordered list.

---

### User Story 2 — New "Step 3: Meet your AI assistant" onboarding step (Priority: P1)

After completing Steps 1 and 2 (creating a GitHub account and signing up for Copilot Pro), the visitor reaches Step 3. This step introduces GitHub Copilot, explains how to navigate to the web-based chat interface, explains "Ask Mode", and establishes the pattern of pasting prompt blocks into Copilot for the remainder of the tutorial. The step concludes with a copy-enabled prompt block the visitor pastes into Copilot. When Copilot confirms it understands the tutorial and tells the user the name of the next step, the visitor knows their assistant is ready.

**Why this priority**: This step is the bridge between unaided steps (1–2) and Copilot-assisted steps (4–7). Without it, visitors will not understand the interaction pattern used in all subsequent steps.

**Independent Test**: Load the page and read Step 3. Confirm it explains Copilot, links to `github.com/copilot`, explains Ask Mode, and contains a copy-enabled prompt block with the specified verification prompt text. Confirm the section does NOT contain an "Objectives block" (since it is an unaided step, like Steps 1 and 2).

**Acceptance Scenarios**:

1. **Given** a visitor reads Step 3, **When** they look for guidance on accessing Copilot, **Then** they see instructions directing them to `github.com/copilot`.
2. **Given** a visitor reads Step 3, **When** they look for an explanation of Ask Mode, **Then** they find a clear description of what Ask Mode is and how they will use it.
3. **Given** a visitor reads Step 3, **When** they reach the end of the step, **Then** they see a copy-enabled code block containing a prompt that asks Copilot to read the tutorial and confirm the name of the next step.
4. **Given** a visitor has pasted the prompt into Copilot and receives a response naming "Step 4: Fork the repository", **When** they read the follow-up text on the page, **Then** they see confirmation text telling them they are ready to move on.

---

### User Story 3 — Objectives blocks and Copilot prompt blocks for Steps 4–7 (Priority: P1)

For each of Steps 4 through 7, the visitor sees an "Objectives for this step" block at the top of the section. This block contains bullet points explaining what they will accomplish and a "Topics you may need help with" sub-section listing relevant keywords. After the Objectives block, a short friendly paragraph introduces the task, followed by a copy-enabled prompt block instructing them to paste a message into their Copilot chat. After the prompt block, the walkthrough continues in a colloquial, friendly tone, expanding on the objectives and guiding the visitor through the step.

**Why this priority**: This is the core pedagogical pattern for the Copilot-assisted portion of the tutorial and applies to all remaining steps.

**Independent Test**: For each of Steps 4, 5, 6, and 7, verify: (a) an Objectives block is present at the top of the section, (b) the Objectives block contains goal bullet points and a "Topics you may need help with" keywords list, (c) a copy-enabled prompt block is present with the correct step number and repo URL, and (d) the walkthrough text after the prompt block is written in a friendly, informal tone.

**Acceptance Scenarios**:

1. **Given** a visitor reads Step 4, **When** they view the top of the section, **Then** they see an Objectives block with bullet points about forking and a keywords list.
2. **Given** a visitor reads any of Steps 4–7, **When** they look for a prompt block, **Then** they find a copy-enabled code block containing a prompt asking Copilot to read the tutorial and be ready to help with that specific step number.
3. **Given** a visitor reads Step 5, **When** they view the Objectives block, **Then** the keywords list includes terms like "Codespaces", "cloud development environment", and "VS Code".
4. **Given** a visitor reads any of Steps 4–7, **When** they read the text after the prompt block, **Then** the tone is informal and friendly rather than formal or academic.

---

### User Story 4 — Preserve existing content and functionality outside the redesign scope (Priority: P2)

The "What is this?" introductory section, the "Next Steps" section, the "Reference Links" section, the copy-to-clipboard functionality, and the site's overall visual appearance remain unchanged.

**Why this priority**: Ensuring nothing outside scope is broken is important, but this is a verification concern rather than new feature work.

**Independent Test**: Load the page and verify (a) "What is this?" section text is unchanged, (b) "Next Steps" section text is unchanged, (c) "Reference Links" section is unchanged, (d) copy buttons work on all code blocks (old and new), and (e) the page styling is visually consistent with the current design.

**Acceptance Scenarios**:

1. **Given** a visitor loads the redesigned page, **When** they read the "What is this?" section, **Then** its content is identical to the current version.
2. **Given** a visitor loads the redesigned page, **When** they click any "Copy" button on a code/prompt block, **Then** the block's text is copied to their clipboard and the button text changes to "Copied!" temporarily.
3. **Given** a visitor loads the redesigned page, **When** they scroll to "Next Steps" and "Reference Links", **Then** those sections are present and unchanged.

---

### Edge Cases

- What if the visitor does not yet have Copilot access when they reach Step 3? The step should clearly state that Steps 1 and 2 must be completed first and should link back to the Copilot signup as a reminder.
- What if the visitor's Copilot session does not confirm the name of the next step correctly in Step 3? The tutorial text should reassure the visitor that they can try the prompt again and that slight wording variations in Copilot's response are fine as long as it mentions "Step 4" or "Fork the repository".
- What if the copy-to-clipboard button does not work (e.g., the visitor is on a browser that does not support the Clipboard API)? The prompt block text should still be visible and selectable so the visitor can manually copy it.

## Requirements *(mandatory)*

### Functional Requirements

#### Structure & Navigation

- **FR-001**: The page MUST NOT contain a "Key Concepts" section.
- **FR-002**: The page MUST NOT contain a single "Getting Started" section wrapping all steps in one ordered list.
- **FR-003**: The page MUST present seven individual step sections, each with its own heading following the pattern "Step N: [Title]".
- **FR-004**: The seven steps MUST be titled, in order: "Step 1: Create a GitHub account", "Step 2: Sign up for the GitHub Copilot Pro free trial", "Step 3: Meet your AI assistant", "Step 4: Fork the repository", "Step 5: Open your fork in GitHub Codespaces", "Step 6: Preview the site locally", "Step 7: Publish your site with GitHub Pages".

#### Steps 1 and 2 — Unaided Steps

- **FR-005**: Step 1 MUST provide a brief explanation of GitHub and a link to `https://github.com/signup`.
- **FR-006**: Step 2 MUST provide a brief explanation of what Copilot Pro gives the user and a link to `https://github.com/github-copilot/signup`.
- **FR-007**: Steps 1 and 2 MUST NOT contain an "Objectives block" or a Copilot prompt code block.

#### Step 3 — Copilot Onboarding Step

- **FR-008**: Step 3 MUST explain what GitHub Copilot is in beginner-friendly language.
- **FR-009**: Step 3 MUST tell the visitor how to access the Copilot web chat at `github.com/copilot`.
- **FR-010**: Step 3 MUST explain "Ask Mode" and establish that the visitor will use it for subsequent steps.
- **FR-011**: Step 3 MUST introduce the concept of pointing Copilot at the tutorial's GitHub repository URL so it can understand the tutorial context.
- **FR-012**: Step 3 MUST NOT contain an "Objectives block" (it follows the same unaided pattern as Steps 1 and 2).
- **FR-013**: Step 3 MUST end with a copy-enabled code block containing a prompt that asks Copilot to read the tutorial and confirm the name of the next step.
- **FR-014**: Step 3 MUST include follow-up text after the prompt block confirming that if Copilot responds with "Step 4: Fork the repository", the visitor is ready to move on.

#### Steps 4–7 — Copilot-Assisted Steps

- **FR-015**: Each of Steps 4, 5, 6, and 7 MUST begin with a clearly delineated "Objectives for this step" block.
- **FR-016**: Each Objectives block MUST contain a bulleted list of goals for the step.
- **FR-017**: Each Objectives block MUST contain a "Topics you may need help with" sub-section listing relevant keywords/concepts for that step.
- **FR-018**: After the Objectives block, each step MUST have a short introductory paragraph in a colloquial, friendly tone.
- **FR-019**: After the introductory paragraph, each step MUST have an instructional element telling the visitor to copy the following text block and paste it into a new Copilot chat in Ask Mode at `github.com/copilot`.
- **FR-020**: Each step (4–7) MUST contain a copy-enabled code block with a prompt that references the repo URL (`https://github.com/Davis-B-Allen/sddhello`), identifies the tutorial location (`site/` folder), and states the current step number.
- **FR-021**: After the code block, each step MUST continue with colloquial walkthrough text that expands on the goals from the Objectives block.
- **FR-022**: The walkthrough content for Steps 4–7 MUST preserve the substantive instructional content from the corresponding original steps (3–6), including relevant links, sub-steps, and explanations, adapted into the new format.

#### Content Tone & Concepts

- **FR-023**: Key concepts (forking, Codespaces, GitHub Pages, etc.) MUST be introduced inline within the step where they first become relevant, not in a separate front-loaded section.
- **FR-024**: All walkthrough text in Steps 3–7 MUST use a friendly, informal, second-person tone ("you").

#### Copy-to-Clipboard

- **FR-025**: Every Copilot prompt code block MUST have a visible "Copy" button that copies the block's text content to the visitor's clipboard.
- **FR-026**: The copy button MUST provide visual feedback (e.g., text changes to "Copied!") upon successful copy.

#### Scope Boundaries

- **FR-027**: The "What is this?" section MUST remain unchanged.
- **FR-028**: The "Next Steps" section MUST remain unchanged.
- **FR-029**: The "Reference Links" section MUST remain unchanged.
- **FR-030**: The site's visual styling MUST remain consistent with the current design. Any new elements (Objectives blocks, additional code blocks) MUST be styled to match the existing look and feel.

### Key Entities

- **Step Section**: A self-contained tutorial step with its own heading, content, and (for Steps 4–7) an Objectives block and Copilot prompt block. Each step is numbered 1–7.
- **Objectives Block**: A structured block at the top of Steps 4–7 containing goal bullet points and a keywords list. Provides a concise overview for both the reader and any AI reading the page.
- **Copilot Prompt Block**: A copy-enabled code block containing pre-written text the visitor pastes into their Copilot chat. Present in Steps 3–7.
- **Topics Keywords List**: A set of short concept terms at the end of each Objectives block, identifying topics the visitor may need help with during that step.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: 100% of page visitors can navigate through all seven individually titled step sections without encountering a "Key Concepts" section or a single "Getting Started" numbered list.
- **SC-002**: A first-time visitor with no prior development experience can read Steps 1–3 and reach the point of interacting with Copilot in under 15 minutes.
- **SC-003**: Each of Steps 4–7 contains an Objectives block with at least 2 goal bullet points and at least 2 keywords in the "Topics you may need help with" list.
- **SC-004**: Every Copilot prompt code block (Steps 3–7) can be copied to clipboard with a single click.
- **SC-005**: A visitor following the tutorial who pastes the Step 3 prompt into Copilot receives a response that demonstrates Copilot has read and understood the tutorial content.
- **SC-006**: 90% of beginner users (no prior coding experience) can follow the tutorial from start to finish without needing external help beyond the page content and their Copilot assistant.
