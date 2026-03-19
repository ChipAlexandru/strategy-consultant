---
description: Sharpen a vague business question into a decision-oriented problem statement with clear scope
argument-hint: "<business challenge, client brief, or RFP>"
---

# /define-problem — Problem Definition

> If you see unfamiliar placeholders or need to check which tools are connected, see [CONNECTORS.md](../CONNECTORS.md).

**Important**: This plugin assists with strategic analysis and research but does not constitute professional consulting, financial, or legal advice. All outputs should be reviewed by qualified professionals before use in decision-making.

Take a vague business challenge and distill it into a problem statement sharp enough to drive analysis.

## Usage

```
/define-problem <business challenge or brief>
```

### Arguments

- `business challenge or brief` — The starting point. Can be:
  - A vague question: "We need to grow faster"
  - A client brief or RFP (file upload)
  - A project description or meeting transcript
  - A specific but unscoped question: "Should we acquire Company X?"

If no input is provided, prompt the user to supply context.

## Workflow

This command invokes the **problem-definition** skill as a standalone capability.

### Step 1: Extract Raw Situation
Read all provided materials and identify the stated problem, implicit assumptions, and what's missing.

### Step 2: Ask Targeted Questions
Using the AskUserQuestion tool, clarify:
- What decision will this inform?
- Time horizon for action?
- Known constraints?
- Who is the ultimate decision-maker and what do they care about most?

### Step 3: Draft Problem Statement
Produce a structured problem statement:
- **Context**: Client and situation (1-2 sentences)
- **Tension**: What has changed or is at stake (1 sentence)
- **Question**: Specific, decision-oriented question
- **Scope**: Boundaries — geography, time horizon, business unit, constraints

### Step 4: Create Deliverable Blueprint
Envision the ideal successful answer — what the report must contain, how the client uses it, what dimensions must be covered.

### Step 5: Stress-Test
Apply three checks: Partner test, "So what" test, Scope test.

### Step 6: Create Precision Anchor
A compact reference artifact carried through all subsequent phases to prevent analytical drift.

## Output

- Problem statement (Context / Tension / Question / Scope)
- Deliverable Blueprint (structure, must-contain, coverage dimensions, how client uses it)
- Client Question Checklist (every explicit question from source materials)
- Precision Anchor (question, decision, scope, success metric, what precise vs. non-answer looks like)
