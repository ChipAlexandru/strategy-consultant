---
name: engagement-manager
description: >
  Run a full strategy consulting analytical engagement from problem definition through to a client-ready report. Use when someone asks to "run a full analysis", "do a consulting engagement on", "analyze this end to end", "help me with a client engagement", "do the full workflow", or presents a business problem that needs the complete Define → Research → Sense-Check → Synthesize → Deliver treatment. This is the orchestrator skill — it coordinates all other skills in the plugin to produce a comprehensive deliverable.
---

# Strategy Consulting Engagement — Full Analytical Workflow

Orchestrate a complete consulting-grade analytical engagement. This skill coordinates the other skills in sequence, producing an executive-grade client report from a starting business problem.

## Operating Mode
Delivery only. Produce results directly. Flag weak logic inline rather than asking Socratic questions. The user wants outputs, not coaching.

## Workflow

### Phase 1: Define the Problem
Invoke the **problem-definition** skill. Work with the user to sharpen their business question into a decision-oriented problem statement with clear scope and boundaries.

Do not proceed until the user confirms the problem statement.

### Phase 2: Structure Hypotheses (Optional)
Assess whether the problem benefits from a formal hypothesis tree:
- If the question has multiple plausible answers and research needs prioritization → invoke the **hypothesis-tree** skill
- If the question is narrow enough for direct research → skip to Phase 3

If used, present the hypothesis tree to the user and get confirmation on research priorities before proceeding.

### Phase 2.5: Data Source Inquiry (MANDATORY — three required questions)
Before launching research, ask the user about available data sources using the **AskUserQuestion** tool. This step determines the research tier mix and shapes the entire research strategy.

**The following three questions are REQUIRED and must each appear as a separate, clearly worded question in the AskUserQuestion call. You may add additional context-specific questions (e.g., geography focus, deliverable format), but these three must not be omitted, merged, or rephrased beyond recognition:**

1. **Internal/client data** (REQUIRED): Based on the problem statement, suggest 2-3 specific types of internal data that would be most valuable for THIS question and ask whether they are available. Examples: internal strategy documents, store layouts, financial models, operational metrics, customer data. Tailor the examples to the specific engagement — do not use generic placeholders.

2. **Expert interviews** (REQUIRED): Ask explicitly: "Do you have access to expert interviews — either existing transcripts/notes from industry practitioners, or planned interviews we should prepare guides for?" This question must be asked separately from the internal data question because expert data follows a different processing path (Phase 3.5, expert-interview skill). Do NOT merge this with the internal data question.

3. **Other external reference material** (REQUIRED): Ask: "Do you have any other reference material that should inform this research — for example, an industry report, market study, competitor analysis, or third-party dataset?" This captures data sources that are neither internal client data nor expert interviews but still provide valuable context beyond what public web research can find.

**Why these three questions matter:** Each question covers a distinct data tier that follows a different processing path. Internal data (Q1) is analyzed alongside public research in Phase 3. Expert interviews (Q2) activate Phase 3.5 and the expert-interview skill for claim extraction and CS scoring. Other reference material (Q3) feeds into the research brief as supplementary context for the analysts. Together, the answers determine whether the engagement runs as Scenario A (public only), Scenario C (internal + public), Scenario D (public + expert), or Scenario E (all sources).

Record all answers and carry them into the research brief.

### Phase 3: Research
Invoke the **research** skill. This dispatches three agents:
1. **analyst-alpha**: Direct research angle (market data, financials, industry benchmarks)
2. **analyst-bravo**: Complementary angle (competitive dynamics, case studies, contrarian evidence)
3. **research-validator**: Cross-checks both analysts' findings for consistency and source quality

The research brief must include the data availability summary from Phase 2.5. If internal data was provided, analyze it alongside public research. If the user indicated expert interviews are planned, identify the key uncertainties where expert input would be most valuable.

Present the validated research package to the user. Ask if they have additional data or context to contribute before proceeding.

### Phase 3.5: Expert Interviews (if indicated in Phase 2.5)
If the user indicated during the Data Source Inquiry that expert interviews would be available, invoke the **expert-interview** skill. This phase comes AFTER public research because:
- Interview guides are sharper when informed by what the public data already shows
- Questions can target the specific gaps and uncertainties identified during research
- The interviewer knows what to validate vs. what to explore

**Sub-steps:**
1. **Plan**: Based on the research gaps, recommend 3-5 expert profiles ranked by impact on the Precision Anchor question. Present to user for confirmation.
2. **Guide**: Create concise interview guides — each question mapped to a specific information gap, with context on what the public research already found.
3. **Process** (when notes are uploaded): Extract claims, assign CS scores (CS-2 for direct experience, CS-3 for opinion/hearsay), cross-reference against public findings. Flag conflicts and resolve by prioritizing the higher-quality and more precise source.
4. **Integrate**: Feed confirmed, enhanced, and net-new findings back into the research base. Update Research Notes entries.

If expert interviews reveal significant conflicts with public research or surface entirely new information, consider a targeted follow-up research pass before proceeding to sense-check.

### Phase 4: Sense-Check (MANDATORY — produces a written report)
Invoke the **sense-check** skill. This is NOT optional and cannot be replaced with an informal assessment. The sense-check skill prescribes a 7-step process that must produce a written Sense-Check Report containing:
- Claim-by-claim assessment table
- Key vulnerabilities
- Steel-man counter-narrative
- Math checks
- Analytical traps analysis
- Question-Answer Precision Verdict (PRECISE / PARTIAL / DRIFTED)

A DRIFTED verdict is a hard stop — loop back to Phase 3 for targeted research.
A PARTIAL verdict must be carried forward into the synthesis as an explicit qualification.

Present the sense-check report to the user (Checkpoint 3).

COMMON FAILURE MODE: The agent reads the sense-check skill but decides the research is "strong enough" and skips producing the actual report. This defeats the purpose. The discipline of writing each section forces rigor that mental shortcuts do not provide. Always produce the written report.

### Phase 5: Synthesize (MANDATORY — produces a written storyline)
Invoke the **synthesis** skill. This step transforms the evidence into an argument. It is NOT the same as organizing findings by topic — it answers the question "so what should the client do?"

The synthesis skill must produce a written Storyline Document containing:
- One-sentence governing message (tested against the Precision Anchor)
- 2-4 key arguments with evidence mapped to each
- Counter-argument section
- Headline sequence (must read as a coherent argument without supporting text)
- Evidence map (traceability table: headline → evidence → source → CS score)
- Precision Anchor Alignment statement (DIRECTLY / PARTIALLY / WITH QUALIFICATION)

Present the storyline to the user (Checkpoint 4).

COMMON FAILURE MODE: The agent skips synthesis and goes directly from research to the report, organizing findings by topic rather than by argument. The result is a summary, not a synthesis. The test: if you remove all the evidence and read only the headlines, does a decision-oriented argument emerge? If not, the synthesis step was skipped.

### Phase 6: Deliver (MANDATORY — invokes client-report skill)
Invoke the **client-report** skill to produce the final .docx. Do NOT write the document directly using the docx skill alone — the client-report skill contains writing standards, banned words, structure requirements, and a mandatory quality review process that must be followed.

The report MUST include:
- Executive summary (half page)
- Body sections following the synthesis headline sequence, using the "Data → So What → Now What" pattern and industry-standard terminology alongside plain-language explanations
- Counter-argument section addressing: the steel-man counter-narrative, ALL client-raised objections (from the sense-check's Client-Raised Objections Inventory), and foreseeable operational risks
- Specific recommendations — every sourced data point must lead to an actionable recommendation
- Research Notes section (MANDATORY — final section, compiled from the validator's source registry, providing full traceability for every data point in the report)

The client-report quality review MUST include all mandatory checks (5a through 5j), including:
- Citation completeness self-audit (no uncited claims)
- Assumption labeling audit (illustrative vs. sourced numbers clearly distinguished)
- Source-type-aware confidence language audit
- "Data → So What → Now What" pattern check
- Cross-section linkage review
- Client Question Checklist verification (every client question answered or acknowledged)
- Expert-sourced content retention check (no expert finding dropped without explanation)

COMMON FAILURE MODE: The agent bypasses the client-report skill and writes the document directly, producing a well-formatted document that lacks the Research Notes section, the counter-argument section, and the quality review. The client-report skill is not just about formatting — it enforces analytical rigor in the final deliverable.

Present the final document to the user.

## Mandatory User Checkpoints (NON-NEGOTIABLE)

The following checkpoints require presenting output to the user and waiting for their response before proceeding. These are not optional efficiency trade-offs — they are quality gates that catch errors, incorporate user knowledge, and prevent wasted work.

**CHECKPOINT 1 — Problem Statement (Phase 1)**
Present the problem statement, Precision Anchor, AND the Client Question Checklist. Wait for user confirmation.
DO NOT proceed to research until the user confirms.

**CHECKPOINT 2 — Research Package (Phase 3)**
After the validator completes, present the validated research package to the user. Include: key findings summary, evidence strength assessment, and information gaps.
Ask: "Do you have additional data, context, or expert interviews to contribute before I proceed to analysis?"
DO NOT proceed to sense-check until the user responds.
WHY THIS MATTERS: The user may have expert transcripts, internal data, or corrections that change the research base. Skipping this checkpoint means the entire downstream analysis may be built on an incomplete evidence base.

**CHECKPOINT 3 — Sense-Check Report (Phase 4)**
Produce the full sense-check report (claim inventory, triangulation, steel-man, math checks, precision verdict). Present to the user.
DO NOT proceed to synthesis until the user has seen the sense-check results.

**CHECKPOINT 4 — Storyline (Phase 5)**
Present the synthesis output (governing message, headline sequence, evidence map) to the user.
Ask: "Does this storyline answer your question? Any adjustments before I write the report?"
DO NOT proceed to the report until the user approves the storyline.

**Speed vs. quality trade-off:** If the user explicitly asks to "skip the checkpoints" or "just produce the report fast," you may compress checkpoints 2-4 into a single summary. But the default is always to pause at each gate.

## Key Principles Throughout

**Be explicit about evidence quality.** Never present a weak finding as a strong one. Use confidence levels and ranges.

**Be explicit about information boundaries.** Clearly flag what public research can answer vs. what requires client data or expert interviews. Recommend specific data requests and expert profiles where gaps exist.

**Let the user drive pace.** Present output at each phase and wait for confirmation before proceeding. The user may want to inject additional context, redirect the analysis, or skip phases.

**Never pad.** Every sentence in every output must earn its place. If a finding does not change the recommendation, it goes in the appendix or gets cut.

## Quick Reference — Skill Sequence
```
problem-definition → [hypothesis-tree] → data-source-inquiry → research → [expert-interview] → sense-check → synthesis → client-report
                      (optional)          (AskUserQuestion)     (3 agents)   (if interviews available)
```
