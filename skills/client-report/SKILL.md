---
name: client-report
description: >
  Package synthesized findings into an executive-grade Word document (.docx) deliverable. Use when someone asks to "write the report", "create the deliverable", "produce the client document", "draft the final report", "package this into a document", or when the analytical workflow reaches the final delivery phase after synthesis. Also trigger when someone has a completed storyline and needs it turned into a professional, client-ready written report.
---

# Client Report — Executive-Grade Deliverable

Transform the synthesized storyline into a polished .docx report that a senior partner could hand to a client CEO. The document must be clear, direct, and free of the verbal padding that plagues most consulting deliverables.

## Preflight Gate (run BEFORE any other step)

This phase requires upstream state and artifacts. Before doing anything else, verify ALL of the following:

1. `engagement-state.json` exists in the active workspace.
2. `"synthesis"` AND `"storyline-critique"` are in `completed_phases`. (The storyline-critique gate must pass — or the user must explicitly accept open critique risks via `checkpoint_status.checkpoint_4_storyline = "approved"` — before this phase may run.)
3. The following artifacts exist on disk and are non-empty:
   - `storyline.md`
   - `research-validated.md`
   - `sense-check.md`
   - `precision-anchor.md`
   - `client-question-checklist.md`

If ANY required item is missing or empty, STOP. Do not draft an executive summary, do not call the docx skill, do not produce a deliverable. Report the specific missing state field or artifact path and route control back to `engagement-manager`. A report written without a passed storyline-critique is a polished version of an un-pressure-tested argument — the most expensive failure mode in this plugin.

When the gate passes:
- Read `engagement-state.json` and treat its `workspace_path` as the active workspace. Save the deliverable inside it.
- Use `storyline.md` as the authoritative source for governing message, headline sequence, and section structure. Do not reorder sections or rewrite the governing message inside this skill.
- Use `research-validated.md` Source Registry verbatim for the Research Notes section.
- Use `sense-check.md` for the counter-argument section's three sources (steel-man, client-raised objections, evidence-implied risks).
- Use `precision-anchor.md` for the altitude audit (5l) and `client-question-checklist.md` for the Client Question Checklist verification (5h).
- Use `engagement-state.json.deliverable_format` to select Executive Brief vs. Comprehensive vs. Excel vs. PowerPoint mode.

At the end of this phase, after the .docx (or .xlsx / .pptx) is produced, append `"client-report"` to `completed_phases`, update `artifact_paths.final_deliverable`, set `current_phase` to `deliverable-validation`, refresh `next_required_action` and `last_updated`, and write `engagement-state.json`. Do not present the deliverable to the user as final — Phase 6.5 (deliverable-validator) must pass first.

## References (read once, before writing)

- `../../references/altitude-and-precision.md` — altitude qualification rules used in Check 5l. A section that presents the wrong-altitude data without qualification fails the audit.
- `../../references/counter-argument-sources.md` — the three tributaries (steel-man, client-raised objections, evidence-implied risks) the Counter-Argument section must address.
- `../../references/expert-anchor-and-conflicts.md` — expert-anchor rule and strategic conflict handling enforced by Checks 5d and 5e.
- `../../references/research-notes-and-traceability.md` — Source Registry format, CS filtering, and the hard-gate count match enforced by Check 5i. Read this before writing the Research Notes section.
- `references/banned-language.md` — banned words/phrases scanned by Check 5b.

These references are the source of truth. The standards and quality checks below are the phase-specific actions; they reference the doctrine without re-explaining it.

## Writing Standards

### Language Rules
**Do:**
- Write in short, declarative sentences
- Use concrete nouns and active verbs
- State conclusions before evidence
- Use numbers with context ("revenue grew 8%, outpacing the market's 5% average")
- Write for a time-pressed executive who will skim before reading

**Do NOT use any of the following — they are banned from this deliverable:**
- "Leverage" (say "use")
- "Synergies" (say what actually improves and by how much)
- "Unlock value" (say what value, how much, and how)
- "Best-in-class" (say who, specifically, and what they do)
- "Holistic" (say what is included)
- "Ecosystem" (unless literally about biology)
- "Paradigm shift" (describe what actually changed)
- "Move the needle" (say by how much and on what metric)
- "Low-hanging fruit" (describe the specific opportunity)
- "Deep dive" (say "detailed analysis")
- "Going forward" (say the specific time period)
- "At the end of the day" (delete it)
- "Thought leadership" (delete it)
- Any phrase that sounds important but communicates nothing specific

### Tone
Executive, not academic. Direct, not hedging. Confident where the evidence supports confidence. Transparent about uncertainty where it exists. The reader should feel they are getting the unvarnished truth from a trusted advisor, not a sales pitch.

### Precision
- Every number needs a source, a date, and context
- Ranges are more honest than false point estimates ("$2-3B" not "$2.47B")
- Distinguish between facts, estimates, and assumptions explicitly
- "We believe" is fine when followed by "because [evidence]" — but never as a substitute for evidence

## Document Structure

Use the docx skill to create the document. The structure should follow the storyline from the synthesis phase, not a rigid template.

**Executive Brief Mode (4-6 pages — this is the default when confirmed in Phase 2.7):**
When the user selected the executive brief format, enforce these constraints strictly:
- Total body content: 4-6 pages maximum (excluding title page and Research Notes). This is a hard limit, not a target.
- Executive summary: 1 paragraph (3-5 sentences), not half a page
- Body sections: Use bullet points as the primary format. Each bullet = one finding + its implication. Full prose paragraphs only for the governing message and counter-argument section.
- Tables: Maximum 1 table per section, kept compact (no more than 5 rows)
- Recommendations: Numbered, 1-2 sentences each, no extended justification (the body already provides it)
- Research Notes: MANDATORY — condensed to include only sources directly cited in the body, but must be present. No executive brief is complete without source traceability.
- If the content cannot fit in 6 pages, move the least critical findings to a 1-page appendix rather than expanding the body. Prioritize ruthlessly.

**Standard Report Mode (8-15 pages, when comprehensive report is confirmed in Phase 2.7):**
Most reports will include:

### Front Matter
- **Title page**: Client name, engagement title, date, confidentiality notice
- **Executive summary**: The governing message and 2-4 key arguments in ~half a page. A senior executive who reads only this page should understand the recommendation and its basis.

### Body
Organized by the storyline headlines from the synthesis phase. Each section should:
- Open with the headline as a section heading
- Open with the key conceptual insight — the strategic "why" that explains the data
  pattern. When an expert provided a conceptual frame for the topic, that frame is the
  section opener. State it in 1-2 sentences with expert attribution before presenting
  any tables, benchmarks, or data exhibits.
- Then present the structured data (tables, benchmarks, scenarios) as evidence supporting
  the conceptual frame.
- Close with the implication for the client ("so what / now what") and cross-references
  to related sections.

Section structure test: read the first two sentences of each section. Do they state a
principle or insight that the rest of the section supports? If the first thing the reader
sees is a table header or benchmark list, the section structure is inverted. Tables support
insights; they do not replace them.

- Present evidence concisely with source citations
- Include a visual (table, chart, or comparison) where it communicates faster than prose
- For every key data point, follow the **"Data → So What → Now What"** pattern: state the finding, state why it matters for the client's decision, state what the client should do about it
- Use **industry-standard terminology** collected during the research phase, alongside plain-language explanations for readers who may not know the terms (e.g., "proof-of-play reports (verification that ads actually displayed as scheduled)")
- Close with the implication for the client and, where applicable, an explicit cross-reference to related findings in other sections

### Counter-Argument Section
A thorough, honest section addressing risks and objections. This builds credibility.

**Sourcing counter-arguments:** The counter-argument section must draw from three sources, not just the analyst's own reasoning:
1. **The steel-man counter-narrative** from the sense-check phase
2. **Client-raised objections** — every concern, hesitation, or objection the client raised in their call, brief, or messages must be addressed here. Scan the source material systematically for these. Client-raised concerns that go unaddressed are a credibility risk — the client will notice their own question was not answered.
3. **Foreseeable operational risks** — risks that can be inferred from the evidence base itself (e.g., if phased deployment is recommended, address the operational complexity of phasing; if a sales team is needed, address the staffing prerequisite)

For each counter-argument, structure as: "The risk is [X]. We considered this carefully. The evidence suggests [Y], and we recommend [mitigation Z] as a safeguard."

### Recommendations
Specific, actionable, and sequenced. Each recommendation should answer:
- What to do (specific action)
- By when (timeline)
- What it requires (resources, investment, organizational changes)
- What it delivers (expected impact, with honest ranges)

### Appendix (if needed)
Supporting data, detailed methodology, secondary findings that did not make the main storyline but may be useful if the client asks.

### Research Notes (mandatory — always the final section)
This section provides full traceability for every data point used in the report. It is compiled by the research-validator agent and included verbatim from the validated research output. The purpose is not to weigh down the document but to enable the reader to verify any claim with one click.

Format — a simple numbered list:

[1] "The global EV market reached $500B in 2025" — Bloomberg NEF, Annual EV Market Outlook, Jan 2025, https://about.bnef.com/... — CS-1 [VERIFIED]
[2] "Tesla's European market share declined to 17% in Q3 2025" — ACEA, Registration Data Q3 2025, https://www.acea.auto/... — CS-1 [VERIFIED]
[3] "Analysts expect utilization to double by 2028" — FT, March 2025 — CS-2 [VERIFIED]

Each entry quotes the data point as it appears in the report body, followed by the source name, date, actual URL, CS score (CS-1 through CS-4), and verification status. Every number, percentage, and factual claim in the report body must have a corresponding Research Notes entry. If a data point has no verifiable URL, the entry must note this explicitly (e.g., "[URL NOT AVAILABLE — implied from ...]"). Only data points with CS-1, CS-2, or corroborated CS-3 scores may appear.

## Process

### Step 1: Confirm the Storyline
Read the synthesis output. Confirm the governing message, headline sequence, and evidence map are complete. If anything is missing, flag it before writing.

### Step 2: Draft the Executive Summary First
Write the executive summary before the body. This forces clarity — if you cannot summarize the argument in half a page, the storyline is not sharp enough.

### Step 3: Write Each Section
Follow the headline sequence from synthesis. For each section:
- Write the headline as the section heading
- Draft 2-4 paragraphs of evidence-backed prose
- Include one table or data exhibit per section where helpful
- End with a clear "so what" that connects to the next section

### Step 4: Write the Recommendations
Make them specific and sequenced. Number them. Include expected impact ranges and timelines.

### Step 5: Quality Review
Before producing the final document, run every check below. These are not suggestions — each is a mandatory pass.

**5a. Structural coherence check:**
- Read only the section headings in order — does a coherent argument emerge?
- Ensure the executive summary matches the body (they often drift apart during drafting)
- Check total length — most client reports should be 8-15 pages of body content, not 40

**5b. Banned language sweep:**
- Search for every banned word/phrase and replace with concrete language (see banned-language.md)

**5c. Citation completeness self-audit (MANDATORY):**
Scan the entire report body for every factual claim, number, percentage, named example, and benchmark. For each one, verify it has a matching entry in the Research Notes section. Produce a checklist:
- If a data point in the body is missing from Research Notes → either add it (with source and CS score) or remove the unsourced claim from the body
- If an assumption or illustrative number appears in the body → verify it is tagged as such (see 5d below), NOT mixed in with sourced data
- **No factual claim may appear in the body without a corresponding Research Notes entry.** This is the single most important quality gate for credibility.

**5d. Assumption labeling audit (MANDATORY):**
Scan the report for any illustrative calculations, projections, scenario models, or worked examples that use numbers NOT drawn from a sourced data point. For each one:
- The input assumptions must be explicitly labeled: "For illustrative purposes, assuming..." or "Assumed for modeling purposes: ..."
- Illustrative numbers must be visually distinct from sourced data — use italics, a callout box, or a clear verbal marker
- Never present a constructed number with the same confidence framing as a sourced number
- **The test:** Could a reader distinguish, for every number in the report, whether it came from a source or was constructed by the analyst? If not, the labeling is insufficient.

**Expert-anchor check (part of 5d):**
For every quantitative claim in the executive summary and section headlines, verify: if an
expert provided a conditional number on this topic, is the expert's number the headline
anchor? If the report headlines a different number derived from plugin-generated scenario
modeling, the expert's number must be restored as the primary figure and the modeled range
presented as sensitivity context.

If the expert's conditions are judged unlikely in the client's context, the report must
state this explicitly rather than silently replacing the expert's figure. The structure is:
"Expert estimates [X] under [conditions]. Given [client-specific factors], [adjusted range]
is a more conservative planning target." — Both numbers are visible; the reasoning for the
adjustment is transparent.

A report that headlines a plugin-modeled number while burying the expert's sourced figure
in the body text fails this audit.

**5e. Source-type-aware confidence language audit (MANDATORY):**
Scan the report for language that presents data. Verify that the confidence level of the language matches the source type:
- **Expert-confirmed data (CS-1, CS-2 expert interview):** May be stated directly — "Retailers typically deploy 4-6 screens per store."
- **Public research (CS-2 press, CS-2 analyst):** Use hedged attribution — "According to [source]..." or "Industry reports suggest..." or "[Source] estimates..."
- **Single-source or CS-3 data:** Use explicit caveat — "Per [vendor] estimates (not independently verified)..." or "One industry report suggests..."
- **Consultant-constructed assumptions:** Use explicit framing — "For illustrative purposes, assuming..." or "Using an assumed [X]..."
- A report that states a vendor's self-reported market size with the same confidence as a government statistic fails this audit.

**Strategic conflict check (part of 5e):**
Scan the report for any ranking, prioritization, sequencing, or approach recommendation.
For each one, verify: does it align with expert guidance? If public research data implies
a different ranking than the expert provided, the report MUST:
1. Present the expert's view as the primary framing
2. Note the conflicting public data in parentheses
3. Include a flag: "(Consultant to evaluate: [brief description of the tension])"

A report that silently re-ranks expert-guided priorities based on public metrics fails
this audit. The consultant — not the plugin — decides how to resolve strategic conflicts.

**5f. "Data → So What → Now What" pattern check (MANDATORY):**
For sections where the Deliverable Blueprint indicates the client uses the content to make a decision, verify every sourced data point is followed by:
1. **So what** — why this data point matters for the client's decision
2. **Now what** — what the client should do about it (a specific action or recommendation)
For sections where the Deliverable Blueprint indicates the content serves as reference, "Data → So What" is sufficient — the value is the example itself and its relevance to the client's context, not a per-example action item. Data without at least an implication ("so what") is incomplete and belongs in the appendix, not the body.

**5g. Cross-section linkage review (MANDATORY):**
After drafting all sections, review the report as an integrated argument, not as independent answers:
- For each section, ask: "Does any finding here have implications for the conclusions in another section?"
- Where causal chains span sections (e.g., measurement credibility → advertiser adoption → sell-through → payback timeline), insert explicit cross-references: "This [capability/finding] directly supports the [timeline/economics] discussed in Section [X]."
- The deliverable must read as a single integrated argument. If sections could be rearranged without the reader noticing, the linkage is insufficient.

**5h. Client Question Checklist verification (MANDATORY):**
Retrieve the Client Question Checklist from the problem-definition phase. For each item:
- [ ] Verify the question is answered in the report — in the format the client requested
- [ ] If the data does not match the requested format, verify the report either converts it (with a caveat) or explicitly notes the gap and recommends follow-up
- [ ] If a question was deprioritized, verify the report acknowledges this with reasoning
- **No client question may go unanswered without acknowledgment.** The client will notice if their specific request was ignored.

**5i. Research Notes completeness check (HARD GATE — report fails if this does not pass):**
This check is binary. Open the validated research file and count every numbered entry matching the pattern `[N]` in the Research Notes / Source Registry section. That is the expected count. Then count the numbered entries `[N]` in the report's Research Notes section. If the counts do not match, the report FAILS and must be revised before .docx generation.

The Research Notes section must contain the **individual numbered source entries from the validated research**, not a prose summary of them. Each entry must include: the quoted data point, source name, URL (or "[URL NOT AVAILABLE]"), CS score, and verification status — exactly as the validator produced them. "Include verbatim" means transcribe, not summarize.

COMMON FAILURE MODE: When the report is generated programmatically (e.g., via docx-js), the agent avoids encoding dozens of source entries as string literals and instead writes a summary paragraph. This is not acceptable. If the source list is long, read the validated research file at generation time and iterate over entries programmatically — do not hand-code each entry as a literal.

**5j. Expert-sourced content retention check (MANDATORY when expert interviews were
processed):**
If the expert-interview skill produced an Expert Interview Output with Key Findings,
cross-reference every finding marked as FACT or CS-2 against the report body.

For each expert finding, classify as:
- [ ] INCLUDED: The finding appears in the report (possibly rephrased or restructured)
- [ ] INCLUDED IN PARENTHESES: The finding appears as flagged supplementary context
  (because it conflicts with a higher-priority source)
- [ ] EXCLUDED WITH REASON: The finding was deliberately omitted — note why (e.g.,
  not relevant to the Precision Anchor, superseded by client data, contradicted by
  multiple CS-1 sources)
- [ ] MISSING: The finding was dropped without explanation — add it back to the
  appropriate section, or flag in parentheses for consultant decision

No expert-sourced finding may be silently dropped. Each must be either used, flagged,
or explicitly deprioritized with reasoning. The consultant invested time and money to
obtain expert data; the report should use it unless there is a documented reason not to.

**5k. Source Material Awareness Check (MANDATORY):**
Retrieve the Source Material Extraction Log from the research phase. Verify that the author of the report had visibility into every client-provided fact and data point. The purpose of this check is not to force inclusion — it is to ensure nothing was lost by accident. Flag any item from the extraction log that does not appear in the report and was not consciously considered during synthesis. The consultant decides what belongs; this check ensures the decision was made, not defaulted.

**5l. Altitude audit:**
For each section of the report, compare the data presented against the corresponding Precision Anchor sub-question. If the data is at a higher level of aggregation than what the client asked for, the section must include an explicit qualification: what the data shows, what the client asked for, and how to close the gap. A report that presents network totals as the answer to a per-store question — without flagging this — fails the altitude audit.

### Step 6: Produce the .docx
Use the docx skill to create a professionally formatted Word document with:
- Clean, consistent heading styles
- Page numbers
- Table of contents
- Properly formatted tables and exhibits
- Source citations (footnotes or inline)
- Confidentiality notice on the title page

Save the document and present it to the user.

## Reference
For detailed .docx formatting guidance, follow the instructions in the docx skill (which handles fonts, margins, styles, and other formatting details).
