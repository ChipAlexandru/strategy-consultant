---
description: Plan expert interviews and create structured interview guides mapped to research gaps
argument-hint: "<topic or research context>"
---

# /interview-guide — Expert Interview Planning

> If you see unfamiliar placeholders or need to check which tools are connected, see [CONNECTORS.md](../CONNECTORS.md).

**Important**: This plugin assists with strategic analysis and research but does not constitute professional consulting, financial, or legal advice. All outputs should be reviewed by qualified professionals before use in decision-making.

Plan expert interviews and create structured guides that close specific research gaps. Can also process uploaded interview notes or transcripts after interviews are conducted.

## Usage

```
/interview-guide <topic or context>
```

### Arguments

- `topic or context` — What the interviews should cover. Can be:
  - A research topic: "European EV charging market"
  - A reference to prior research: "Based on the research gaps we found"
  - Uploaded interview notes/transcripts to process: "Process these interview notes"
  - A specific expert type: "Prepare for a call with a former VP of Operations at a logistics company"

If no input is provided, prompt the user for the engagement context and research gaps.

## Workflow

This command invokes the **expert-interview** skill, which operates in two modes:

### Mode A: Pre-Interview (Planning)

**Step 1: Identify Gaps**
Review available research findings and identify information gaps that experts can close — particularly claims resting on CS-3 that could be upgraded to CS-2 with expert confirmation.

**Step 2: Define Expert Profiles**
For each priority gap, recommend a specific expert profile with role, qualification, priority level, and company type.

**Step 3: Prioritize**
Rank by impact on the engagement. Recommend 3-5 experts maximum.

**Step 4: Create Interview Guides**
For each expert, produce a structured guide with:
- Context for the interviewer
- 5-8 key questions mapped to specific information gaps
- What we already know vs. what we need from the expert
- Follow-up probes for each question
- Validation section (present 2-3 public research findings for expert to confirm/challenge)
- Closing questions

### Mode B: Post-Interview (Processing)

**Step 1: Extract Claims**
From uploaded notes/transcripts, extract every claim with type (FACT / OPINION / HEARSAY) and confidence score.

**Step 2: Cross-Reference**
Compare every expert claim against public research — classify as Agreement, Enhancement, Conflict, or Net New Insight.

**Step 3: Produce Output**
Structured expert interview output with key findings, cross-reference tables, updated Source Registry entries, and impact on information gaps.

## Output

**Pre-interview**: Expert profiles (prioritized) + structured interview guides with gap mapping

**Post-interview**: Extracted claims with confidence scores, cross-reference against public research, updated Source Registry entries, gap closure assessment
