---
name: ux-design
description: >
  Interactive UX design documentation generator that transforms a PRD (Product Requirements Document)
  into a comprehensive UX design package. Use when the user wants to create UX design documentation,
  wireframes, user flows, sitemaps, content models, or design artifacts from a PRD. Triggers on
  requests like "create UX design from PRD", "generate wireframes from requirements", "walk me through
  UX design for this PRD", or any mention of turning a PRD into UX deliverables. Accepts the PRD
  file path as an argument.
---

# UX Design Documentation Generator

Transform a PRD into a complete UX design documentation package (UX_DESIGN.md) through an interactive,
step-by-step process. All visual artifacts use ASCII-style diagrams.

## Workflow

The process has 8 steps plus a final assembly. Walk the user through each step interactively,
presenting drafts and asking for feedback before moving on.

1. Read the PRD file (passed as argument)
2. Work through each step sequentially (see `references/steps.md`)
3. After each step, present the draft artifact and ask the user for feedback
4. Once all steps are complete, assemble everything into a single `UX_DESIGN.md`

## Interactive Mode Rules

- **One step at a time.** Present each step's output, then ask the user to approve, revise, or skip.
- **Show your work.** For each step, briefly explain what you're doing and why before presenting output.
- **Track progress.** At the start of each step, show a progress indicator: `[Step N/8]`.
- **Allow backtracking.** If the user wants to revisit a previous step, accommodate that.
- **Respect user shortcuts.** If the user says "looks good, keep going" or similar, proceed without extra confirmation until the next major step.

## Output Format

All output goes into a single `UX_DESIGN.md` file in the same directory as the PRD. Use this structure:

```markdown
# UX Design Documentation: [Product Name]

> Generated from: [PRD filename]
> Date: [date]

---

## 1. Problem & Goal Statement
[Step 1 output]

## 2. Structural Diagrams
### 2.1 Sitemap
### 2.2 User Flows
### 2.3 Wireflows
[Step 2 output]

## 3. Content Model & Hierarchy
[Step 3 output]

## 4. Low-Fidelity Ideation
[Step 4 output - 8-Up sketches in ASCII]

## 5. Interface Wireframes
[Step 5 output]

## 6. Refined Wireframes (Visual Design Applied)
[Step 6 output]

## 7. Annotated Wireframes (Handoff-Ready)
[Step 7 output]

## 8. Feedback & Presentation
### 8.1 Design Story
### 8.2 Feedback Tracker
[Step 8 output]
```

## ASCII Visual Conventions

Use these conventions for all diagrams and wireframes:

```
Boxes:        ┌─────────────┐    Arrows:    ──→  ──▶
              │  Content     │               │
              └─────────────┘               ▼

Wireframe:    ┌──────────────────────────┐
              │ ┌──────┐  Logo    [Nav]  │
              │ └──────┘                 │
              │ ┌──────────────────────┐ │
              │ │    Hero Section      │ │
              │ └──────────────────────┘ │
              │ [CTA Button]            │
              └──────────────────────────┘

Flow:         [Start] ──→ [Step 1] ──→ [Decision?]
                                          │    │
                                         Yes   No
                                          │    │
                                          ▼    ▼
                                       [A]   [B]

Sitemap:      Home
              ├── About
              ├── Products
              │   ├── Category A
              │   └── Category B
              └── Contact
```

## Detailed Step Instructions

For the full procedure for each step, read `references/steps.md`.
