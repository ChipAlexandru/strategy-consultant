---
name: research
description: >
  Conduct thorough, multi-tier research on a client question by dispatching two independent research agents and a validation agent. Use when someone asks to "research this topic", "find evidence for", "investigate this market", "gather data on", "what does the evidence say about", or when the analytical workflow reaches the research phase after problem definition. Also trigger when someone uploads client data or expert interview notes that need to be analyzed alongside public research.
---

# Research — Parallel Investigation with Validation

Conduct rigorous research by deploying two independent research agents working in parallel, followed by a validation agent that cross-checks their findings. This three-agent architecture reduces confirmation bias and produces a more trustworthy evidence base than a single research pass.

## Data Source Priority Hierarchy

Data sources are ranked by priority. When multiple sources are available, the higher-priority source sets the direction. Lower-priority sources provide benchmarks, context, and validation. Not every engagement will have all three — the hierarchy adapts to what is available.

**Priority 1 — Internal / client data (when available)**
Internal data is the highest priority source. It sets the direction and starting point for the analysis. When internal data is available, public research serves to benchmark, contextualize, and challenge it — not the other way around.

Internal data includes: client-provided spreadsheets, internal reports, financial data, operational metrics, customer data, prior analyses, strategic plans, and board materials.

Internal data CAN and SHOULD be challenged — but only by high-quality external sources (CS-1 or strong CS-2), and only when the external data is from a similar and relevant context (same geography, time period, industry segment, and definition). A global average does not challenge a client's specific market data. A competitor's reported results in the same market segment do.

**Priority 2 — Expert interviews from reputable companies (when available)**
Expert interviews carry high weight (CS-2) because they come from practitioners with direct domain experience. Expert interview data should be sourced distinctly as "Expert Interview — [Name], [Title], [Company]" in all research outputs and Research Notes.

Expert interviews are especially valuable for: validating or challenging internal data, adding precision to public estimates, providing competitive intelligence not available publicly, and explaining the "why" behind the numbers.

When expert data conflicts with public data, prioritize the more precise and more specific statement. An expert with direct experience in the relevant segment typically provides more precise data than a public report covering a broader scope.

**Priority 3 — Public research (always, via agents)**
Public research provides the external evidence base: industry reports, company filings, earnings transcripts, investor presentations, trade press, regulatory filings, government data, competitor intelligence, and academic research.

When internal data and expert interviews are absent, public research is the sole evidence base. When they are present, public research provides benchmarks, external validation, and the broader context that internal data and expert views sit within.

## How the Hierarchy Adapts to the Engagement

Not every engagement has all three data sources. The Data Source Inquiry (Step 0) determines which scenario applies:

**Scenario A — Public data only** (most common for external benchmarking)
Public research is both the foundation and the evidence base. The CS-1 to CS-4 scoring framework determines source quality within public data. The validator should be especially rigorous about flagging what public data cannot answer.

**Scenario B — Internal data only** (e.g., processing and analyzing client data)
Internal data is the sole source. Analyze it thoroughly — look for patterns, outliers, trends. Flag where external benchmarks would add context, but deliver the analysis based on what is available.

**Scenario C — Internal data + public research**
Internal data sets the starting point and direction. Public research provides external benchmarks and context. Discrepancies between internal and external data are often where the real insight lives. Apply the conflict resolution rules (see research-source-guide.md) when they disagree.

**Scenario D — Public research + expert interviews**
Public research provides the evidence base. Expert interviews confirm, enhance, and challenge the public findings. The expert-interview skill handles the integration after research completes.

**Scenario E — All three sources**
Full three-tier analysis. Internal data sets the direction. Public research provides benchmarks and context. Expert interviews fill remaining gaps and add precision. This is the most robust scenario.

## Process

### Step 0: Data Source Inquiry (MANDATORY — three required questions, before any research begins)
Before writing the research brief or dispatching analysts, use the **AskUserQuestion** tool to understand what data will be available for this engagement. This step shapes the entire research strategy — different data availability leads to fundamentally different research approaches.

**The following three questions are REQUIRED and must each appear as a separate, clearly worded question in the AskUserQuestion call. You may add additional context-specific questions, but these three must not be omitted, merged, or rephrased beyond recognition:**

**Question 1: Available internal/client data (REQUIRED)**
Based on the problem statement and Precision Anchor, identify 2-3 specific types of internal data that would be most valuable for THIS question and ask whether they are available. Tailor the examples — do not use generic placeholders.

For example, if the question is about market entry:
- "Do you have internal sales data broken down by geography or channel?"
- "Do you have customer acquisition cost benchmarks or unit economics from existing markets?"
- "Do you have any prior market analyses, competitive intelligence, or strategic planning documents on this topic?"

For example, if the question is about cost optimization:
- "Do you have a detailed cost breakdown by category and business unit?"
- "Do you have operational efficiency metrics (cycle times, utilization rates, defect rates)?"
- "Do you have benchmarking data from prior consulting engagements or internal audits?"

**Question 2: External expert interviews (REQUIRED — must be a SEPARATE question)**
Ask explicitly: "Do you have access to external expert interviews — either existing transcripts/notes from industry practitioners, or planned interviews we should prepare guides for?" This question must be asked separately from the internal data question because expert data follows a different processing path (the expert-interview skill). Do NOT merge this with Question 1.

**Why this question matters:** If the user has expert transcripts, the expert-interview skill activates to extract claims, assign CS scores, and cross-reference against public findings. If this question is never asked, an entire evidence tier is silently excluded. This determines whether the engagement runs as Scenario A, C, D, or E.

**Question 3: Other external reference material (REQUIRED)**
Ask: "Do you have any other reference material that should inform this research — for example, an industry report, market study, competitor analysis, or third-party dataset?"

This captures data sources that are neither internal client data nor expert interviews but still provide valuable context beyond what public web research can find. These materials are fed into the research brief as supplementary context for the analysts.

**Determining the research tier mix:** Based on the combined answers to all three questions, determine the research scenario:
- **Public only** (no to all three): Analysts focus entirely on Tier 1 (public research). The validator should be especially rigorous about flagging what public data cannot answer.
- **Public + internal data**: Internal data will be analyzed alongside public research. Research brief should instruct analysts to identify specific areas where internal data could fill gaps.
- **Public + expert interviews**: Research brief should identify the key uncertainties where expert input would be most valuable.
- **All sources**: Full multi-tier research. Internal data sets the direction, public research provides benchmarks and context, expert interviews fill remaining gaps, and reference materials provide additional framing.

**Record the answers** and carry them into the research brief. If the user provides data files or reference materials, note their contents. If they indicate data will come later, note what to expect and when.

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
