# Research Notes & source traceability

This is the canonical specification of how source traceability flows from analyst memos through to the final deliverable. Referenced by `analyst-alpha`, `analyst-bravo`, `analyst-deep`, `research-validator`, `client-report` (5c, 5i), and `deliverable-validator` (Checks A and B). Skills should LINK to this reference rather than re-explaining the doctrine; they retain their phase-specific instructions.

For the underlying CS-1 to CS-4 confidence-scoring scale, see `skills/research/references/research-source-guide.md`. This reference does not duplicate the scale — it specifies how scored entries become Research Notes.

## Source Registry entry format (produced by analysts and validator)

Every validated data point has a numbered Source Registry entry of the form:

```
[N] "<exact data point as it would appear in the report body>" — <Source name, publisher, date>, <URL or [URL NOT AVAILABLE — explanation]> — CS-<n> [VERIFIED] | [VERIFIED — corroborated] | [UNVERIFIED — reason]
```

Required fields:
- The data point as a direct quote (exactly as it would appear in the report body).
- Source name, publication/author, date.
- The actual URL where the data can be found or verified, OR an explicit `[URL NOT AVAILABLE — <reason>]` marker.
- CS score (CS-1 through CS-4).
- Verification status.

## CS filtering for Research Notes

| Source CS | Allowed in Research Notes? | Conditions |
|-----------|----------------------------|------------|
| CS-1 | Yes | Direct inclusion |
| CS-2 | Yes | Direct inclusion |
| CS-3 | Only if corroborated | Note the corroborating CS-1 or CS-2 source |
| CS-4 | No | Reject; record in Source Quality Issues; do NOT include |

Estimates derived from adjacent data must be labeled `[ESTIMATE]` with the source and bridging assumption stated in one sentence. Estimates never carry the same confidence framing as a directly sourced fact.

## Final-deliverable Research Notes section

The final `.docx` (or `.xlsx` Sources sheet, or `.pptx` Sources appendix) must contain the **same numbered entries** that the validator produced — verbatim, transcribed, not summarised.

Common failure mode: when the report is generated programmatically (e.g., via docx-js), the agent avoids encoding dozens of source entries as string literals and writes a summary paragraph instead. **This is not acceptable.** If the source list is long, read `research-validated.md` at generation time and iterate over entries programmatically — do not hand-code each entry as a literal.

## Hard-gate count match (deliverable-validator Check A)

Count the entries matching `[N]` in `research-validated.md`'s Source Registry section. Count the entries matching `[N]` in the deliverable's Research Notes (or .xlsx Sources sheet, or .pptx Sources appendix). Report both:

> "Source Registry: X entries. Deliverable Research Notes: Y entries."

If X ≠ Y, the deliverable FAILs Check A and the rest of deliverable-validator's checks are not run. The most common failure is a prose summary replacing the numbered list; if the deliverable's Research Notes contains zero `[N]` entries, flag immediately.

## Body-claim traceability (client-report 5c and deliverable-validator Check B)

Every factual claim, number, percentage, named example, and benchmark in the deliverable's body must have a matching Source Registry entry. If a body claim has no matching entry, either:
- Add the entry (with source and CS score), OR
- Remove the unsourced claim from the body.

Assumptions and illustrative numbers are NOT factual claims and must instead be tagged per the assumption-labeling rule (`client-report` 5d).

## Where this is enforced

| Stage | Producer / Auditor | Action |
|-------|--------------------|--------|
| Research, Step 1 | analyst-alpha, analyst-bravo, analyst-deep | Each finding gets a Source Registry entry per the format above |
| Research, Step 5 | research-validator | Verifies CS scoring; rejects CS-4; corroborates CS-3; produces consolidated Research Notes |
| Synthesis, Step 3 | synthesis skill | Evidence map references entries by `[N]`; does not introduce unsourced claims |
| Delivery, Step 5 | client-report 5c & 5i | Citation completeness self-audit; Research Notes count match |
| QA, Phase 6.5 | deliverable-validator Checks A and B | Hard count match; body-claim spot check |
