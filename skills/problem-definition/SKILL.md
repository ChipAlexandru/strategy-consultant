---
name: problem-definition
description: >
  Internal phase of the strategy-consultant engagement — invoke via engagement-manager, not directly. Define and scope a client problem into a sharp, decision-oriented question. Use when someone says "help me define this problem", "scope this engagement", "what's the real question here", "sharpen this problem statement", or provides a vague business challenge that needs structuring before analysis can begin. Also trigger when someone shares a client brief, RFP, or project description and needs help extracting the core analytical question.
---

# Problem Definition

Take the client situation — however vague or sprawling — and distill it into a problem statement sharp enough to drive analysis.

## Routing Check (run BEFORE any other step)

This skill is Phase 1 of the engagement. There is no upstream phase to gate on for fresh runs, so this is **not** a hard upstream preflight gate (unlike research, sense-check, synthesis, client-report, etc.) — it is a routing check that confirms the skill is being entered through a legitimate path and that workspace ownership is correctly attributed to engagement-manager.

Before drafting anything, determine which case applies:

**Case (a) — Fresh `/engagement` Phase 1 invocation.** The user has just started a new engagement. `engagement-manager` owns workspace creation and initial state setup; it will create `./engagements/<slug>-<date>/` and initialize `engagement-state.json` during or immediately after this phase. Proceed normally with Steps 1–7 below. Do NOT create the workspace folder or write `engagement-state.json` from inside this skill — that is engagement-manager's responsibility. This skill produces problem-definition artifacts (`problem-statement.md`, `client-question-checklist.md`, `precision-anchor.md`, `source-material-extraction-log.md`) and engagement-manager places them in the correct workspace and registers them in state.

**Case (b) — `/define-problem` continuation invocation.** The user has invoked the continuation command to refine an existing engagement's problem definition. Before proceeding, verify that an active workspace exists:

1. `./engagements/<slug>-<date>/engagement-state.json` is present, OR
2. legacy `./engagement/precision-anchor.md` is present (v1.4.0 backward-compatible fallback).

If neither is present, STOP. Do not proceed with Steps 1–7. Do not create a workspace from inside this skill. Report to the user: "No active engagement workspace found. Use `/engagement <topic>` to start a new engagement — it will create the workspace and route into problem-definition automatically." Then route control back to engagement-manager.

**Subcommands must not create workspaces.** Workspace creation, slug derivation, dating, and `engagement-state.json` initialization are owned exclusively by engagement-manager. If this skill detects it has been invoked through a continuation command without an active workspace, the correct action is to stop and route back — never to silently create a workspace and continue. That bypass rebuilds the orchestrator piecemeal and is a known v1.4-era failure mode that v1.5.0 explicitly removes.

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

### Step 4.5: Envision the Best Possible Answer (MANDATORY)
Before stress-testing the problem statement, concretely imagine what the client holds in their hands if this engagement succeeds perfectly. Write a Deliverable Blueprint:

```
DELIVERABLE BLUEPRINT (carry forward to all downstream phases)

STRUCTURE: [How is the ideal document organized? Describe the sections
and their logic — not "a comprehensive report" but the specific skeleton.]

MUST CONTAIN: [What specific content must appear? Be concrete enough
that you could check each item off a list.]

COVERAGE DIMENSIONS: [What dimensions must the answer span completely?
List them. These become the completeness standard for research and
the report.]

HOW THE CLIENT USES IT: [Will they make one decision and move on, or
return to this document repeatedly? This determines whether the primary
quality metric is argumentative tightness or coverage completeness.]

```

Present the blueprint to the user for confirmation alongside the problem statement.

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

**Document-anchored feedback check:** If the client provided a document (deck, report, draft) and asked for feedback, review, or improvement suggestions, add an explicit checklist item:

```
[ ] DOCUMENT FEEDBACK: Client requested feedback on [document name]. Deliverable must anchor feedback to the document's structure — slide-by-slide for decks, section-by-section for reports. Thematic feedback alone is insufficient when the client has a specific document they will revise. Structural coordinates: [Reference the Structural Index from the Source Material Extraction Log]
```
This ensures the deliverable tells the client "on Slide 6, change X to Y" rather than "the deck lacks a data narrative." The client needs to know WHERE to make changes, not just WHAT themes are missing.

### Step 7: Create the Precision Anchor
Once the problem statement is confirmed, produce a **Precision Anchor** — a compact reference block that will be carried through every downstream phase to ensure the final answer precisely matches the question asked.

**Precision Anchor format:**
```
PRECISION ANCHOR (carry forward to all downstream phases)
Question: [The exact decision-oriented question — copied verbatim from the problem statement]
Decision: [What specific decision this will inform]
Scope: [Geography, time horizon, business unit, constraints]
Target entity: [When the client's request references a specific type of offering, capability, or business function (e.g., "DaaS platform," "managed services," "supply chain solution"), state your working definition in one sentence — what it is, and what adjacent offering at the same companies it is not. This travels with the Precision Anchor and governs what the research agents profile. The client confirms or corrects by exception when reviewing the problem statement.]
Success metric: [How we will know the answer is precise enough — e.g., "must quantify the revenue impact within ±20%" or "must compare at least 3 options with clear trade-offs"]
What a precise answer looks like: [1 sentence describing what the output must contain to actually answer the question — not an adjacent or easier question]
What a non-answer looks like: [1 sentence describing the most likely drift — the adjacent question the analysis might accidentally answer instead]
Deliverable Blueprint: [Reference the full Deliverable Blueprint from Step 4.5 above]
```

The Precision Anchor must be included in the research brief, passed to the validator, and re-checked at synthesis. Its purpose is to prevent analytical drift — the common failure mode where the team finds interesting data that answers a different (often easier) question than the one the client actually asked.

## Common Failure Modes to Avoid
- Accepting "improve performance" or "develop a strategy" as a problem statement — these are categories of work, not analytical questions
- Defining the problem so broadly that any analysis would take months
- Defining it so narrowly that the answer is obvious and not worth the engagement
- Confusing the client's stated problem with the real problem (the stated one is often a symptom)
