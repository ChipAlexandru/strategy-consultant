---
name: problem-definition
description: >
  Define and scope a client problem into a sharp, decision-oriented question. Use when someone says "help me define this problem", "scope this engagement", "what's the real question here", "sharpen this problem statement", or provides a vague business challenge that needs structuring before analysis can begin. Also trigger when someone shares a client brief, RFP, or project description and needs help extracting the core analytical question.
---

# Problem Definition

Take the client situation — however vague or sprawling — and distill it into a problem statement sharp enough to drive analysis.

## What a Good Problem Statement Contains

A complete problem statement answers four questions in 2-4 sentences:

1. **Who** is the client and what is their context? (Industry, size, situation)
2. **What** is happening that demands attention? (The tension, change, or threat)
3. **What decision** will this analysis inform? (Not "understand X" but "decide whether to X or Y")
4. **What are the boundaries?** (Geography, time horizon, business unit, budget constraints)

## Process

### Step 1: Extract the Raw Situation
Read whatever the user provides — a brief, a conversation summary, a rambling description, uploaded documents. Pull out every factual claim, stated objective, and implied constraint.

### Step 2: Identify What Is Missing
Most problem descriptions are incomplete. Common gaps:
- The decision is implicit, not stated ("grow margins" is an objective, not a decision — the decision is *how*)
- The scope is undefined (global or one market? all products or one category?)
- Success criteria are absent (grow by how much? over what timeframe? relative to what benchmark?)
- The stakeholder's real concern is buried under corporate language

### Step 3: Ask Targeted Questions
Use the AskUserQuestion tool to fill critical gaps. Ask only what is needed to make the problem statement actionable — do not ask for information that can be discovered through research.

Priority questions (ask only what is missing):
- **Additional context and documents** (ask this first): "Do you have any additional documents or context that would help define the scope — for example, a client call transcript, project brief, prior analysis, or internal memo?" This question should be asked early because having source documents fundamentally changes how thorough the problem definition can be. If the user provides documents, read and incorporate them into Steps 1 and 2 before proceeding to draft the problem statement.
- What decision will this analysis inform?
- What is the time horizon for action?
- Are there known constraints (budget, organizational, regulatory)?
- Who is the ultimate decision-maker and what do they care about most?

### Step 4: Draft the Problem Statement
Write the problem statement in this format:

**Context**: [1-2 sentences on who the client is and their current situation]
**Tension**: [1 sentence on what has changed or what is at stake]
**Question**: [The specific, decision-oriented question this engagement will answer]
**Scope**: [Boundaries — geography, time horizon, business unit, constraints]

### Step 5: Stress-Test It
Before presenting the problem statement, run three quick checks:
1. **The partner test**: If a senior partner read only the Question line, would they immediately understand what work needs to happen?
2. **The "so what" test**: Does answering this question actually change what the client does? If the answer is "interesting but doesn't drive action," the question is wrong.
3. **The scope test**: Is this answerable in the time and resources available? If not, narrow it.

Present the problem statement to the user and ask for confirmation before any downstream analysis begins.

### Step 6: Extract the Client Question Checklist
After confirming the problem statement, systematically extract **every explicit question, request, and specification** from all available source material — the client brief, call transcript, uploaded documents, or the user's messages. Record each one as a checklist item.

**Client Question Checklist format:**
```
CLIENT QUESTION CHECKLIST (carry forward — verify at report delivery)
[ ] Q1: [Exact question or request, in the client's own words or a faithful paraphrase]
    Source: [Where this appeared — e.g., "client call transcript, minute 14" or "project brief, paragraph 3"]
    Required format: [If the client specified a format — e.g., "in inches", "by store size", "as a ranking" — note it here. Otherwise: "No format specified."]
[ ] Q2: ...
[ ] Q3: ...
```

**Extraction rules:**
- Include every explicit question the client asked, even if it seems minor
- Include every request for specific data, comparisons, or specifications
- Note the exact format or unit the client requested (e.g., "screen sizes in inches," "broken out by region," "ranked by priority")
- Include requests implied by the decision context (e.g., if the client is writing an RFP, they need spec-level detail)
- If the available data does not perfectly match the requested format, the report must either convert it (with a caveat) or explicitly note the format gap and flag it for follow-up
- This checklist will be verified during the client-report quality review — no client question should go unanswered without acknowledgment

### Step 7: Create the Precision Anchor
Once the problem statement is confirmed, produce a **Precision Anchor** — a compact reference block that will be carried through every downstream phase to ensure the final answer precisely matches the question asked.

**Precision Anchor format:**
```
PRECISION ANCHOR (carry forward to all downstream phases)
Question: [The exact decision-oriented question — copied verbatim from the problem statement]
Decision: [What specific decision this will inform]
Scope: [Geography, time horizon, business unit, constraints]
Success metric: [How we will know the answer is precise enough — e.g., "must quantify the revenue impact within ±20%" or "must compare at least 3 options with clear trade-offs"]
What a precise answer looks like: [1 sentence describing what the output must contain to actually answer the question — not an adjacent or easier question]
What a non-answer looks like: [1 sentence describing the most likely drift — the adjacent question the analysis might accidentally answer instead]
```

The Precision Anchor must be included in the research brief, passed to the validator, and re-checked at synthesis. Its purpose is to prevent analytical drift — the common failure mode where the team finds interesting data that answers a different (often easier) question than the one the client actually asked.

## Common Failure Modes to Avoid
- Accepting "improve performance" or "develop a strategy" as a problem statement — these are categories of work, not analytical questions
- Defining the problem so broadly that any analysis would take months
- Defining it so narrowly that the answer is obvious and not worth the engagement
- Confusing the client's stated problem with the real problem (the stated one is often a symptom)
