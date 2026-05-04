---
description: Run a full strategy consulting engagement — from problem definition through research, validation, synthesis, and executive-grade client report
argument-hint: "<business question or topic>"
---

# /engagement — Full Consulting Engagement

> If you see unfamiliar placeholders or need to check which tools are connected, see [CONNECTORS.md](../CONNECTORS.md).

**Important**: This plugin is designed to handle 80–90% of the analytical workload in a strategy engagement — research, evidence validation, structured synthesis, and report drafting — so that the consultant can focus on the 10–20% that creates unique value: client relationship judgment, proprietary insight, and final recommendations. All outputs are intended as high-quality working drafts for expert review, not finished deliverables.

Run a complete consulting-grade analytical engagement on a business question, producing an executive-grade client report.

## Usage

```
/engagement <business question or topic>
```

### Arguments

- `business question or topic` — The business problem, client brief, or analytical question to investigate. Can be:
  - A direct question: "Should we enter the European EV charging market?"
  - A vague brief: "The client wants to grow in Asia"
  - A file upload: client brief, RFP, or project description

If no topic is provided, prompt the user to supply one.

## Workflow

This command invokes the **engagement-manager** skill, which orchestrates the full end-to-end workflow. The phase numbering below mirrors the orchestrator; see `skills/engagement-manager/SKILL.md` for the authoritative phase logic, gates, and state-file conventions.

### Phase 1 — Problem Definition
Invoke the problem-definition skill to sharpen the business question into a decision-oriented problem statement with a Precision Anchor, Client Question Checklist, and Deliverable Blueprint. **Checkpoint 1**: user confirms before proceeding.

### Phase 2 — Hypothesis Tree (Optional)
Invoke hypothesis-tree only when structured decomposition adds value. Skip when the question is narrow enough for direct research.

### Phase 2.5 — Data Source Inquiry (Mandatory)
Ask the user three required questions about available data — internal/client data, external expert interviews, and other reference material. The answers determine the research scenario (A/B/C/D/E) and are recorded in `step0-answers.md`.

### Phase 2.7 — Deliverable Format Confirmation (Mandatory)
Confirm the output format before research begins: Executive Brief (.docx, default), Comprehensive Report (.docx), Excel (.xlsx), or PowerPoint (.pptx). Recorded in `engagement-state.json.deliverable_format`.

### Phase 3 — Research
Invoke the research skill. It dispatches **two analysts in parallel** (analyst-alpha and analyst-bravo, on differentiated angles), then **research-validator validates their memos** sequentially after both are complete. The user may optionally trigger a third analyst-deep pass on under-explored sub-dimensions before validation finishes. **Checkpoint 2**: user reviews the validated research package.

### Phase 3.5 — Expert Interviews (If Indicated)
If Phase 2.5 indicated expert interviews, invoke expert-interview to plan profiles and guides, and/or process uploaded interview notes back into the research base.

### Phase 4 — Sense-Check (Mandatory)
Invoke sense-check to pressure-test findings — triangulation, steel-man, math, precision verdict, analytical traps. **Checkpoint 3**: a DRIFTED verdict is a hard stop.

### Phase 5 — Synthesis (Mandatory)
Invoke synthesis to produce a storyline (governing message, 2–4 key arguments, counter-argument section, headline sequence, evidence map, Precision Anchor Alignment).

### Phase 5.5 — Storyline Critique (Mandatory)
Dispatch the synthesis-critic agent to pressure-test the storyline against precision-anchor, validated research, and sense-check. Produces a PASS / FAIL Storyline Critique Report. **Checkpoint 4**: client-report cannot begin until critique returns PASS, or the user explicitly accepts open risks.

### Phase 6 — Deliver
Invoke the format-appropriate delivery path: client-report skill for .docx (Executive Brief or Comprehensive), xlsx skill for Excel, pptx skill for PowerPoint. Source traceability — Research Notes section (.docx) / Sources sheet (.xlsx) / Sources appendix slide (.pptx) — is required in every format.

### Phase 6.5 — Deliverable Validation (Mandatory)
Dispatch the deliverable-validator agent to audit the produced deliverable against precision-anchor, client-question-checklist, research-validated, sense-check, and storyline. Produces a PASS / FAIL Deliverable Gap Report. **Checkpoint 5**: deliverable is presented to the user only after a PASS verdict.

## Output

A validated client deliverable in the format chosen at Phase 2.7 — Word document (Executive Brief or Comprehensive), Excel workbook, or PowerPoint deck — containing:
- The governing message and 2–4 key arguments
- Evidence-backed body sections following the storyline's headline sequence
- A counter-argument section addressing the steel-man case, every client-raised objection, and every evidence-implied risk
- Specific, sequenced recommendations
- Source traceability appropriate to the format: Research Notes section (.docx), Sources sheet (.xlsx), or Sources appendix slide (.pptx) — non-negotiable in all three
