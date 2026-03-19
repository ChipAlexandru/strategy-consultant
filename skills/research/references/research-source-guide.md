# Research Source Guide

## Confidence Scoring Scale (CS-1 to CS-4)

Every data point collected during research must be assigned a confidence score. This score determines how the data point can be used in the final deliverable.

### CS-1 — Highest Confidence
**Use directly. Anchor the analysis on these.**

Sources:
- **Company-reported results**: 10-K, 10-Q, annual reports, proxy statements, audited financials (SEC EDGAR, local equivalents)
- **Direct executive quotes**: Earnings call transcripts, investor presentations, on-record interviews
- **Top-tier independent analysts**: Goldman Sachs, Morgan Stanley, JP Morgan, Bernstein equity research; Gartner, Forrester, IDC industry research (often paywalled — note when referencing)
- **Government and regulatory data**: Census, BLS, Eurostat, national statistics offices, trade data (UN Comtrade), FTC, EC competition filings
- **Peer-reviewed academic research**: Published journals, NBER working papers
- **Patent filings and court documents**: USPTO, EPO, litigation records

Usage rule: CS-1 data points can be stated as facts in the report. They form the backbone of the argument.

### CS-2 — High Confidence
**Use with attribution. Solid supporting evidence.**

Sources:
- **Reputable independent research**: McKinsey Global Institute, BCG Henderson Institute, established think tanks
- **Established trade publications**: Industry-specific journals with editorial standards
- **Expert interviews from reputable companies**: When the interviewee has direct domain expertise and the company has a credible position in the market
- **Business press of record**: Financial Times, Wall Street Journal, Bloomberg, Reuters, The Economist
- **Industry associations**: Useful for aggregate data, though may advocate for members — note potential bias
- **Conference presentations**: Good for emerging trends, but often promotional — note context

Usage rule: CS-2 data points can be used as evidence in the report with clear attribution. They strengthen CS-1 findings but should not be the sole basis for critical claims.

### CS-3 — Low Confidence
**Use only to corroborate higher-tier findings. Flag bias risk explicitly.**

Sources:
- **General news articles**: May oversimplify or sensationalize
- **Vendor and consulting firm reports**: Risk of self-serving bias — the vendor may be promoting their own market or solution
- **Company press releases**: Inherently promotional
- **Industry marketing materials**: White papers, sponsored research, branded content

Usage rule: CS-3 data points must NOT be used as standalone evidence. They may only appear in the report when corroborated by at least one CS-1 or CS-2 source. When used, the report must note the source limitation (e.g., "according to vendor estimates" or "per company claims").

### CS-4 — Lowest Confidence
**Do NOT use as evidence. May cite only as market sentiment with explicit caveat.**

Sources:
- **Blog posts and opinion pieces**: Useful for perspective, not for facts
- **Social media**: Anecdotal, unverified
- **Undated or unattributed content**: Treat with extreme skepticism
- **Anonymous or crowd-sourced data**: Glassdoor, Reddit, forums — anecdotal signal only

Usage rule: CS-4 data points must NEVER appear as evidence in the report. They may only be referenced as "market sentiment" or "anecdotal signal" with an explicit caveat that the source is unverified. If the only source for a critical claim is CS-4, flag it as an information gap requiring better sourcing.

---

## How Confidence Scores Drive the Report

| Score | Can anchor a conclusion? | Can support a conclusion? | Needs corroboration? | Needs caveat in report? |
|-------|--------------------------|--------------------------|---------------------|------------------------|
| CS-1  | Yes                      | Yes                      | No                  | No                     |
| CS-2  | No (unless multiple CS-2 converge) | Yes             | Preferred           | Attribution required   |
| CS-3  | Never                    | Only with CS-1/CS-2 backup | Mandatory          | Yes — flag bias risk   |
| CS-4  | Never                    | Never as evidence        | N/A                 | Yes — "unverified"     |

**Escalation rule**: If the strongest available evidence for a critical claim is CS-3, the validator must flag this as a gap and recommend either additional research or an expert interview to upgrade it. Do not proceed to synthesis with critical claims supported only by CS-3 or CS-4 sources.

---

## Data Source Priority and Conflict Resolution

### Priority Ranking

When multiple data source types are available, they are prioritized in this order:

1. **Internal / client data** — Sets the direction and starting point. Highest priority because the client knows their own business best. Internal data includes financial results, operational metrics, customer data, strategic plans, and prior analyses.
2. **Expert interviews from reputable companies** — High weight (CS-2). Source as "Expert Interview — [Name], [Title], [Company]" in all outputs. Valuable for validation, precision, competitive intelligence, and explaining the "why."
3. **High-quality public sources (CS-1)** — Company filings, government data, top-tier analysts. Provide external benchmarks and independent validation.
4. **Other public sources (CS-2 through CS-4)** — Provide context and corroboration, subject to the confidence scoring rules above.

### Conflict Resolution Rules

When data sources disagree, apply these rules in order:

**Internal data vs. public data:**
- Internal data is the default starting point. It reflects the client's actual situation.
- Public data CAN challenge internal data, but ONLY when:
  - The challenging source is CS-1 or strong CS-2 (not CS-3 or CS-4)
  - The context is similar and relevant: same geography, same time period, same industry segment, same metric definition
  - The challenging data is specific enough to be comparable (a global average does NOT challenge a client's market-specific data)
- When public data legitimately challenges internal data, present BOTH with a clear explanation: "Internal data shows X. External data from [source] shows Y. The discrepancy may be due to [possible reasons]. We recommend [how to resolve]."
- Never silently override internal data with public data. The conflict must be visible.

**Expert interview data vs. public data:**
- Expert data from a reputable company (CS-2) with direct experience in the relevant domain generally takes priority over public data for claims within the expert's area of direct knowledge.
- Prioritize the **more precise and more specific** statement. An expert who says "our segment grew 18% last year" is more precise than a public report saying "the market grew 10-15%."
- Prioritize the **more accurate** statement. If the expert's claim can be independently verified and it contradicts a less specific public source, the expert version is preferred.
- When expert data conflicts with CS-1 public sources (e.g., government data, company filings), present both and explain the discrepancy. CS-1 public sources should not be dismissed — the conflict may reveal something important.
- Source expert interview data distinctly in Research Notes: "Expert Interview — [Name], [Title], [Company], [Date]"

**Strategic conflicts (expert recommendation vs. public metrics):**
When an expert provides strategic guidance — a recommendation on prioritization, sequencing,
approach selection, or resource allocation — and public research provides a metric that
implies a different ranking or priority, this is a STRATEGIC CONFLICT, not a data conflict.
Strategic conflicts cannot be resolved by comparing precision, because the expert's
recommendation and the public metric operate on different dimensions.

Resolution rule: The expert's strategic recommendation is the PRIMARY framing in the
deliverable. The conflicting public metric is presented in parentheses as supplementary
context, flagged for the consultant to evaluate and decide whether to retain or remove.

Format: "[Expert's recommendation with attribution]. (Note: [public source] suggests
[alternative implication based on metric] — consultant to evaluate whether [expert's
rationale] or [metric-based rationale] should govern this decision.)"

Examples of strategic conflicts across domains:

- Market entry: Expert says "enter via acquisition — organic entry takes too long in this
  regulatory environment." Public data shows organic entrants have higher 5-year margins.
  → Lead with expert's recommendation; note the margin data in parentheses for consultant
  review.

- Pricing: Expert says "price at parity with incumbent — customers in this segment won't
  pay a premium for unproven technology." Public research shows comparable SaaS products
  command 20-30% premiums in adjacent segments.
  → Lead with expert's pricing guidance; note the premium data in parentheses.

- Operations: Expert says "prioritize supplier diversification over cost optimization."
  Public benchmarks show single-supplier models deliver 15% lower unit costs.
  → Lead with expert's recommendation; note the cost data in parentheses.

Why: Experts provide strategic recommendations based on operational experience that
encompasses factors beyond any single metric. A single metric (margin, CPM, cost, conversion
rate) does not capture the full decision context — regulatory complexity, execution risk,
organizational readiness, competitive dynamics — all of which the expert weighs implicitly.
Public metrics are one input to the decision; the expert's integrated judgment is a
higher-priority input.

**Expert interview data vs. internal data:**
- Both are high-priority sources. When they conflict, assess which is more recent, more specific to the question, and more verifiable.
- If the expert has direct experience in the exact area the internal data covers, the conflict may reveal a blind spot in the client's understanding — flag this as a key insight.
- Present both perspectives with context. Do not silently choose one over the other.

**Within public data (analyst vs. analyst, or source vs. source):**
- Apply the CS scoring hierarchy: CS-1 beats CS-2, CS-2 beats CS-3, etc.
- At the same CS level, prefer: more recent > older, more specific > more general, primary > secondary, independently corroborated > single source.
- When two CS-1 sources disagree, note the contradiction explicitly and investigate whether the disagreement is due to different definitions, time periods, or methodologies.

### Attribution Rules by Source Type

In all outputs (Consolidated Findings, Research Notes, client report), data must be attributed with its source type clearly identified:

| Source Type | Attribution Format in Research Notes |
|---|---|
| Internal / client data | "Client data — [document/dataset name], [date]" |
| Expert interview | "Expert Interview — [Name], [Title], [Company], [Date]" |
| Public — company filing | "[Company], [Filing type], [Date], [URL]" |
| Public — analyst report | "[Firm], [Report title], [Date], [URL]" |
| Public — government data | "[Agency], [Dataset], [Date], [URL]" |
| Public — press | "[Publication], [Date], [URL]" |

---

## Search Strategy by Question Type

### Market Sizing
1. Search: "[industry] market size [year] [geography]"
2. Search: "[industry] TAM SAM SOM"
3. Look for: analyst reports, industry association data, government statistics
4. Cross-reference: top-down (total market) vs. bottom-up (unit economics × volume)
5. Sanity check: does the market size imply reasonable per-capita or per-business spend?

### Competitive Landscape
1. Search: "[company] competitors market share [industry]"
2. Search: "[company] vs [competitor] [metric]"
3. Look for: investor presentations with competitive positioning slides
4. Check: annual reports for "competitive landscape" or "risk factors" sections
5. Map: revenue, market share, strategic focus, recent moves for top 5-10 players

### Growth Rates and Trends
1. Search: "[industry] growth rate CAGR [start year]-[end year]"
2. Search: "[industry] forecast outlook [year]"
3. Look for: multiple sources with different methodologies (demand-side vs. supply-side)
4. Check: whether "growth" means volume, revenue, or profit — these often diverge
5. Validate: does the projected growth rate make sense given historical patterns?

### Client-Specific Intelligence (Public Companies)
1. SEC filings: 10-K (annual), 10-Q (quarterly), DEF 14A (proxy), 8-K (events)
2. Earnings transcripts: management commentary on strategy, outlook, challenges
3. Investor presentations: often the clearest view of management's strategic priorities
4. Glassdoor/employee reviews: organizational culture and capability signals
5. Patent filings: R&D direction and innovation pipeline

### Regulatory and Policy
1. Search: "[industry] regulation [geography] [year]"
2. Check: relevant regulatory body websites directly
3. Look for: pending legislation, recent enforcement actions, public consultations
4. Note: regulatory changes often take 12-24 months to implement — track timelines
