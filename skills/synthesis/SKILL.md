---
name: synthesis
description: >
  Synthesize research findings into a coherent storyline that answers the client question. Use when someone asks to "synthesize these findings", "build the storyline", "what's the narrative", "put this together into a story", "structure the argument", "what should we tell the client", or when the analytical workflow moves from sense-checked research to constructing the client-facing argument. Also trigger when someone has a collection of findings and needs help turning them into a logical, persuasive narrative.
---

# Synthesis — Build the Storyline

Synthesis is not summarizing. Summarizing says "here is what the data shows." Synthesis says "here is what it means for the client's decision — and here is what they should do."

Take the validated, sense-checked research findings and organize them into the storyline that most directly and persuasively answers the client question.

## Preflight Gate (run BEFORE any other step)

This phase requires upstream state and artifacts. Before doing anything else, verify ALL of the following:

1. `engagement-state.json` exists in the active workspace.
2. `"sense-check"` is in `completed_phases`.
3. The following artifacts exist on disk and are non-empty:
   - `sense-check.md`
   - `research-validated.md`
   - `precision-anchor.md`

If ANY required item is missing or empty, STOP. Do not write a governing message, do not draft headlines, do not produce a storyline. Report the specific missing state field or artifact path and route control back to `engagement-manager`. A storyline written without a passed sense-check is the most dangerous failure mode in this plugin — it converts un-pressure-tested findings into persuasive narrative.

Additionally, before proceeding, read `sense-check.md` and confirm the Question-Answer Precision Verdict is `PRECISE` or `PARTIAL`. If the verdict is `DRIFTED`, STOP — the engagement-manager must loop back to research, not forward to synthesis.

When the gate passes:
- Read `engagement-state.json` and treat its `workspace_path` as the active workspace.
- Use `precision-anchor.md` as the authoritative reference for Step 0 (Precision Anchor Re-Check) and the governing message altitude test.
- Use `research-validated.md` as the evidence base; treat its CS scores and alignment markers ([DIRECT]/[SUPPORTING]/[ADJACENT]) as authoritative.
- Use `sense-check.md` for the steel-man counter-narrative, Client-Raised Objections Inventory, Evidence-Implied Risks, and Value-Add Opportunities.

At the end of this phase, append `"synthesis"` to `completed_phases`, update `artifact_paths.storyline`, set `current_phase` to `storyline-critique`, refresh `next_required_action` and `last_updated`, and write `engagement-state.json`.

## References (read once, before drafting)

- `../../references/altitude-and-precision.md` — altitude rules used in Step 0 (Precision Anchor Re-Check) and Step 1 (governing-message altitude test). The verdict semantics (DIRECTLY / PARTIALLY / WITH QUALIFICATION) come from this reference.
- `../../references/counter-argument-sources.md` — the three tributaries you must address in Step 4. Do not invent your own; pull them from `sense-check.md`.
- `../../references/expert-anchor-and-conflicts.md` — the expert-anchor rule for quantitative claims and the insight-before-data rule used in Step 3.
- `references/storyline-patterns.md` — when to lead with the answer, when to compare options, when to phase a roadmap.

These references are the source of truth. The steps below are the phase-specific actions; they do not re-explain the underlying doctrine.

## Core Principle: Let the Answer Shape the Structure

Do NOT force findings into a predetermined framework. The storyline structure should emerge from the logic of the answer itself. Some client questions are best answered with:
- A recommendation and its supporting pillars
- A comparison of options with a clear winner
- A phased roadmap with decision gates
- A risk-reward assessment with a recommended posture
- A diagnostic that reveals the root cause before proposing a fix

Choose the structure that makes the argument clearest for THIS specific question. If the natural logic of the answer suggests a structure, use it. If not, default to: lead with the answer, support with evidence, address the counter-argument.

## Process

### Step 0: Precision Anchor Re-Check (mandatory before writing anything)
Before writing a single word, re-read the **Precision Anchor** from the problem-definition phase. Copy it to the top of your working notes. Then answer these three questions:
1. **Can I answer the exact question in the Precision Anchor with the available evidence?** If yes, proceed to Step 1.
2. **Can I partially answer it?** If yes, proceed — but the governing message MUST state what the evidence answers AND what it does not. The synthesis must include a clear qualification (e.g., "The data shows X, which implies Y for the client's question, because [reasoning]. However, the direct question of Z cannot be fully answered without [specific missing data].")
3. **Has the analysis drifted to answer a different question?** Compare the validator's Consolidated Findings — if most are tagged [ADJACENT] or [SUPPORTING] rather than [DIRECT], STOP. Do not synthesize an answer to a question the client did not ask. Instead, flag the drift and recommend either (a) additional targeted research or (b) reframing the engagement question with the client.

**Altitude check on the governing message:** Place the Precision Anchor success metric next to the governing message. Does the answer operate at the same level of specificity? If the success metric says "specific screen counts by store size" and the governing message says "retailers are deploying thousands of screens," the altitude is wrong. Rewrite the governing message to either (a) answer at the right altitude if the evidence supports it, or (b) explicitly state the altitude gap: "Public data provides network-level benchmarks but not per-store deployment specs by store size; expert interviews are needed to build DFI's archetypes."

A governing message that operates at the wrong altitude will produce a report that sounds authoritative but doesn't actually help the client make their decision.

### Step 1: Start with the Answer
Re-read the Deliverable Blueprint from the Precision Anchor. If the blueprint describes a document where the value is coverage and completeness, the governing message should frame what the coverage reveals, not force a single-action recommendation. The storyline structure should take the blueprint's structure as its starting point.

Write the answer to the client question in one sentence. This is the governing message of the entire storyline. If you cannot write it in one sentence, the thinking is not sharp enough yet.

Test the answer:
- Is it specific enough to drive action? ("Invest in digital" fails. "Invest $30M over 18 months to build a DTC channel in Germany, starting with Category X" passes.)
- Does it directly answer the question from the problem definition? **Re-read the Precision Anchor — does the governing message address the exact question, decision, scope, and success metric?**
- Would a CEO hearing only this sentence understand what to do?
- **Precision test**: Place the Precision Anchor question and the governing message side by side. Does the answer match the question, or has it drifted? If it answers an easier or adjacent question, rewrite it.

### Step 2: Identify the 2-4 Key Arguments
Distill the evidence into the 2-4 arguments that most powerfully support the answer. Each argument should:
- Be independently meaningful (not just a data point — an insight)
- Be supported by evidence from the research phase
- Connect directly to the governing message
- Pass the "so what" test: if this argument were not true, would the answer change?

Prioritize against the Deliverable Blueprint. Findings that fill a dimension the client needs belong in the main storyline even if they don't individually drive a single recommendation. Findings that don't serve the blueprint's structure go to the Value-Add Review (Step 2.5) before being sent to the appendix — some may deserve their own section.

### Step 2.5: Value-Add Review

The precision architecture (Steps 0-2) ensures the client's question gets answered. This step ensures the deliverable doesn't stop there.

Review the full research base — analyst memos, validated findings, expert interview extractions — for insights that fall outside the Precision Anchor but would materially elevate the deliverable.

**The test for inclusion**: Would the client, after reading the deliverable, say "I'm glad they included this even though I didn't ask for it"? If yes, it belongs in the report as a supplementary section, not in the appendix.

**What to look for**: Do not prescribe specific categories — the research itself reveals what is valuable. Scan the full research base (including [ADJACENT] findings from the validator, expert content that didn't map to a sub-question, and deprioritized research threads) and ask: "Is there anything here that a knowledgeable practitioner would consider important context, even though the client didn't specifically request it?"

**How to include it**: Value-add sections sit after the core arguments but before the counter-arguments. Label them to signal supplementary value (e.g., "Practical Considerations," "Implementation Context," "Additional Capabilities"). Each section earns its place by being directly useful, not by being comprehensive.

**What still goes to the appendix**: Findings that are intellectually interesting but not practically useful. The distinction is client utility.

### Step 3: Stack the Evidence Under Each Argument
For each argument, organize the supporting evidence:
- **Insight-before-data rule:** Each argument/section must open with the KEY CONCEPTUAL
  INSIGHT — the "why" that explains the data pattern — before presenting structured data
  (tables, benchmarks, scenarios).

  When an expert provided a conceptual frame for the topic, that frame should be the section
  opener: a 1-2 sentence statement of the principle, with attribution, that tells the reader
  WHY the data looks the way it does. The structured data then follows as evidence supporting
  the frame.

  This applies regardless of the domain:
  - If the insight is "revenue follows a diminishing returns curve" → state that, then show
    the benchmark table
  - If the insight is "customer acquisition cost rises non-linearly with market share" →
    state that, then show the competitor comparison
  - If the insight is "regulatory approval timelines are the binding constraint, not
    technology readiness" → state that, then show the timeline analysis

  A section that opens with data tells the reader WHAT. A section that opens with the
  conceptual insight tells them WHY — which is what they need to make decisions. Data
  without a frame is a spreadsheet; data with a frame is an argument.
- Lead with the strongest, most credible data point
- Layer in corroborating evidence from different sources
- Acknowledge limitations or caveats honestly (this builds credibility)
- Include the "compared to what?" benchmark for every number
- For every key data point, enforce the **"Data → So What → Now What"** pattern:
  - **Data**: State the finding with source attribution
  - **So what**: State why it matters for the client's decision
  - **Now what**: State the specific action the client should take based on this finding
  - Example: "85% of ad revenue is sold direct, 15% programmatic [Expert, CS-2]. This means the client should staff a direct sales team as the primary revenue driver, and use programmatic fill via their ad server for unsold inventory."
- Use **source-type-aware confidence language**: state expert-confirmed data directly; hedge public research with "according to [source]"; explicitly label consultant-constructed assumptions as "for illustrative purposes"
- **Expert-anchor principle for quantitative claims:** When an expert provides a conditional
  quantitative claim (a specific number with stated conditions), use the expert's figure as
  the HEADLINE ANCHOR. Present plugin-generated scenarios, sensitivity ranges, or modeled
  estimates as CONTEXT AROUND the expert's number — not as a replacement for it.

  Structure: "[Expert's number] is achievable when [expert's stated conditions] [Expert,
  CS-2]. Sensitivity analysis: under [alternative assumptions], the range extends to
  [modeled range]."

  The expert's conditional number is a CS-2 data point from a practitioner with direct
  experience. The plugin's scenario model is constructed from assumptions that may not
  themselves be sourced. A constructed number should never displace a sourced number in
  the headline — it should contextualize it.

  This applies to any quantitative claim where both an expert figure and a plugin-modeled
  figure exist: payback periods, market sizes, growth rates, cost estimates, adoption
  timelines, margin targets, etc.

  When the expert's conditions are unlikely to be met in the client's specific context,
  the report should say so explicitly — "Expert estimates [X] under [conditions]; the
  client's situation differs in [specific ways], suggesting [adjusted range]" — rather
  than silently substituting the adjusted range as the headline.

- **Source material cross-reference:** When a finding supports or challenges content from
  a client-provided document, cite the structural coordinate from the Source Material
  Extraction Log (e.g., "this contradicts the positioning on DFI Slide 16" or "this
  validates the approach shown in Kroger deck, p20-21"). The deliverable should make
  visible where the analysis confirms, extends, or challenges what the client already has.
  A client who provided a 30-slide deck expects the analysis to engage with specific slides,
  not just the themes.

### Step 4: Address the Counter-Arguments (comprehensive, not single-risk)
The storyline must pre-empt objections from THREE sources:

1. **The steel-man counter-narrative** from the sense-check phase — the strongest analytical case against the recommendation.
2. **Client-raised objections** — re-read the client call transcript, brief, and all source material. Extract every concern, hesitation, or objection the client raised. Each must be addressed explicitly. Client-raised concerns that go unaddressed in the deliverable are a credibility risk — the client will notice their own question was not answered.
3. **Foreseeable operational risks** — risks inferable from the evidence itself. If the recommendation involves phased deployment, address operational complexity. If it requires a sales team, address staffing prerequisites. If it depends on third-party adoption, address the dependency.

For each counter-argument, show that:
- You considered it seriously
- The evidence weighs against it (or it represents a manageable risk)
- You have a mitigation plan if the risk materializes

A storyline that addresses only the most obvious objection while ignoring client-raised concerns or operational risks will lose credibility.

### Step 5: Write Draft Headlines
Write the sequence of headlines that would appear on each page of a client document. Read them in order — they should form a coherent, logical argument without any supporting text.

Test the headline sequence:
- Does each headline logically follow from the previous one?
- Is there a gap in the argument where a skeptical reader would say "wait, why?"
- Does the sequence build to the recommendation naturally?
- Would a client who reads only the headlines understand the full argument?

### Step 6: Map Evidence to Headlines
For each headline, note which specific research findings support it. This creates traceability from the final storyline back to the evidence base, and reveals any headlines that lack adequate support.

### Step 7: Cross-Section Linkage Review (MANDATORY)
After mapping all evidence, review the storyline as an integrated argument:
- For each argument/section, ask: "Does any finding here have implications for the conclusions in another section?"
- Where causal chains span sections, note the cross-reference explicitly in the storyline notes (e.g., "The measurement capability in Argument 2 directly accelerates the advertiser adoption rate in Argument 1, which drives the payback timeline in Argument 3")
- If sections could be reordered without the reader noticing a break in logic, the storyline is a list of findings, not an integrated argument. Revise until the sections build on each other.

### Step 8: Assumption Labeling Pass
Review the storyline for any illustrative calculations, projections, or scenario models. For each:
- Clearly distinguish between "data I found" (sourced) and "numbers I constructed to show the math" (illustrative)
- Label every non-sourced input assumption: "Assumed for modeling purposes: [X]"
- This distinction must carry through to the report — the client-report skill will enforce it in the quality review

## Output Format

```
## Governing Message
[One sentence: the answer to the client question]

## Storyline Structure
[Brief explanation of why this structure fits this question]

## The Argument

### [Headline 1]
Supporting evidence: [specific findings with sources]
Key data point: [the anchor number or fact]

### [Headline 2]
Supporting evidence: [specific findings with sources]
Key data point: [the anchor number or fact]

### [Headline 3]
Supporting evidence: [specific findings with sources]
Key data point: [the anchor number or fact]

### Addressing the Counter-Argument
[The objection, why the evidence still supports the recommendation, and the mitigation plan]

### Value-Add Sections (if any)
[Insights from the research base that go beyond the Precision Anchor but materially elevate the deliverable. For each: the insight, why it's valuable, and supporting evidence.]

## Headline Sequence (read-through test)
1. [Headline 1]
2. [Headline 2]
3. [Headline 3]
4. ...

## Precision Anchor Alignment
[Copy the Precision Anchor here. Then state: "The governing message answers the Precision Anchor question [DIRECTLY / PARTIALLY / WITH QUALIFICATION]." If partially or with qualification, explain the gap and what would be needed to close it.]

## Evidence Map
| Headline | Key Evidence | Source | CS Score |
|----------|-------------|--------|----------|

## Appendix Candidates
[Findings that passed the Value-Add Review without qualifying — available if the client asks]
```

Present the synthesis to the user. This is the blueprint that the client-report skill will turn into a polished deliverable.
