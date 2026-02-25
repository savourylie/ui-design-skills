# UX Design Steps — Detailed Reference

## Step 1: Problem & Goal Statement

Translate the PRD's requirements into user-focused goals.

**Action:** Answer three questions from the PRD:
- **Who** will use the solution?
- **What** are their goals?
- **What problem** does this address?

**Output:** A concise text block formatted as a "sticky note" — the first artifact in the document. Keep it to 3-5 sentences max. Include user persona, primary goal, and core problem.

**Example:**
```
┌─────────────────────────────────────────────────┐
│  TARGET USER: Small business owners (non-tech)  │
│  GOAL: Track expenses without accounting skill  │
│  PROBLEM: Current tools are complex, expensive, │
│  and require training to use effectively.       │
└─────────────────────────────────────────────────┘
```

---

## Step 2: Structural Diagrams

Translate abstract PRD requirements into logical flows.

**Action:** Create three types of diagrams:

### Sitemaps
Outline the hierarchy using tree notation. Show parent-child page relationships.

### User Flows
Map the step-by-step journey for specific use cases. Start at the user's end goal (the "happy path") and work backward. Use decision diamonds for branching.

### Wireflows
Combine low-fidelity wireframe boxes with arrows to show how the interface changes across screens.

**Tips:**
- Derive pages/screens directly from PRD features
- Each PRD user story should map to at least one user flow
- Identify shared screens across flows

---

## Step 3: Content Model (Inside-Out Design)

Separate content from layout.

**Action:**
1. List all must-have information for each key screen (derived from PRD requirements)
2. Arrange content in priority order (top = most important)
3. Start with the smallest content unit and expand outward

**Output:** A prioritized content block per key screen.

**Example:**
```
Screen: Dashboard
─────────────────
[CRITICAL]  Account balance summary
[CRITICAL]  Recent transactions (last 5)
[HIGH]      Quick-add expense button
[HIGH]      Monthly spending chart
[MEDIUM]    Category breakdown
[LOW]       Tips & recommendations
```

---

## Step 4: Low-Fidelity Ideation

Generate many divergent ideas rapidly using constraints.

**Action:** For each key screen, produce an "8-Up" exercise — 8 distinct layout concepts using only basic shapes. Apply stress-case prompts:
- "What if the user is on mobile?"
- "What if there are 0 items? 1000 items?"
- "What if the user is in a rush?"

**Output:** ASCII sketches, one per idea, labeled 1-8. Use only rectangles, lines, and placeholder text like `[xxx]` or `~~~~`.

**Example (one of eight):**
```
Idea 3/8 — Card-based dashboard
┌──────────────────┐
│ $[balance]       │
├──────┬───────────┤
│[+Add]│ [recent]  │
│      │ [recent]  │
│      │ [recent]  │
├──────┴───────────┤
│ [chart ~~~~~~~~] │
└──────────────────┘
```

---

## Step 5: Interface Wireframes

Transition rough ideas into structured interfaces.

**Action:**
1. Transform shapes into standard UI components (buttons, inputs, navs, cards, lists, forms)
2. Combine components into UI patterns (navigation bars, card grids, data tables)
3. Consolidate repeating structures into page templates
4. Begin replacing placeholders with real or realistic sample text

**Output:** Mid-fidelity wireframes using recognizable UI elements.

---

## Step 6: Visual Design Principles

Optimize wireframes for human perception and reduced cognitive load.

**Action:** Apply these principles to each wireframe:

- **Hierarchy:** Use size differentiation and spacing to make primary actions dominant. Apply the "blur test" — describe what stands out when squinting.
- **Alignment:** Left-align text blocks, anchor elements to screen edges, use consistent grid.
- **Clarity:** Hide, group, or remove non-essential elements. Each screen should have one clear primary action.

**Output:** Refined wireframes with visual improvements noted via inline comments like `← primary CTA, largest element`.

---

## Step 7: Annotations for Handoff

Add implementation guidance that wireframes alone cannot communicate.

**Action:** Annotate wireframes with:
- **Error states:** What happens when things go wrong (validation, empty states, network errors)
- **Dynamic behavior:** Loading states, animations, transitions
- **Edge cases:** Truncation rules, overflow behavior, responsive breakpoints
- **Design rationale:** Brief notes explaining *why* a decision was made

**Output format:** Numbered callouts next to wireframe elements.

**Example:**
```
┌──────────────────────────────┐
│ ┌──────┐                     │
│ │ Logo │  [Nav] [Nav] [•••]  │ ← (1)
│ └──────┘                     │
│                              │
│  Welcome back, [Name]  (2)→  │
│                              │
│ ┌──────────────────────────┐ │
│ │   $2,450.00              │ │ ← (3)
│ │   Total Balance          │ │
│ └──────────────────────────┘ │
└──────────────────────────────┘

(1) Nav collapses to hamburger at <768px
(2) Shows "Welcome" (no name) if profile incomplete
(3) Error state: "Unable to load balance" + retry link
    Loading state: shimmer placeholder
    Format: locale-aware currency
```

---

## Step 8: Feedback & Presentation

Create presentation materials and feedback tracking.

**Action:**

### Design Story
Write a narrative walkthrough of the design from the user's perspective:
1. Background — the problem context
2. Meet the user — introduce the persona
3. The journey — walk through the primary flow

### Feedback Tracker
Create a markdown table to track design feedback:

```
| # | Feedback Item | Source | Status | Notes |
|---|--------------|--------|--------|-------|
| 1 | Example item | [name] | Agree & do now | ... |
```

**Status categories:**
- `Agree & do now` — Will implement immediately
- `Agree & do later` — Valid but deferred
- `Needs research` — Requires more investigation
- `Clarify` — Need more details from stakeholder
- `No` — Considered and rejected (document why)
