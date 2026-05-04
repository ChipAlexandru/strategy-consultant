---
name: expert-interview
description: >
  Internal phase of the strategy-consultant engagement — invoke via engagement-manager, not directly. Plan, guide, and process expert interviews to confirm and enhance research findings. Use when someone asks to "prepare for expert interviews", "create an interview guide", "who should we interview", "process interview notes", "extract insights from interviews", or when the analytical workflow includes expert interviews after the research phase. Also trigger when someone uploads expert interview transcripts or notes that need to be analyzed and integrated into the research base.
---

# Expert Interview — Confirm, Enhance, and Challenge Research Findings

Expert interviews come AFTER the public research phase. Their purpose is to confirm findings, fill information gaps, add precision to estimates, and surface insights that public data cannot provide. Expert interview data carries high weight (CS-2) because it comes from practitioners with direct domain knowledge.

## Preflight Gate (run BEFORE any other step)

This phase requires upstream state and artifacts. Before doing anything else, verify ALL of the following:

1. `engagement-state.json` exists in the active workspace.
2. `"research"` is in `completed_phases`.
3. The following artifacts exist on disk and are non-empty:
   - `research-validated.md`
   - `precision-anchor.md`

If ANY required item is missing or empty, STOP. Do not identify gaps, do not draft expert profiles, do not write interview guides. Report the specific missing state field or artifact path and route control back to `engagement-manager`. Do not reconstruct research findings locally — without `research-validated.md`, gap identification has no anchor and the guides will be generic.

When the gate passes:
- Read `engagement-state.json` and treat its `workspace_path` as the active workspace.
- Read `research-validated.md` for gap identification and CS-3 claims to upgrade.
- Read `precision-anchor.md` for the question that frames every interview guide.

At the end of this phase, append `"expert-interview"` to `completed_phases`, update `artifact_paths.expert_interview_notes` (and any updated `research_validated` if the validator was re-run), set `current_phase` to `sense-check`, refresh `next_required_action` and `last_updated`, and write `engagement-state.json`.

This skill covers three phases: planning who to interview, creating interview guides informed by research findings, and processing interview outputs back into the research flow.

## When This Skill Activates

This skill activates in two scenarios:
1. **Pre-interview** (after research, before interviews happen): Plan who to interview and create interview guides
2. **Post-interview** (after interviews are conducted): Process uploaded notes/transcripts and integrate findings

If the user indicated during the Data Source Inquiry (Phase 2.5) that expert interviews would be available, this skill should be invoked after the research phase completes.

---

## Phase 1: Interview Planning — Who to Interview

Based on the Precision Anchor, the validated research findings, and the information gaps identified by the research-validator, recommend specific expert profiles.

### Step 1: Identify Information Gaps That Experts Can Close
Review the validator's output — specifically:
- The Remaining Gaps table (focus on gaps categorized as "Requires expert interview")
- Findings marked [ADJACENT] or [SUPPORTING] in the Precision Alignment Check that could become [DIRECT] with expert confirmation
- Critical claims resting on CS-3 sources that need upgrading to CS-2
- Areas where public data is stale, contradictory, or at an insufficient level of granularity

For each gap, write a one-sentence description of what the expert needs to provide.

### Step 2: Define Expert Profiles
For each priority gap, recommend a specific expert profile. Be precise — not "someone in the industry" but a targeted description:

**Format for each expert profile:**
```
Expert Profile #[N]
Role: [e.g., "Former VP of Supply Chain at a top-3 European FMCG company"]
Why this expert: [Which specific information gap they are best positioned to close]
Key qualification: [What direct experience makes them credible — e.g., "managed distribution across 5+ EU markets in the last 3 years"]
Priority: [HIGH / MEDIUM] — HIGH if the gap blocks a critical claim, MEDIUM if it would strengthen an already-supported finding
Company type: [e.g., "competitor", "customer", "supplier", "regulator", "industry body"]
```

### Step 3: Prioritize and Recommend
Rank the expert profiles by impact on the engagement. Recommend 3-5 experts maximum, prioritized by:
1. Which gaps are most critical to the Precision Anchor question
2. Which gaps would upgrade the most CS-3 findings to CS-2
3. Which gaps affect the strongest claims in the emerging storyline

Present the expert profiles to the user and ask for confirmation before creating interview guides.

---

## Phase 2: Interview Guide Creation

Create concise, problem-specific interview guides — NOT generic questionnaires. Each guide is tailored to the Precision Anchor, the specific gaps from the research phase, and the expert's profile.

### Step 1: Review Research Findings Relevant to This Expert
Before writing questions, identify:
- What the public research already established (so the interviewer doesn't waste time on known facts)
- Where the public research is uncertain, contradictory, or thin
- Specific data points or claims to validate or challenge
- Areas where the expert's direct experience can provide precision that public data lacks

### Step 2: Write the Interview Guide

**Guide structure:**

```
INTERVIEW GUIDE — [Expert Profile Description]
Engagement: [Problem statement — one line]
Date: [To be filled]
Interviewer: [To be filled]

CONTEXT FOR THE INTERVIEWER
[2-3 sentences summarizing what the research has found so far and what this interview aims to confirm, challenge, or deepen. This helps the interviewer understand the strategic context without biasing the expert.]

OPENING (2-3 minutes)
- Brief introduction of the engagement context (without leading the expert)
- Ask the expert to describe their relevant experience in their own words
- Establish the time horizon and scope they are most knowledgeable about

KEY QUESTIONS (20-30 minutes)
[5-8 questions, each explicitly mapped to an information gap]

Q1: [Question]
→ Gap this addresses: [Which information gap from the research phase]
→ What we already know: [Brief summary of public research on this point]
→ What we need from the expert: [Specific data point, validation, or insight]
→ Follow-up probes: [2-3 follow-up questions if the initial answer is vague or incomplete]

Q2: [Question]
→ Gap this addresses: ...
...

VALIDATION SECTION (5-10 minutes)
[Present 2-3 specific findings from the public research and ask the expert to confirm, challenge, or nuance them. Frame as: "Our research suggests [X]. Does that align with your experience? What would you adjust?"]

CLOSING (2-3 minutes)
- "What haven't I asked about that you think is important for this question?"
- "Who else would you recommend we speak with?"
- "Is there any data or documentation you could share that would help?"
```

### Step 3: Map Questions to Gaps
Create a traceability table showing which interview question addresses which information gap:

| Question | Information Gap | Current Best Evidence | CS Score of Current Evidence | What Expert Input Would Provide |
|----------|----------------|---------------------|---------------------------|-------------------------------|

This ensures no critical gap is missed and helps prioritize if the interview runs short.

---

## Phase 3: Information Extraction — Processing Interview Notes

When the user uploads interview notes or transcripts, process them systematically to extract findings and integrate them into the research base.

### Step 1: Extract Claims
Read the interview notes in full. For every substantive claim the expert makes, extract it as a discrete data point:

```
[1] Claim: "[Exact claim in the expert's words]"
    Expert: [Name, title, company]
    Context: [What prompted this claim — the question asked or topic discussed]
    Type: [FACT — based on the expert's direct experience / OPINION — the expert's judgment or prediction / HEARSAY — something the expert heard but did not directly experience]
```

Separate facts from opinions rigorously. An expert saying "we saw 15% cost reduction when we switched suppliers" is a FACT (their direct experience). An expert saying "I think the market will grow 20%" is an OPINION. An expert saying "I heard Company X is planning to enter" is HEARSAY.

### Step 2: Assign Confidence Scores
Expert interview claims are scored as follows:
- **CS-1**: Expert provides verifiable, company-reported data from their own organization (e.g., internal metrics, specific financial results they were directly responsible for). This is rare — most expert claims are CS-2.
- **CS-2**: Expert provides claims based on direct professional experience and domain expertise from a reputable company. This is the default for most expert interview findings. The expert must have direct experience (not second-hand knowledge) and the company must have a credible position in the relevant market.
- **CS-3**: Expert provides opinions, predictions, or hearsay. Also applies if the expert's company is not clearly reputable in the relevant domain, or if the claim is outside their area of direct expertise.

### Step 3: Cross-Reference Against Public Research
This is the critical step. For every expert claim, compare it against the public research findings:

**Agreement**: Expert confirms a public finding → Upgrade confidence. Note: "Corroborated by expert interview with [name], [company]." If the public finding was CS-3, it may now be upgradeable with CS-2 expert corroboration.

**Enhancement**: Expert adds precision or detail to a public finding → Record the enhanced version. Example: public research says "market is growing"; expert says "market grew 18% in our segment last year, driven by regulatory changes." The expert version is more precise and actionable.

**Conflict**: Expert contradicts a public finding → This requires careful adjudication:
1. **Assess source quality**: Compare the CS score of the public finding against the CS score of the expert claim. Higher quality wins as the primary source, but the conflict must be noted.
2. **Assess precision**: The more specific and verifiable statement wins. "The market is about $5B" (public estimate) vs. "Our segment alone is $2.3B and we have 40% share, so the market is at least $5.75B" (expert with direct data) → the expert version is more precise.
3. **Assess context**: Is the conflict due to different definitions, time periods, geographies, or segments? If so, both may be correct in their own context — note the difference.
4. **Flag for the validator**: Any unresolved conflict between expert and public data must be flagged in the output with both versions and a recommendation on which to use.

**Net new insight**: Expert provides information that public research did not uncover → Add as a new finding with CS-2 (or CS-1 if verifiable company data). Note that this is "expert-sourced, not publicly corroborated."

### Step 4: Produce the Expert Interview Output

```
## Interview Summary
Expert: [Name, title, company, date of interview]
Relevance to engagement: [One sentence on why this expert was selected]

## Key Findings from Interview
[Numbered list of the most important claims, each with type (FACT/OPINION/HEARSAY) and CS score]

## Cross-Reference Against Public Research

### Confirmed Findings
| # | Public Finding | Expert Confirmation | Effect on Confidence |
|---|---------------|--------------------|--------------------|

### Enhanced Findings
| # | Original Public Finding | Enhanced Version (from expert) | Improvement |
|---|------------------------|-------------------------------|-------------|

### Conflicts
| # | Public Finding (CS score) | Expert Claim (CS score) | Recommended Resolution | Reasoning |
|---|--------------------------|------------------------|----------------------|-----------|

### Net New Insights
| # | Expert Claim | CS Score | Gap It Fills | Publicly Corroborated? |
|---|-------------|----------|-------------|----------------------|

## Updated Source Registry Entries
[New or modified Source Registry entries resulting from this interview, in the standard format for inclusion in Research Notes]

[N] Data point: "[claim]"
    Source: Expert interview — [Name], [Title], [Company], [Date]
    URL: [N/A — expert interview]
    CS Score: [CS-1 / CS-2 / CS-3]
    Verbatim from source: "[Exact quote from interview notes]"

## Impact on Information Gaps
| Original Gap | Status After Interview | Notes |
|-------------|----------------------|-------|
[CLOSED / PARTIALLY CLOSED / STILL OPEN]

## Recommendations
[Any follow-up research needed based on new information or unresolved conflicts. Any additional experts to interview.]
```

### Step 5: Feed Back into the Research Flow
After processing, the expert interview output should be:
1. Passed to the research-validator to incorporate into the Consolidated Findings and Research Notes
2. Used by the sense-check to update the claim-by-claim assessment
3. Referenced in the synthesis with proper attribution ("per expert interviews with [company type] executives")

---

## Quality Standards

- **Attribution**: Every expert claim must be attributed to the specific expert (name, title, company). Anonymous expert claims are CS-3 at best.
- **Fact vs. opinion**: Never present an expert's opinion as a fact. If an expert says "I think the market will consolidate," write "Expert X believes the market will consolidate" — do not write "the market will consolidate."
- **Bias awareness**: Experts from specific companies may have self-serving perspectives. A competitor's executive may overstate their own position. A customer may focus on their pain points. Note potential bias for each expert.
- **Recency**: Expert knowledge has a shelf life. Ask when the expert last had direct exposure to the topic. Experience from 5+ years ago should be flagged as potentially stale.
- **Corroboration**: A single expert's view is one data point. Where possible, seek convergence across multiple experts. When experts disagree, note the disagreement and analyze why.
