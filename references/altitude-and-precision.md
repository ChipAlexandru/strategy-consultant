# Altitude & Precision — canonical rules

This is the canonical specification of altitude and precision checks across the plugin. Referenced by `research` (Step 5.5), `sense-check` (Step 5), `synthesis` (Step 0 and Step 1), `client-report` (5l), `synthesis-critic`, and `deliverable-validator`. Skills should LINK to this reference rather than re-explaining the doctrine; they keep their phase-specific gates and verdict actions.

## What altitude means

Altitude is the LEVEL OF SPECIFICITY at which evidence answers a question — how zoomed-in or zoomed-out it is, on units that matter to the client.

- **Geography**: per-country vs. region-level vs. global aggregate.
- **Aggregation unit**: per-store vs. per-region vs. network total. Per-SKU vs. per-category. Per-customer-segment vs. blended average.
- **Metric**: revenue impact vs. margin impact vs. EBITDA impact (these are NOT interchangeable).
- **Time period**: this quarter vs. trailing twelve months vs. multi-year average.
- **Definition**: same product/segment/cohort/period definition the client used, or a different one.

## The altitude test

Place the Precision Anchor's success metric and "what a precise answer looks like" sentence next to the candidate finding (or governing message). Ask: does the candidate operate at the same altitude? Classify:

- **PRECISE MATCH** — same level of specificity. Counts as a direct answer.
- **ALTITUDE MISMATCH** — right topic, wrong altitude. Looks like an answer but the client cannot use it. Examples: client asked per-store-by-size, finding gives network total. Client asked country-specific, finding gives global average. Client asked margin impact, finding gives revenue impact.
- **TOPIC MISS** — wrong topic entirely. Exclude or move to Adjacent Findings.

Altitude mismatches are the most dangerous category because they LOOK like answers. The data is relevant, the topic is right, and it is tempting to present it as responsive.

## Required behavior when altitude is wrong

When a finding or governing message has the wrong altitude:

1. **Flag it explicitly.** Use the form "ALTITUDE MISMATCH — we have [X], the client asked for [Y]."
2. **Calculate what can be inferred.** A network total of N screens across S stores gives an average of N/S, but state explicitly that the average masks the by-size distribution.
3. **State what specific data would close the gap** (expert interview, client data request, store audit, etc.).
4. **Carry the qualification forward.** Sense-check downgrades the verdict to PARTIAL at best. Synthesis records "ALIGNMENT: PARTIALLY" or "WITH QUALIFICATION." Client-report surfaces the qualification — it does not bury it.

## Question-Answer Precision Verdict (used by sense-check and synthesis-critic)

Three possible verdicts:

- **PRECISE** — the analysis answers the exact question at the exact altitude.
- **PARTIAL** — the analysis addresses the right topic but at a different altitude, geography, time period, or unit. Or one or more Coverage Dimensions are GAP/THIN.
- **DRIFTED** — the analysis answers a different question entirely (e.g., describes the market when asked whether to enter it).

Verdict actions:
- PRECISE → proceed.
- PARTIAL → proceed only with the qualification carried forward into synthesis and the report.
- DRIFTED → hard stop. Engagement-manager loops back to research with a redirected brief. Do not synthesize.

## Coverage Dimensions check

If the Precision Anchor's Deliverable Blueprint lists Coverage Dimensions (e.g., specific countries, categories, sub-segments), every dimension is part of the precision standard. Build a Coverage Matrix:

| Dimension Unit | Status | Notes |
|----------------|--------|-------|
| <country / category / segment> | COVERED / THIN / GAP | <one-line evidence summary> |

Any unit classified GAP downgrades the verdict to PARTIAL at best. Any unit classified THIN must be flagged for follow-up.

## Where this is enforced

| Phase | Where altitude is checked | What happens on mismatch |
|-------|---------------------------|--------------------------|
| research, Step 5.5 | Answer Altitude Check on every Precision Anchor sub-question | Flag mismatch in research package, calculate what can be inferred, state gap-closing action |
| sense-check, Step 5 | Question-Answer Precision Check | Verdict downgraded to PARTIAL (or DRIFTED) — written into sense-check.md |
| synthesis, Step 0 / Step 1 | Precision Anchor Re-Check + governing-message altitude test | Governing message rewritten or qualification added; Precision Anchor Alignment statement set |
| client-report, 5l | Altitude audit | Section adds explicit qualification; data not presented as a precise answer |
| synthesis-critic, Check 1 / Check 6 | Independent re-check | Storyline FAILed if altitude was hidden |
| deliverable-validator, Check F | Final-deliverable altitude qualification | Deliverable FAILed if upstream qualification was dropped |
