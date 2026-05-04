---
name: engagement-manager
description: >
  Run a full strategy consulting analytical engagement from problem definition through to a client-ready report. Use when someone asks to "run a full analysis", "do a consulting engagement on", "analyze this end to end", "help me with a client engagement", "do the full workflow", or presents a business problem that needs the complete Define → Research → Sense-Check → Synthesize → Deliver treatment. This is the orchestrator skill — it coordinates all other skills in the plugin to produce a comprehensive deliverable.
---

# Strategy Consulting Engagement — Full Analytical Workflow

Orchestrate a complete consulting-grade analytical engagement. This skill coordinates the other skills in sequence, producing an executive-grade client report from a starting business problem.

## Operating Mode
Delivery only. Produce results directly. Flag weak logic inline rather than asking Socratic questions. The user wants outputs, not coaching.

## Shared references (read once; linked from every phase)

Several rules apply across multiple phases. To avoid drift, the canonical specifications live at the plugin root and every skill links to them rather than re-explaining the doctrine:

- `references/data-source-inquiry.md` — the three required questions, scenario classification, where each tier is processed.
- `references/altitude-and-precision.md` — altitude rules, the precision verdict, Coverage Dimensions check.
- `references/counter-argument-sources.md` — the three tributaries (steel-man, client-raised objections, evidence-implied risks) and the structured counter-argument format.
- `references/expert-anchor-and-conflicts.md` — expert-anchor for quantitative claims, insight-before-data, strategic conflict handling.
- `references/research-notes-and-traceability.md` — Source Registry format, CS filtering, hard-gate count match.
- `skills/research/references/research-source-guide.md` — CS-1 to CS-4 confidence-scoring scale and Data Source Priority Hierarchy. Source of truth for source-quality rules; do not duplicate the scale elsewhere.
- `skills/sense-check/references/analytical-traps.md` — confirmation bias, survivorship, cherry-picking, false precision, and the rest of the trap checklist.
- `skills/synthesis/references/storyline-patterns.md` — when to lead with the answer, comparison-of-options, phased roadmap, etc.
- `skills/client-report/references/banned-language.md` — banned words/phrases scanned by Check G.

When a phase needs to invoke one of these doctrines, the SKILL.md links to the relevant reference rather than re-stating it. Hard gates and phase-specific actions remain in the SKILL.md.

## Skill invocation rule (applies to every phase below)

For every phase in the workflow, invoke the named skill. Its internal preflight gates and content rules are authoritative — do not bypass, summarize, or re-implement them locally inside this orchestrator. If a skill's preflight gate fails, fix the missing upstream artifact (or update engagement-state.json) and retry the skill — do not work around the gate.

This rule replaces the per-phase "Invoke the skill. Its internal gates are authoritative — do not bypass." preambles that previously appeared on every phase below. State it once here; apply it everywhere.

## Workspace convention

This skill is the singular entry point to the plugin. Sub-commands (`/research`, `/define-problem`, `/interview-guide`) are continuation-only and check for the workspace described here before proceeding.

### Namespaced workspaces

Every engagement gets its own folder under `./engagements/`, named with a topic slug and the engagement start date:

```
./engagements/<slug>-<YYYY-MM-DD>/
```

Examples:
- `./engagements/europe-ev-charging-2026-05-03/`
- `./engagements/private-label-defense-2026-05-12/`
- `./engagements/dfi-retail-media-2026-04-21/`

The slug is a 2-5 word lowercase-hyphenated identifier derived from the Precision Anchor question (e.g., "europe-ev-charging" not "client_q1"). The date is the day the engagement was started, in ISO format. Together they make the workspace path unique even when the same client returns multiple times in the same week.

Inside the workspace, the file layout is:

- `engagement-state.json` — the source of truth for resume logic (see schema below). Created at the end of Phase 1 and updated at the end of every successful phase.
- `precision-anchor.md` — the Precision Anchor, produced in Phase 1.
- `client-question-checklist.md` — every explicit question extracted from source materials, produced in Phase 1.
- `source-material-extraction-log.md` — the systematic extraction of every factual claim, data point, named example, and question from user-provided documents, produced in Phase 1.
- `step0-answers.md` — the three data-source-inquiry answers from Phase 2.5 plus the deliverable-format answer from Phase 2.7.
- Per-phase outputs: `hypothesis-tree.md` (if used), `research-brief.md`, `research-alpha.md`, `research-bravo.md`, `research-deep.md` (if used), `research-validated.md`, `expert-interview-notes.md` (if used), `sense-check.md`, `storyline.md`, `storyline-critique.md`, the final deliverable (`.docx` / `.xlsx` / `.pptx`), and `deliverable-gap-report.md`.

**Every phase writes its artifacts inside the active workspace.** No phase may write a phase artifact to the user's bare working directory or to a different engagement's workspace. The active workspace path is recorded in `engagement-state.json` (`workspace_path`) and passed forward to every skill invocation.

### engagement-state.json schema

```json
{
  "engagement_id": "<slug>-<YYYY-MM-DD>",
  "topic": "Should the client enter the European EV charging market?",
  "workspace_path": "./engagements/europe-ev-charging-2026-05-03/",
  "current_phase": "synthesis",
  "completed_phases": [
    "problem-definition",
    "data-source-inquiry",
    "deliverable-format",
    "research",
    "sense-check"
  ],
  "artifact_paths": {
    "precision_anchor": "./engagements/europe-ev-charging-2026-05-03/precision-anchor.md",
    "client_question_checklist": "./engagements/europe-ev-charging-2026-05-03/client-question-checklist.md",
    "source_material_extraction_log": "./engagements/europe-ev-charging-2026-05-03/source-material-extraction-log.md",
    "step0_answers": "./engagements/europe-ev-charging-2026-05-03/step0-answers.md",
    "research_validated": "./engagements/europe-ev-charging-2026-05-03/research-validated.md",
    "sense_check": "./engagements/europe-ev-charging-2026-05-03/sense-check.md",
    "storyline": null,
    "storyline_critique": null,
    "final_deliverable": null,
    "deliverable_gap_report": null
  },
  "checkpoint_status": {
    "checkpoint_1_problem_statement": "approved",
    "checkpoint_2_research_package": "approved",
    "checkpoint_3_sense_check": "approved",
    "checkpoint_4_storyline": "pending",
    "checkpoint_5_deliverable": "pending"
  },
  "next_required_action": "Run synthesis skill — produce storyline.md against precision-anchor.md, research-validated.md, and sense-check.md.",
  "deliverable_format": "executive-brief-docx",
  "scenario": "C",
  "created_at": "2026-05-03T09:14:22Z",
  "last_updated": "2026-05-04T11:08:51Z"
}
```

Field semantics:
- `engagement_id` — globally unique within `./engagements/`. Equals the workspace folder name.
- `topic` — the user-facing engagement question, in plain prose.
- `workspace_path` — relative path to the workspace folder. All artifact paths must live inside it.
- `current_phase` — the phase that is in flight or about to start. One of: `problem-definition`, `hypothesis-tree`, `data-source-inquiry`, `deliverable-format`, `research`, `expert-interview`, `sense-check`, `synthesis`, `storyline-critique`, `client-report`, `deliverable-validation`, `complete`.
- `completed_phases` — ordered list of phases that finished successfully. Phase gates check this list before running.
- `artifact_paths` — one key per known artifact. Value is the path if the artifact has been produced, otherwise `null`.
- `checkpoint_status` — per-checkpoint state. Values: `pending`, `presented`, `approved`, `rejected`. Phases that depend on user approval check this.
- `next_required_action` — a one-sentence human-readable description of what the next skill must do. This is what the resume flow shows the user.
- `deliverable_format` — recorded once Phase 2.7 confirms the format. Used by client-report.
- `scenario` — `A`/`B`/`C`/`D`/`E` per the data-source-inquiry scenarios.
- `created_at` / `last_updated` — ISO 8601 UTC timestamps.

### Resume behavior (mandatory at the start of every `/engagement` invocation)

When `/engagement` is invoked, do this BEFORE creating any new workspace:

1. **Scan `./engagements/` for existing workspace folders.**
   - If the folder does not exist or is empty, treat the user's request as a brand-new engagement and proceed to Phase 1 after creating a new namespaced workspace.
   - If exactly one workspace exists, read its `engagement-state.json` and ask the user: "Resume engagement `<engagement_id>` (next: `<next_required_action>`), or start a new one?" Wait for the answer. If they choose resume, set the active workspace and jump to `current_phase`. If new, create a new namespaced workspace alongside the existing one.
   - If multiple workspaces exist, list them with engagement_id, topic, current_phase, and last_updated. Ask the user which to resume, or whether to start a new one. **Do not guess** — ambiguous resumes are a major source of mixed-engagement contamination.

2. **If `engagement-state.json` is missing but artifacts are present** (e.g., legacy `./engagement/` workspaces from v1.4.0 or earlier, or a workspace that was created before the state file convention existed):
   - Reconstruct state from artifacts:
     - Walk `artifact_paths` keys in phase order. For each artifact found on disk, mark its phase as completed and record the path.
     - Set `current_phase` to the first phase whose required artifact is missing (or `complete` if all are present).
     - Set `next_required_action` to the corresponding skill invocation.
   - Write the reconstructed `engagement-state.json` to the workspace before continuing. Tell the user: "Reconstructed engagement state from artifacts. Continuing from `<phase>`."

3. **Legacy `./engagement/` migration.** If a bare `./engagement/` folder is present (the v1.4.0 layout), treat it as a single legacy workspace:
   - Read its artifacts and reconstruct state per (2) above.
   - Write `engagement-state.json` directly into `./engagement/` so future continuations resolve correctly.
   - Do NOT silently move or rename the folder — that would break paths the user may have linked elsewhere. Instead, record `workspace_path: "./engagement/"` in the state file and continue using that path. New engagements still use `./engagements/<slug>-<date>/`; the legacy path is preserved as-is for backward compatibility.

4. **State updates.** At the end of every successful phase, append the phase to `completed_phases`, set the new `current_phase`, update `artifact_paths`, refresh `last_updated`, and set `next_required_action`. Sub-commands invoked as continuations must read `engagement-state.json` first and write it back at the end of the phase they ran. The state file is the single resume coordinator — do not branch on artifact presence alone.

Do not scatter phase outputs across the user's working directory, and do not create a fresh workspace inside a sub-command — that rebuilds the orchestrator piecemeal.

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

Run the inquiry once per engagement, BEFORE research begins. The three required questions (Internal/client data, External expert interviews, Other reference material), the rule that they must be asked as separate questions, the scenario classification (A/B/C/D/E), and the answer-recording conventions are specified in `references/data-source-inquiry.md`. **Read that file and follow it verbatim** — do not paraphrase the three required questions, and do not merge Q1 and Q2.

What this phase does in the orchestration flow:
1. Tailors Q1's example data types to the specific engagement (the Precision Anchor's Question and Decision should drive what to suggest).
2. Calls AskUserQuestion with all three required questions (plus any context-specific additions, max 4 per call; use a second call if needed).
3. Writes all answers to `step0-answers.md` in the active workspace.
4. Sets `engagement-state.json.scenario` to A / B / C / D / E.
5. Carries the answers into the research brief in Phase 3.

This phase is the single owner of the inquiry. The `research` skill reads `step0-answers.md` and does NOT re-ask.

### Phase 2.7: Deliverable Format Confirmation (MANDATORY)
After the Data Source Inquiry, use the **AskUserQuestion** tool to confirm the deliverable format. This question must be asked BEFORE research begins so the synthesis and delivery phases know what to produce.

**Important:** The format choice does NOT affect research quality or depth. Research is always driven by the Precision Anchor and Coverage Dimensions — the agents investigate the question thoroughly regardless of output format. The format choice only determines how findings are presented in the final deliverable.

**Question**: "The default deliverable is a concise executive Word document (4-6 pages, bullet-driven, with sourced recommendations and Research Notes). Would you prefer a different format?"

**Options**:
- **Executive brief (4-6 pages, Word)** — Concise, bullet-driven, focused on key findings and actionable recommendations. (This is the default.)
- **Comprehensive report (10-20 pages, Word)** — Full analytical narrative with detailed evidence, counter-arguments, and appendix.
- **Excel** — Structured spreadsheet. Best when the deliverable must map findings across many dimension intersections.
- **PowerPoint** — Slide-based deliverable for presenting to stakeholders.

If the user requests a format not listed above, confirm that you can produce it and adapt the delivery phase accordingly.

**Carry the format choice forward** to the synthesis phase and the client-report/delivery phase. The Deliverable Blueprint from problem-definition should be updated to reflect the confirmed format.

### Phase 3: Research
Include the Deliverable Blueprint from the Precision Anchor in the brief/input for this phase.

Invoke the **research** skill. It dispatches **two analysts in parallel**, then **research-validator** runs sequentially after both memos are complete:
1. **analyst-alpha**: Direct research angle (market data, financials, industry benchmarks) — runs in parallel with bravo
2. **analyst-bravo**: Complementary angle (competitive dynamics, case studies, contrarian evidence) — runs in parallel with alpha
3. **research-validator**: Dispatched only after research-alpha.md AND research-bravo.md exist; cross-checks both analysts' findings for consistency, CS scoring, and Precision Anchor alignment, and produces research-validated.md

The research brief must include the data availability summary from Phase 2.5. If internal data was provided, analyze it alongside public research. If the user indicated expert interviews are planned, identify the key uncertainties where expert input would be most valuable.

After the validator completes, the research skill will present an executive summary and a Deep Research assessment identifying under-explored sub-dimensions. The user can choose to dispatch a third "deep dive" agent targeting those specific gaps, or proceed with the existing research base.

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
Include the Deliverable Blueprint from the Precision Anchor in the brief/input for this phase.

Invoke the **synthesis** skill. This step transforms the evidence into an argument. It is NOT the same as organizing findings by topic — it answers the question "so what should the client do?"

The synthesis skill must produce a written Storyline Document containing:
- One-sentence governing message (tested against the Precision Anchor)
- 2-4 key arguments with evidence mapped to each
- Counter-argument section
- Headline sequence (must read as a coherent argument without supporting text)
- Evidence map (traceability table: headline → evidence → source → CS score)
- Precision Anchor Alignment statement (DIRECTLY / PARTIALLY / WITH QUALIFICATION)

Present the storyline to the user (Checkpoint 4) — but DO NOT proceed to client-report until Phase 5.5 (storyline critique) returns PASS, OR the user explicitly accepts the open risks listed in the critique.

COMMON FAILURE MODE: The agent skips synthesis and goes directly from research to the report, organizing findings by topic rather than by argument. The result is a summary, not a synthesis. The test: if you remove all the evidence and read only the headlines, does a decision-oriented argument emerge? If not, the synthesis step was skipped.

### Phase 5.5: Storyline Critique (MANDATORY — independent critic, not the synthesizer)

Synthesis is the highest-risk phase in the workflow because the agent who writes the storyline cannot reliably judge whether it has converted adjacent findings into a persuasive but wrong narrative. The same author should not be the only judge of whether the governing message answers the Precision Anchor.

Dispatch the **synthesis-critic** agent. Its full role and required inputs are defined in `agents/synthesis-critic.md`.

**Process:**
1. Dispatch synthesis-critic with these inputs (paths come from `engagement-state.json.artifact_paths`):
   - `storyline` (`storyline.md`)
   - `engagement-state.json`
   - `precision_anchor` (`precision-anchor.md`)
   - `client_question_checklist` (`client-question-checklist.md`)
   - `research_validated` (`research-validated.md`)
   - `sense_check` (`sense-check.md`)

2. The critic runs eight checks (governing message altitude, evidence backing, [ADJACENT] vs. [DIRECT] handling, client-objection carry-forward, headline-sequence-as-argument, gap qualification, Deliverable Blueprint coverage, value-add precedence) and writes `storyline-critique.md` to the workspace with a binary PASS / FAIL verdict.

3. **If PASS**: present both the storyline and the critique to the user at Checkpoint 4. On user approval, append `"storyline-critique"` to `completed_phases` and proceed to Phase 6.
4. **If FAIL**: route control back to synthesis with the critique. Regenerate `storyline.md`, then re-run synthesis-critic. **Client-report cannot begin until either (a) synthesis-critic returns PASS, or (b) the user, at Checkpoint 4, explicitly accepts the open risks listed in the FAIL critique.** When the user accepts open risks, record this in `engagement-state.json` (`checkpoint_4_storyline = "approved"` AND append `"storyline-critique"` to `completed_phases` with the acceptance noted in `next_required_action`). Without one of these two outcomes, the client-report preflight gate will block.

**Why this exists, and why it is scoped to synthesis only.** Synthesis is where adjacent findings become persuasive. An independent critic on this phase has more value than a second self-check on every phase. We deliberately do NOT add a critic for problem-definition, research, or sense-check — those phases either already have independent validators (research-validator) or do not produce a persuasive narrative that can drift. Adding a critic everywhere would be process inflation. Adding one here addresses the specific shortcutting we observe.

### Phase 6: Deliver (MANDATORY)
Include the Deliverable Blueprint from the Precision Anchor in the brief/input for this phase, along with the confirmed deliverable format from Phase 2.7.

**Format-specific delivery:**

- **Executive brief or Comprehensive report (.docx)**: Invoke the **client-report** skill. Do NOT write the document directly using the docx skill alone — the client-report skill contains writing standards, banned words, structure requirements, and a mandatory quality review process. For executive briefs, enforce a strict 4-6 page limit (see client-report skill, Executive Brief Mode).

- **Excel (.xlsx)**: Use the xlsx skill. Let the Deliverable Blueprint and the user's stated needs guide the structure. Do not over-engineer — apply the default xlsx skill and ask the user for any structural preferences (e.g., how to organize rows/columns) if not already clear from the Deliverable Blueprint.

- **PowerPoint (.pptx)**: Use the pptx skill. Let the synthesis storyline guide the slide structure. Do not over-engineer — apply the default pptx skill and ask the user for any structural preferences if not already clear.

**Research Notes / source traceability requirement:** Regardless of format, source traceability must be included — adapted to the format. For Word documents: the Research Notes section as specified in the client-report skill. For Excel: a Sources sheet listing every reference cited in the matrix cells. For PowerPoint: a Sources appendix slide. The traceability requirement is non-negotiable; the specific format adapts.

The report MUST include:
- Executive summary (half page)
- Body sections following the synthesis headline sequence, using the "Data → So What → Now What" pattern and industry-standard terminology alongside plain-language explanations
- Counter-argument section addressing: the steel-man counter-narrative, ALL client-raised objections (from the sense-check's Client-Raised Objections Inventory), and foreseeable operational risks
- Specific recommendations — every sourced data point must lead to an actionable recommendation
- Research Notes section (MANDATORY — final section, compiled from the validator's source registry, providing full traceability for every data point in the report)

The client-report quality review MUST include all mandatory checks (5a through 5l), including:
- Citation completeness self-audit (no uncited claims)
- Assumption labeling audit (illustrative vs. sourced numbers clearly distinguished)
- Source-type-aware confidence language audit
- "Data → So What → Now What" pattern check
- Cross-section linkage review
- Client Question Checklist verification (every client question answered or acknowledged)
- Expert-sourced content retention check (no expert finding dropped without explanation)

COMMON FAILURE MODE: The agent bypasses the client-report skill and writes the document directly, producing a well-formatted document that lacks the Research Notes section, the counter-argument section, and the quality review. The client-report skill is not just about formatting — it enforces analytical rigor in the final deliverable.

### Phase 6.5: Deliverable Validation (MANDATORY — no agent audits its own output)
The agent that wrote the report cannot objectively audit it. Dispatch the dedicated **deliverable-validator** agent to read the generated deliverable alongside the upstream artifacts and produce a Deliverable Gap Report.

**Why this exists:** The client-report skill specifies mandatory quality checks (5a–5l), but when the same agent that wrote the report also runs the checks, it has sunk-cost bias toward what it already produced. The research phase already solves this problem — two analysts write, a separate validator checks. This phase extends that pattern to delivery.

**Why a dedicated agent (not research-validator):** Research-validator is scoped to analyst memos — its checks are CS scoring, source spot-checking, and Precision Alignment of findings. Final-deliverable QA is a different job: counting Research Notes against the source registry, mapping counter-arguments back to the sense-check inventory, verifying the Client Question Checklist, and detecting altitude qualifications and banned-language slips in the produced .docx / .xlsx / .pptx. Re-using research-validator for both blurs the role and creates routing ambiguity. Use **deliverable-validator** here.

**Process:**
1. Dispatch the **deliverable-validator** agent with these inputs (paths come from `engagement-state.json.artifact_paths`):
   - `final_deliverable` (the generated .docx / .xlsx / .pptx)
   - `engagement-state.json`
   - `precision_anchor` (`precision-anchor.md`)
   - `client_question_checklist` (`client-question-checklist.md`)
   - `research_validated` (`research-validated.md`)
   - `sense_check` (`sense-check.md`)
   - `storyline` (`storyline.md`)

2. The validator runs the checks defined in `agents/deliverable-validator.md` (Research Notes count match, source traceability, counter-argument coverage, client question coverage, headline-to-section fidelity, altitude qualification, banned language, assumption labeling, expert-anchor / strategic conflict, format-specific). Check A (Research Notes count match) is a hard gate.

3. The validator writes `deliverable-gap-report.md` to the workspace with a binary PASS / FAIL verdict, and updates `engagement-state.json` per its agent definition.

4. **If FAIL**: route control back to client-report with the gap list. Fix the gaps in the deliverable, then re-run deliverable-validator. Do not present to the user until PASS.

5. **If PASS**: present the validated deliverable to the user.

COMMON FAILURE MODE: The agent decides the report "looks good enough" and skips this phase. This is the phase that would have caught the most common delivery failure — omitted Research Notes, missing sources, dropped client questions. It adds one agent call. Do not skip it.

## Mandatory User Checkpoints (NON-NEGOTIABLE)

The following checkpoints require presenting output to the user and waiting for their response before proceeding. These are not optional efficiency trade-offs — they are quality gates that catch errors, incorporate user knowledge, and prevent wasted work.

**CHECKPOINT 1 — Problem Statement (Phase 1)**
Present the problem statement, Precision Anchor (including the Deliverable Blueprint), AND the Client Question Checklist. Wait for user confirmation.
DO NOT proceed to research until the user confirms.

**CHECKPOINT 2 — Research Package (Phase 3)**
After the validator completes, present the validated research package to the user. Include: key findings summary, evidence strength assessment, and information gaps.
DO NOT proceed to sense-check until the user responds.

**CHECKPOINT 3 — Sense-Check Report (Phase 4)**
Produce the full sense-check report (claim inventory, triangulation, steel-man, math checks, precision verdict). Present to the user.
DO NOT proceed to synthesis until the user has seen the sense-check results.

**CHECKPOINT 4 — Storyline + Critique (Phase 5 / 5.5)**
Present BOTH the synthesis output (governing message, headline sequence, evidence map) AND the synthesis-critic's Storyline Critique Report.
- If the critique returned PASS, ask: "The storyline passes the independent critique. Any adjustments before I write the report?"
- If the critique returned FAIL, present the failed checks and ask: "The independent critique flagged the issues above. Do you want me to (a) regenerate the storyline to address them, or (b) accept these open risks and proceed to the report anyway?"
DO NOT proceed to the report until the user has either approved a PASS critique OR explicitly accepted the open risks of a FAIL critique. If they accept open risks, record this in engagement-state.json as described in Phase 5.5.

**CHECKPOINT 5 — Validated Deliverable (Phase 6.5)**
After deliverable-validator returns PASS, present the validated deliverable and the Deliverable Gap Report to the user. If FAIL, do not present — return to client-report.

## Key Principles Throughout

**Be explicit about evidence quality.** Never present a weak finding as a strong one. Use confidence levels and ranges.

**Be explicit about information boundaries.** Clearly flag what public research can answer vs. what requires client data or expert interviews. Recommend specific data requests and expert profiles where gaps exist.

**Let the user drive pace.** Present output at each phase and wait for confirmation before proceeding. The user may want to inject additional context, redirect the analysis, or skip phases.

**Never pad.** Every sentence in every output must earn its place against the Deliverable Blueprint. What counts as earning its place depends on what the client needs: driving a recommendation, filling a coverage dimension, providing a reference example the client will return to.

## Quick Reference — Skill Sequence
```
problem-definition → [hypothesis-tree] → data-source-inquiry → deliverable-format → research → [deep-research] → [expert-interview] → sense-check → synthesis → storyline-critique → deliver → deliverable-validation
                      (optional)          (AskUserQuestion)      (AskUserQuestion)   (3 agents)  (user-initiated)   (if interviews)                              (synthesis-critic)  (format-aware)   (deliverable-validator)
```
