---
name: sense-check
description: >
  Pressure-test research findings and analytical conclusions for robustness. Use when someone asks to "sense-check this", "pressure-test these findings", "challenge this analysis", "stress-test the argument", "play devil's advocate", "poke holes in this", or when the analytical workflow needs a quality gate between research and synthesis. Also trigger when someone presents a conclusion and wants it challenged before taking it to a client.
---

# Sense-Check — Pressure-Test Everything

Take the research findings and emerging conclusions and systematically try to break them. This is the quality gate between having evidence and having a defensible argument. Most weak consulting work fails here — the analyst found data that supports the hypothesis and stopped looking.

## Process

### Step 1: Inventory the Claims
List every substantive claim that the eventual storyline will rest on. For each claim, note:
- What evidence supports it
- How many independent sources corroborate it
- What confidence level the research assigned

### Step 2: Triangulate
For each major claim, check whether the same conclusion holds when approached from different angles:
- Does the top-down view (market data) align with the bottom-up view (unit economics)?
- Does the quantitative evidence (numbers) align with the qualitative evidence (expert opinions, case studies)?
- Does the historical trend support the forward-looking projection?

If three independent angles point the same way, the claim is on solid ground. If only one does, flag it as fragile.

### Step 3: Steel-Man the Opposite AND Surface Client-Raised Objections
This step has two parts. Both are mandatory.

**Part A: Steel-man the analytical counter-argument.**
For each key conclusion, construct the strongest possible counter-argument:
- What would someone who disagrees point to?
- What data would you need to see to change your mind?
- What assumptions does the conclusion depend on, and how sensitive is it to those assumptions being wrong?

Write the steel-man argument out in full. If you cannot articulate a strong opposing case, the conclusion may be trivially true (and therefore not very useful) — or you have not thought hard enough.

**Part B: Systematically extract client-raised objections.**
Re-read the client call transcript, brief, and all source materials. Extract every concern, hesitation, objection, or risk the client raised — even offhand comments. For each one:
- Note the exact concern and where it appeared
- Assess whether the current evidence base addresses it
- If unaddressed, flag it as a gap that must be covered in the counter-argument section of the synthesis and report

Client-raised concerns that go unaddressed in the deliverable are a credibility risk. The client will notice their own question was not answered. Even if the concern seems minor, it is safer to address it briefly than to ignore it.

### Step 4: Sanity-Check the Math
For every quantitative claim:
- Does the back-of-envelope math check out? (A 15% margin improvement on a $2B revenue base is $300M — does that magnitude make sense in context?)
- Are the units consistent? (Market share percentages vs. absolute revenue vs. volume)
- Are comparisons apples-to-apples? (Same geography, same time period, same definition)
- Is the precision warranted? (Do not say "$4.237B" when the assumptions could swing by $500M — use ranges)

### Step 5: Question-Answer Precision Check
This is the most important check in the sense-check process. Re-read the **Precision Anchor** from the problem-definition phase, then ask:

**Has the analysis drifted?** Compare the emerging conclusion to the exact question in the Precision Anchor. Common drift patterns:
- The question asks "should we enter market X?" but the analysis answers "market X is growing" (describes the market instead of recommending an action)
- The question asks about a specific geography but the data is global
- The question asks about profitability but the analysis focuses on revenue
- The question asks "which option?" but the analysis only evaluates one option favorably
- The question asks for a timeline but the analysis gives a static snapshot

**Is the answer at the right altitude?** This is the most common and most dangerous form of analytical drift. The analysis may address the right topic but at the wrong level of specificity:
- Client asks for per-store breakdown → analysis provides network totals
- Client asks for country-specific data → analysis provides global averages
- Client asks for margin impact → analysis provides revenue impact
- Client asks for by-SKU economics → analysis provides category-level economics

An altitude mismatch is NOT a precise answer. It is a PARTIAL answer at best. When the sense-check identifies an altitude mismatch, the verdict must be PARTIAL and the gap must be explicitly stated: "The evidence answers [what it actually answers] but the client asked for [what they actually asked]. The gap is [specific missing data]. To close it, [specific recommended action]."

Do NOT let altitude mismatches pass as precise answers. A consultant who presents network totals when the client asked for per-store breakdowns has not answered the question — they have provided useful context that happens to be on the same topic.

**If the data doesn't match the question**: This is NOT a reason to answer a different question. Instead, the sense-check must flag: (a) what the available data can answer, (b) the gap between that and what the client asked, and (c) a clear recommendation for how to close the gap (additional research, client data, expert interviews). If the gap cannot be closed, the conclusion must include an explicit qualification.

**Verdict**: [The emerging conclusion PRECISELY answers the Precision Anchor question / The conclusion PARTIALLY answers it — specify the gap / The analysis has DRIFTED — specify to what question]

If the verdict is DRIFTED, recommend looping back to targeted research before proceeding to synthesis. Do not let a drifted analysis pass this gate.

### Step 6: Check for Analytical Traps
Run through this checklist:

**Confirmation bias**: Did the research primarily seek evidence that supports the hypothesis? Is there a systematic gap in disconfirming evidence?

**Survivorship bias**: Are we only looking at successful examples? What about companies/markets/strategies that tried the same thing and failed?

**Cherry-picking**: Are there data points that were found but excluded because they did not fit the narrative?

**False precision**: Are we presenting uncertain estimates as if they were exact?

**Missing "compared to what?"**: Every number needs context. 8% growth sounds good — unless the market grew 12%. $50M in savings sounds large — unless the cost base is $20B.

**Recency bias**: Are we over-weighting recent events and under-weighting structural factors?

**Anchoring**: Are we anchored on the first number we found rather than the best number?

### Step 7: Produce the Sense-Check Report

```
## Overall Assessment
[1-2 sentences: How robust is the evidence base? Can we proceed to synthesis or does more work need to happen?]

## Question-Answer Precision Verdict: [PRECISE / PARTIAL / DRIFTED]
[If PARTIAL: what does the data answer vs. what was asked? What is the gap?]
[If DRIFTED: what question is the analysis actually answering? What would bring it back on track?]

## Claim-by-Claim Assessment
| Claim | Evidence Strength | Triangulated? | Counter-Argument | Verdict |
|-------|------------------|--------------|-----------------|---------|

## Key Vulnerabilities
[The 2-3 weakest points in the argument — where a skeptical partner or client would push back]

## Steel-Man Counter-Narrative
[The best case against the emerging conclusion, written as a coherent argument]

## Client-Raised Objections Inventory
| # | Client Concern | Source (where raised) | Addressed in Evidence? | Action Needed |
|---|---------------|----------------------|----------------------|---------------|
[Every concern, hesitation, or objection the client raised in the call, brief, or messages. For each: note whether the current evidence addresses it, and if not, what action is needed to address it in the synthesis/report.]

## Math Checks
[Results of back-of-envelope sanity checks on key numbers]

## Analytical Traps Identified
[Any biases or logical errors found, with specific examples]

## Recommendation
[Proceed to synthesis / Revisit specific research areas / Downgrade confidence on specific claims / REDIRECT — analysis has drifted, needs targeted research on the actual question]
```

Present the sense-check report to the user. If vulnerabilities are serious or the precision verdict is DRIFTED, recommend specific follow-up research before proceeding to synthesis. A DRIFTED verdict is a hard stop — do not proceed to synthesis until the analysis is redirected to answer the actual question.
