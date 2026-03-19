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

This command invokes the **engagement-manager** skill, which orchestrates the full end-to-end workflow:

### Phase 1: Define the Problem
Invoke the problem-definition skill to sharpen the business question into a decision-oriented problem statement with clear scope, a Precision Anchor, and a Deliverable Blueprint.

**Checkpoint 1**: User approves problem statement before proceeding.

### Phase 2: Structure Hypotheses (Optional)
If the problem benefits from structured decomposition, invoke the hypothesis-tree skill to build a MECE hypothesis tree with testable branches. Skip when the question is narrow enough for direct research.

### Phase 3: Data Source Inquiry (Mandatory)
Ask the user three mandatory questions about available data:
1. Internal/client data available
2. Expert interviews (existing transcripts or planned)
3. Other external reference material

### Phase 4: Research
Invoke the research skill, which dispatches three agents in parallel:
- **analyst-alpha**: Independent research thread A (dynamically assigned angle)
- **analyst-bravo**: Independent research thread B (complementary angle with critical thinking mandate)
- **research-validator**: Cross-checks both analysts for consistency, source quality, and gaps

**Checkpoint 2**: User reviews validated research package.

### Phase 5: Expert Interviews (If Indicated)
If expert interview data is available or planned, invoke the expert-interview skill to plan guides and/or process interview notes.

### Phase 6: Sense-Check (Mandatory)
Invoke the sense-check skill to pressure-test all findings through triangulation, steel-manning the counter-argument, math checks, precision verdict, and bias scanning. Produces a written sense-check report.

**Checkpoint 3**: User reviews sense-check report. DRIFTED verdict = hard stop.

### Phase 7: Synthesis (Mandatory)
Invoke the synthesis skill to build a storyline that directly answers the client question, with governing message, headline sequence, and evidence map.

**Checkpoint 4**: User approves storyline before report generation.

### Phase 8: Deliver
Invoke the client-report skill to produce an executive-grade .docx with professional formatting, sourced claims, Research Notes appendix, and 13-point quality audit.

## Output

A complete .docx client report with:
- Executive summary
- Evidence-backed body sections following the storyline
- Counter-argument section
- Specific, sequenced recommendations
- Research Notes appendix with full source traceability
