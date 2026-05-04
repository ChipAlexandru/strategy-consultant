---
name: research
description: >
  Internal phase of the strategy-consultant engagement — invoke via engagement-manager, not directly. Conduct thorough, multi-tier research on a client question by dispatching two independent research agents and a validation agent. Use when someone asks to "research this topic", "find evidence for", "investigate this market", "gather data on", "what does the evidence say about", or when the analytical workflow reaches the research phase after problem definition. Also trigger when someone uploads client data or expert interview notes that need to be analyzed alongside public research.
---

# Research — Parallel Investigation with Validation

Conduct rigorous research by deploying two independent research agents working in parallel, followed by a validation agent that cross-checks their findings. This three-agent architecture reduces confirmation bias and produces a more trustworthy evidence base than a single research pass.

## Preflight Gate (run BEFORE any other step)

This phase requires upstream state and artifacts. Before doing anything else, verify ALL of the following:

1. `engagement-state.json` exists in the active workspace.
2. `"problem-definition"` is in `completed_phases`.
3. The following artifacts exist on disk and are non-empty:
   - `precision-anchor.md`
   - `client-question-checklist.md`
   - `source-material-extraction-log.md`
   - `step0-answers.md`

If ANY required item is missing or empty, STOP. Do not run Step 0, do not write a research brief, do not dispatch agents. Report the specific missing state field or artifact path to the user and route control back to `engagement-manager`. Do NOT reconstruct upstream context locally — the orchestrator owns that.

When the gate passes:
- Read `engagement-state.json` and treat its `workspace_path` as the active workspace. All artifacts produced in this phase write into that workspace.
- Use the `precision-anchor.md` and `client-question-checklist.md` from the workspace as authoritative — do not paraphrase or rewrite them inside this skill.

At the end of this phase, after `research-validated.md` is written and Checkpoint 2 is approved, append `"research"` to `completed_phases`, set `current_phase` to the next phase (`expert-interview` if scenario D/E, otherwise `sense-check`), update `artifact_paths.research_validated`, set a new `next_required_action`, refresh `last_updated`, and write `engagement-state.json`.

## Data Source Priority Hierarchy and Scenarios

Source priority (Internal data > Expert interviews > Public research), conflict-resolution rules, attribution rules by source type, and the underlying CS-1 to CS-4 scoring scale are specified in `references/research-source-guide.md`. **Read that file before dispatching analysts.** It is the source of truth for source-quality rules; do not re-explain them inside this SKILL.

The five scenarios (A/B/C/D/E) and which evidence tiers each engagement runs against are specified in `../../references/data-source-inquiry.md` (at the plugin root). The active scenario is recorded in `engagement-state.json.scenario` after Phase 2.5 completes.

What this skill does with the hierarchy:
- Reads `engagement-state.json` to determine the scenario and `step0-answers.md` for tier-specific details.
- Builds a research brief that gives analysts the scenario-appropriate framing (Step 1 below).
- For scenarios B / C / E, includes Step 4 (Process Client Data) alongside the public research dispatch.
- For scenarios D / E, hands off to `expert-interview` after validation.

## Process

### Step 0: Data Source Inquiry (deferred to engagement-manager Phase 2.5)

In an active engagement, the Data Source Inquiry is owned by `engagement-manager` (Phase 2.5) and runs once per engagement. Its three required questions, scenario classification (A/B/C/D/E), and answer-recording conventions are specified in `references/data-source-inquiry.md` (at the plugin root). Do not re-ask the questions here.

**Within this skill, the preflight gate already verified that `step0-answers.md` exists and is non-empty.** Read it from the active workspace. The answers determine:

- Which research scenario applies (recorded in `engagement-state.json.scenario`).
- Whether internal data must be analyzed alongside public research (Step 4).
- Whether expert interviews are planned (Phase 3.5 will be invoked after this skill).
- Whether other reference material should be summarized into the research brief.

**If `step0-answers.md` is missing** (i.e., this skill was somehow invoked before Phase 2.5 ran), STOP and route back to `engagement-manager`. Do not re-run the inquiry inside this skill — that rebuilds the orchestrator piecemeal and risks divergent question phrasings between engagements.

For standalone runs of `/research` outside of engagement-manager (which the continuation-only command file should already prevent), the same rule applies: the inquiry is the orchestrator's job, not this skill's.

### Step 0.5: Systematic Source Material Extraction (MANDATORY)
Before writing the research brief, perform a systematic extraction pass on **every source document** provided by the user — client briefs, call transcripts, uploaded documents, prior analyses, and messages.

**Document-structure-aware extraction:** The extraction must preserve the structural coordinates of the original document so that every downstream phase can reference source material at the level of granularity the client thinks in. A client who provided a 30-slide deck thinks in slides; a client who provided a 20-page report thinks in sections and pages. If the extraction flattens these into a thematic summary, the structural reference is lost and cannot be recovered later.

**Step 0.5a: Structural Index (do this FIRST for every document)**
Before extracting claims, build a lightweight structural index of each document:

- **Slide decks / presentations (.pptx, .pdf pitch decks):** List every slide by number with a 5-10 word summary of its content. This is the reference grid that all subsequent extraction anchors to.
- **Reports / documents (.docx, .pdf reports):** List every section heading (or page break for unstructured docs) with the page number and a 5-10 word summary.
- **Spreadsheets / data files:** List every tab/sheet name, the column headers, and the row count.
- **Transcripts / call notes:** List the topics discussed in order, with approximate timestamps or paragraph ranges.

The structural index is compact (typically 1-2 pages even for a 60-slide deck). Its purpose is to give every downstream phase — research analysts, the validator, synthesis, and the report author — a map of the source document they can reference by coordinate (slide number, page, section, tab) rather than by memory.

**Step 0.5b: Content Extraction (anchored to the structural index)**
For each document, extract:

1. Every factual claim, data point, named example, and benchmark
2. Every question, request, or specification the client raised
3. Every concern, objection, or hesitation the client expressed
4. Log all extractions as a numbered checklist, **with structural coordinates**

**Source Material Extraction Log format:**
```
SOURCE MATERIAL EXTRACTION LOG
Document: [name/description]
Document type: [slide deck / report / spreadsheet / transcript / other]

STRUCTURAL INDEX:
[Slide/page/section list — see 0.5a above]

FACTUAL CLAIMS & DATA POINTS:
[1] [Claim/data point] — [Slide X / Page Y / Section Z]
[2] ...

CLIENT QUESTIONS & REQUESTS:
[1] [Question/request] — [Slide X / Page Y / Section Z]
[2] ...

CLIENT CONCERNS & OBJECTIONS:
[1] [Concern/objection] — [Slide X / Page Y / Section Z]
[2] ...

KEY CONTENT FOR CROSS-REFERENCING:
[For reference documents the client provided as examples or benchmarks
(e.g., a competitor's pitch deck, an industry report), identify the 3-5
most important pages/slides that contain insights the client likely wants
the analysis to engage with. These are the pages the analyst should cite
by number when comparing the client's situation to the reference.]
```

During the writing phase, verify that each extracted point is either (a) incorporated into the report with its structural coordinate preserved, (b) explicitly deprioritized with reasoning, or (c) flagged for the consultant. **Nothing from the source material should be silently dropped.**

The Source Material Extraction Log is a first-class artifact — it travels with the Precision Anchor, the Client Question Checklist, and the Deliverable Blueprint through every downstream phase. Its purpose is visibility, not forced inclusion: downstream phases must be aware of what the client provided so they can make deliberate decisions about what to use, rather than losing material by accident.

**Structural reference rule for all downstream phases:** When the deliverable references a finding that originated from or relates to a provided source document, it should cite the structural coordinate (e.g., "as shown in the Kroger deck, p16-17" or "DFI deck, Slide 25"). This specificity serves two purposes: (1) the client can immediately locate the reference, and (2) the consultant can verify the plugin's interpretation against the original.

### Step 1: Write the Research Brief
Before dispatching agents, write a clear research brief that includes:
- **The Precision Anchor** (from the problem-definition phase) — include it verbatim at the top of the brief. This is the reference against which all findings will be judged for relevance.
- The client question (from the problem-definition phase)
- **The Client Question Checklist** (from the problem-definition phase) — include it so analysts know the specific questions the client needs answered.
- **The Source Material Extraction Log** — include the full log WITH the Structural Index. Instruct analysts: "When your research findings relate to content in a provided source document, cite the specific structural coordinate (slide number, page, section) alongside your finding. For example: 'Kroger's closed-loop attribution (see provided Kroger deck, p20-21) is the industry standard that DFI's reporting should benchmark against.' This cross-referencing is essential — the deliverable must show the client that the analysis engaged with the specific materials they provided, not just the topic in general."
- **Data availability summary** (from Step 0): What internal data is available? What expert interviews are planned? Is this public-only or multi-source? This shapes what the analysts should prioritize and where they should flag gaps for internal data to fill.
- Specific sub-questions or hypothesis branches to investigate (from hypothesis-tree, if used)
- Any known constraints or context the agents need
- What "good evidence" looks like for this question
- **Relevance instruction to analysts**: "Your findings must directly address the question in the Precision Anchor. If your research leads to findings that are interesting but address an adjacent or different question, place them in a separate 'Adjacent Findings' section and explain how they relate (or don't) to the original question. Do not let adjacent findings displace direct answers."
- **Industry terminology instruction to analysts**: "As part of your research, identify and collect the standard industry-specific terminology, jargon, and technical vocabulary used by practitioners in this domain. Record these terms with brief definitions in a dedicated 'Industry Terminology' section of your output. These terms will be used in the report alongside plain-language explanations."
- **Outcome data instruction to analysts**: "For every competitor or case study example, capture both the mechanism (what they do) and the measurable outcome (what results it produced — revenue, conversion, adoption rate, cost reduction, engagement metrics). A competitor example without a quantified outcome is incomplete. If no outcome data is publicly available, note this explicitly rather than silently omitting it."
- **Source traceability instruction to analysts**: "Every factual claim must include: (a) the source name, (b) a working URL or the marker [NO URL]. When you derive an estimate from adjacent data, label it [ESTIMATE] and state the source and bridging assumption in one sentence. Never present an estimate with the same confidence framing as a directly sourced fact."

### Step 2: Generate Differentiated Research Angles (DYNAMIC — do not use fixed categories)

Before dispatching agents, analyze the Precision Anchor, hypothesis branches, and research brief to generate TWO custom research angles tailored to THIS specific question. The angles must be:

1. **Distinct**: Each angle covers meaningfully different territory — different source types, different sub-questions, or different analytical lenses. If the two angles would lead to the same first 5 Google searches, they are not distinct enough.
2. **Relevant**: Both angles directly serve the Precision Anchor. Do not assign an angle just because it sounds rigorous — it must help answer the actual question.
3. **Comprehensive together**: The union of both angles should cover the full evidence surface the question demands. No critical sub-question should fall outside both angles.

**How to generate angles:**
- Read the Precision Anchor and hypothesis branches
- Identify the 4-6 most important evidence threads the question requires
- Group those threads into two clusters that are internally coherent and externally distinct
- Name each angle in 5-10 words that make the scope immediately clear
- Write a 2-3 sentence scope description for each, specifying what source types and sub-questions fall within it

**Examples of dynamic angle generation:**

| Precision Anchor | Angle A | Angle B |
|---|---|---|
| "Should client enter European EV charging?" | "EV adoption demand curves and charging infrastructure economics" | "Competitive landscape, regulatory regimes, and failed market entries" |
| "How should client respond to private-label threat?" | "Private label penetration trends and consumer switching drivers" | "Branded manufacturer defense strategies and retailer negotiation dynamics" |
| "What is the optimal pricing strategy for new SaaS product?" | "Willingness-to-pay data and competitive pricing benchmarks" | "Pricing model structures, packaging psychology, and churn-price sensitivity" |
| "Should client acquire TargetCo?" | "TargetCo financials, growth trajectory, and asset valuation" | "Integration risks, cultural factors, and comparable M&A outcomes" |

**Do NOT fall back to generic categories** like "market data vs. competitive dynamics" or "quantitative vs. qualitative." The angles must be specific to the question being researched.

**Deliverable Blueprint check:** When the Precision Anchor includes a Deliverable Blueprint with Coverage Dimensions, ensure the two research angles together will cover all dimensions. If coverage dimensions include geographies or categories, at least one angle should be organized by that dimension rather than purely by topic.

### Step 3: Dispatch Agents in Parallel (BOTH agents required)
Use the Agent tool to dispatch BOTH analyst agents simultaneously in the SAME message (this is critical — a single message with two Agent tool calls ensures true parallel execution). Pass each one:
- The research brief
- Their dynamically generated research angle (name + scope description from Step 2)
- Instructions to write their findings to a file

```
Dispatch analyst-alpha with:
"Research brief: [brief]. Your assigned research angle: [Angle A name — scope description]. Write findings to research-alpha.md"

Dispatch analyst-bravo with:
"Research brief: [brief]. Your assigned research angle: [Angle B name — scope description]. Write findings to research-bravo.md"
```

**Verification:** Before proceeding to Step 5, confirm that BOTH of the following files exist and contain substantive findings:
- research-alpha.md (from analyst-alpha)
- research-bravo.md (from analyst-bravo)

If only one file exists, the other analyst was not dispatched. Go back and dispatch the missing analyst before proceeding to validation.

COMMON FAILURE MODE: The agent dispatches analyst-alpha and, upon receiving a comprehensive response, decides analyst-bravo is unnecessary. This defeats the purpose of parallel investigation. The value of two analysts is not redundancy — it is that they approach the question from different angles, reducing confirmation bias and increasing coverage. Even if analyst-alpha produces excellent results, analyst-bravo may surface contrarian evidence, failure cases, or competitive dynamics that alpha missed.

### Step 4: Process Client Data (if available)
While agents run on public research (or after they return), analyze any uploaded client data:
- Look for the story in the numbers before being told what to find
- Cross-reference internal metrics against the public benchmarks from Tier 1
- Flag discrepancies between internal and external data
- Note patterns, outliers, and trends

### Step 5: Dispatch the Validator
Once both analyst memos are complete, dispatch the research-validator agent:

```
Dispatch research-validator with:
"Validate research findings in research-alpha.md and research-bravo.md. Cross-check for consistency, source quality, and gaps. Write validated findings to research-validated.md"
```

### Step 5.3: Deep Research Option (User-Initiated)

After the validator completes, present the user with:

1. **A concise executive summary** (5-8 bullet points) of what the two analysts found — organized by the Precision Anchor's sub-questions or Coverage Dimensions, not by analyst. Each bullet should state: the sub-question, what was found, and the confidence level.

2. **A Deep Research assessment** identifying sub-dimensions that appear under-explored. The assessment should dynamically generate the sub-dimension checklist based on the engagement's domain, but always check for these general patterns:
   - **Classification sub-tiers**: Are there sub-categories within each top-level classification that have different implications the first pass didn't distinguish? (e.g., in market analysis: SMB vs mid-market vs enterprise segments; in regulatory work: different product sub-types with different rules; in competitive analysis: direct vs indirect vs substitute competitors)
   - **Client-specific relevance**: Did the agents find information that specifically addresses the client's stated context (their product categories, geographies, size, maturity stage), or only general/industry-wide findings?
   - **Adjacent domains**: Beyond the primary domain researched, are there adjacent frameworks, regulations, market forces, or stakeholder dynamics that materially affect the answer? (e.g., for a pricing question: not just competitor pricing but also procurement practices and switching costs; for a market entry question: not just market size but also distribution channels and local partnership requirements)
   - **Granularity of process/mechanism**: Where the first pass identified that a process, approval, or mechanism exists, did it capture the operational specifics — who is involved, what system/channel is used, what the timeline and cost are, and what the requirements for compliance or participation look like?
   - **Outcome data**: For every example, case study, or benchmark cited, is there quantified outcome data (revenue impact, adoption rate, cost, timeline) — or only descriptions of what was done without measuring what it achieved?

3. **An explicit question to the user**: "I've identified [N] sub-dimensions that could benefit from deeper research. Would you like me to dispatch a third research agent to investigate these specifically? This will add depth but also time to the engagement."

**If the user confirms**, dispatch the **analyst-deep** agent with:
- The validated findings from research-alpha.md and research-bravo.md
- The specific sub-dimensions identified above as the research brief
- Instructions: "Investigate these specific sub-dimensions: [list]. Write findings to research-deep.md"

**After the deep agent completes**, re-dispatch the validator to cross-check all THREE research files (research-alpha.md, research-bravo.md, research-deep.md) and produce an updated research-validated.md.

**If the user declines**, proceed normally to Step 5.5 with the existing two-agent research base.

### Step 5.5: Answer Altitude Check (MANDATORY — before compiling the research package)

For each sub-question in the Precision Anchor, assess whether the evidence answers the question at the LEVEL OF SPECIFICITY the client needs — not just the topic.

**The altitude test:** If the client asked "how many screens per store by store size," evidence that answers "how many screens in the total network" is at the WRONG ALTITUDE. It addresses the right topic but at a higher level of aggregation than the client can use.

For each sub-question, classify the evidence as:

- **PRECISE MATCH**: Evidence answers the question at the exact level of specificity requested. Example: "CVS deploys 2 screens in small stores (checkout + entrance), 4 in medium (add pharmacy + endcap), 6 in large (add 2 additional endcaps)."
- **ALTITUDE MISMATCH**: Evidence addresses the right topic but at a different level of aggregation, geography, time period, or unit of analysis. Example: "CVS has 11,000 screens across 9,000 stores" when the question was per-store by size.
- **TOPIC MISS**: Evidence addresses a different topic entirely.

Altitude mismatches are the most dangerous because they LOOK like answers. The data is relevant, the topic is right, and it's tempting to present it as responsive. But the client cannot use network totals to build a per-store archetype.

**Coverage completeness check:** If the Precision Anchor includes a Deliverable Blueprint with Coverage Dimensions, check whether the evidence base has findings for each dimension. For each dimension unit (e.g., each country, each category, each functionality), classify as:
* COVERED: At least one substantive finding with a sourced example
* THIN: A finding exists but lacks specificity (e.g., a general statement about "Southeast Asia" rather than a specific competitor example in that market)
* GAP: No evidence found for this dimension unit

For THIN and GAP classifications, state what specific research would close it. Do not proceed past research without surfacing this to the user — a gap in a coverage dimension is equivalent to a partial answer.

**Note:** If the Deep Research agent (Step 5.3) was deployed, include its findings in the altitude check. Deep Research findings often resolve altitude mismatches identified in the initial two-agent pass.

**When altitude mismatches are found:**
1. Flag them explicitly in the research package as "ALTITUDE MISMATCH — [what we have] vs. [what was asked]"
2. Calculate whatever can be inferred (e.g., "11,000 screens / 9,000 stores = ~1.2 avg, but this average masks the small/medium/large distribution")
3. State what specific data would close the gap (e.g., "CVS store-level deployment data, available via expert interview with CVS digital media team or in-store audit of 10-15 locations")
4. Carry this classification forward to the sense-check and synthesis — an altitude mismatch must be surfaced in the report as a qualification, not buried

### Step 6: Compile the Research Package
After validation, compile the final research output that includes:
- Validated findings (from the validator)
- Client data analysis (if applicable)
- Expert input synthesis (if applicable)
- A unified information gap assessment
- Recommendations for what private information (client data, expert interviews) would strengthen the evidence base

## Handling Information Boundaries

Be explicit about what public research can and cannot answer:

**Public research CAN typically provide:**
- Market sizes, growth rates, and industry benchmarks
- Competitor strategies, financials, and market positions
- Regulatory landscape and policy trends
- Customer segments and behavioral trends (at an aggregate level)
- Technology trends and adoption curves

**Public research CANNOT typically provide:**
- Client-specific financials beyond what is publicly filed
- Internal operational metrics (cost structures, process efficiency)
- Customer-level data (retention, LTV, NPS at granular level)
- Proprietary pricing and margin data of private competitors
- Organizational capabilities and culture

When a finding depends on private information, do not guess. Flag it explicitly and recommend the specific data request or expert interview that would fill the gap.

## Output
Present the compiled research package to the user with a clear signal on evidence strength and remaining gaps. This package feeds directly into the sense-check phase.
