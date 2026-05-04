# Expert-anchor & strategic-conflict handling

This is the canonical specification of how expert claims interact with public data and plugin-generated estimates, and how conflicts between expert guidance and metric-based rankings are surfaced (never silently resolved).

Referenced by `synthesis` (Step 3), `client-report` (5d, 5e), `research-validator` (Strategic Conflict Detection), `synthesis-critic`, and `deliverable-validator` (Check I). Skills should LINK to this reference rather than re-explaining; they keep their phase-specific actions.

For the underlying CS-1 to CS-4 scoring scale and source priority hierarchy, see `skills/research/references/research-source-guide.md` — that file is the source of truth for source-quality rules; this reference is the source of truth for HOW expert outputs propagate through synthesis and delivery.

## Expert-anchor principle (quantitative claims)

When an expert provides a CONDITIONAL QUANTITATIVE claim (a specific number with stated conditions), use the expert's figure as the **headline anchor**. Plugin-generated scenarios, sensitivity ranges, and modeled estimates are **context around** the expert's number — never a replacement for it.

Required structure when both an expert figure and a plugin-modeled figure exist:

> "[Expert's number] is achievable when [expert's stated conditions] [Expert, CS-2]. Sensitivity analysis: under [alternative assumptions], the range extends to [modeled range]."

The expert's conditional number is a CS-2 data point from a practitioner with direct experience. The plugin's scenario model is constructed from assumptions that may not themselves be sourced. A constructed number must never displace a sourced number in the headline — it must contextualize it.

This applies to ANY quantitative claim where both an expert figure and a modeled figure exist: payback periods, market sizes, growth rates, cost estimates, adoption timelines, margin targets, etc.

When the expert's conditions are unlikely to be met in the client's specific context, the report must state this explicitly — "Expert estimates [X] under [conditions]; the client's situation differs in [specific ways], suggesting [adjusted range]" — rather than silently substituting the adjusted range as the headline.

## Insight-before-data rule

When an expert provided a conceptual frame for a topic, that frame is the section opener: a 1–2 sentence statement of the principle, with attribution, that tells the reader WHY the data looks the way it does. The structured data follows as evidence supporting the frame.

A section that opens with data tells the reader WHAT. A section that opens with the conceptual insight tells them WHY — which is what they need to make decisions.

## Strategic conflict detection

A STRATEGIC CONFLICT exists when:

- The expert recommends Action A over Action B (qualitative guidance), AND
- Public data provides a metric that would rank Action B above Action A, AND
- The metric operates on a single dimension while the expert's recommendation integrates multiple dimensions.

Strategic conflicts are NEVER silently resolved by the plugin. They must be surfaced at every downstream phase.

Required handling for each strategic conflict:

1. Flag it explicitly in `research-validated.md` Contradictions Found as "STRATEGIC CONFLICT".
2. Record the expert's recommendation as the primary view.
3. Record the public metric as the alternative lens, in parentheses.
4. Add a consultant decision flag: "(Consultant to evaluate: [expert rationale] vs [metric-based rationale])".

Synthesis carries both perspectives forward. The deliverable presents the expert view as primary framing, with the metric in parentheses, plus the flag.

## Where this is enforced

| Phase | What it does |
|-------|--------------|
| research-validator | Detects strategic conflicts; flags in Contradictions Found; never picks a side |
| synthesis, Step 3 | Section openers use expert frame; quantitative claims use expert anchor |
| client-report, 5d | Expert-anchor check — verifies headline figures are expert-anchored, not plugin-anchored |
| client-report, 5e | Strategic conflict check — verifies any ranking carries the expert frame as primary |
| synthesis-critic | Catches storylines that swapped a plugin estimate for an expert anchor |
| deliverable-validator, Check I | Catches deliverables that reversed the expert/metric ordering |

The consultant — not the plugin — decides how to resolve strategic conflicts. The plugin's job is to make sure both perspectives are visible all the way through to the deliverable.
