# Data Source Inquiry — three required questions

This is the canonical specification of the Data Source Inquiry. It is referenced by `engagement-manager` (Phase 2.5) and `research` (Step 0). Skills must not rephrase the three required questions beyond recognition or merge them — they cover distinct evidence tiers that follow different processing paths.

## The three required questions (MANDATORY, ASK SEPARATELY)

Use the **AskUserQuestion** tool. Each question must appear as a separate, clearly worded question in the AskUserQuestion call. The tool accepts a maximum of 4 questions per call — if context-specific additions push you past the limit, use a second call. Do NOT omit, merge, or rewrite any of the three required questions.

1. **Internal/client data (REQUIRED).** Based on the problem statement and Precision Anchor, identify 2–3 specific types of internal data that would be most valuable for THIS question and ask whether they are available. Tailor the examples — do not use generic placeholders.

   Examples for a market-entry question:
   - "Do you have internal sales data broken down by geography or channel?"
   - "Do you have customer acquisition cost benchmarks or unit economics from existing markets?"
   - "Do you have any prior market analyses, competitive intelligence, or strategic planning documents on this topic?"

   Examples for a cost-optimization question:
   - "Do you have a detailed cost breakdown by category and business unit?"
   - "Do you have operational efficiency metrics (cycle times, utilization rates, defect rates)?"
   - "Do you have benchmarking data from prior consulting engagements or internal audits?"

2. **External expert interviews (REQUIRED — must be a SEPARATE question).** Ask explicitly: "Do you have access to external expert interviews — either existing transcripts/notes from industry practitioners, or planned interviews we should prepare guides for?"

   This question must be asked separately from the internal data question because expert data follows a different processing path (the `expert-interview` skill). Do NOT merge it with Question 1.

3. **Other external reference material (REQUIRED).** Ask: "Do you have any other reference material that should inform this research — for example, an industry report, market study, competitor analysis, or third-party dataset?"

   This captures data sources that are neither internal client data nor expert interviews but still provide valuable context beyond what public web research can find.

## Why each tier matters

- Internal data (Q1) is analyzed alongside public research and **sets the direction** for the analysis.
- Expert interviews (Q2) activate Phase 3.5 and the `expert-interview` skill for claim extraction and CS scoring; expert claims carry CS-2 weight.
- Other reference material (Q3) feeds into the research brief as supplementary context for the analysts.

If Q2 is never asked, an entire evidence tier is silently excluded.

## Scenario classification

The combined answers determine the research scenario:

| Scenario | Internal data | Expert interviews | Public research |
|----------|---------------|-------------------|-----------------|
| A | — | — | ✓ |
| B | ✓ | — | — |
| C | ✓ | — | ✓ |
| D | — | ✓ | ✓ |
| E | ✓ | ✓ | ✓ |

Record the scenario in `engagement-state.json` (`scenario` field) and carry it into the research brief.

## Capturing answers

Write the full set of answers to `step0-answers.md` in the active workspace. This artifact is required by the research preflight gate and is read by `research-validator` and `engagement-manager`.

## Where the doctrine is enforced

- `engagement-manager` Phase 2.5: orchestrates the inquiry once per engagement and records `scenario` in state.
- `research` Step 0: does not re-ask if Phase 2.5 already produced `step0-answers.md`. If the file is missing, route back to `engagement-manager` rather than re-asking.

Phase-specific implementations should LINK to this reference rather than duplicating the question text.
