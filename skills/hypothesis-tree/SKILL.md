---
name: hypothesis-tree
description: >
  Build a structured hypothesis tree with testable branches to guide analysis. Use when someone asks to "build a hypothesis tree", "structure this problem into hypotheses", "create an issue tree", "break this down MECE", or when a defined problem would benefit from structured decomposition before research begins. This skill is optional — not every problem requires a formal hypothesis tree. Skip it when the question is narrow enough that direct research is more efficient.
---

# Hypothesis Tree

Build a hypothesis tree that decomposes the client question into testable branches. This skill is a tool, not a requirement — invoke it only when structuring hypotheses genuinely helps focus the research effort.

## When to Use vs. Skip

**Use a hypothesis tree when:**
- The client question has multiple plausible answers and research needs prioritization
- The problem has 3+ distinct dimensions (e.g., market entry involves market attractiveness, competitive dynamics, and client capabilities)
- The team risks boiling the ocean without a structured view of what to investigate

**Skip the hypothesis tree when:**
- The question is narrow and specific enough that direct research answers it
- The user explicitly wants to go straight to research
- The situation is better served by a simple decision framework or pros/cons analysis

## Process

### Step 1: Start with the Governing Hypothesis
Write a single, falsifiable statement that represents the best initial answer to the client question. This is not a guess — it is a reasoned starting position that research will confirm, modify, or disprove.

Format: "We believe [specific answer to the client question] because [initial reasoning]."

The governing hypothesis must be:
- Specific enough to be wrong (if it cannot be disproven, it is not a hypothesis)
- Actionable — if proven true, the client knows what to do
- Grounded in at least preliminary logic, not pulled from thin air

### Step 2: Decompose into Branches
Break the governing hypothesis into 2-4 supporting conditions — the things that must be true for the hypothesis to hold.

Each branch must be:
- **Mutually exclusive**: no overlap between branches
- **Collectively exhaustive**: together they fully support (or disprove) the governing hypothesis
- **Testable**: each branch ends in a question that research can answer with evidence

Do not fetishize perfect MECE structure at the expense of speed. A pragmatic decomposition that the team can test in days beats an elegant one that takes a week to build.

### Step 3: Define What Proves or Disproves Each Branch
For every branch, specify:
- What evidence would **support** this branch (and where to find it)
- What evidence would **undermine** it (and where to find it)
- What **threshold** or benchmark distinguishes "this is true" from "this is false"

### Step 4: Prioritize
Not all branches are equally important or equally uncertain. Mark each branch:
- **Priority**: High / Medium / Low (based on impact on the overall answer)
- **Certainty**: High / Medium / Low (based on how much we already know)
- **Research approach**: What data or analysis is needed to test this branch

The research phase should start with high-priority, low-certainty branches — that is where investigation adds the most value.

## Output Format

```
## Governing Hypothesis
[The falsifiable initial answer]

## Hypothesis Tree

### Branch 1: [Name]
- Statement: [What must be true]
- Supports if: [Evidence that would confirm]
- Undermines if: [Evidence that would disprove]
- Priority: [High/Medium/Low] | Certainty: [High/Medium/Low]
- Research needed: [Specific data or analysis]

### Branch 2: [Name]
[Same structure]

### Branch 3: [Name]
[Same structure]

## Research Prioritization
[Ordered list of what to investigate first and why]
```

Present the tree to the user for review. Adjust branches based on their feedback — they often know which branches are already settled (no research needed) and which are genuinely uncertain.
