# Analytical Traps Reference

A checklist of cognitive biases and logical errors that commonly undermine consulting analysis. Use this as a systematic scan during the sense-check phase.

## Cognitive Biases

### Confirmation Bias
**What it is**: Seeking, interpreting, and remembering evidence that confirms pre-existing beliefs while ignoring contradictory evidence.
**How it shows up**: The research phase found 8 data points supporting the hypothesis and 2 contradicting it — but the 2 contradictions were dismissed as "outliers" without investigation.
**How to check**: Ask "did we search as hard for disconfirming evidence as confirming evidence?" Review the search queries used — were any designed to find counter-evidence?

### Anchoring
**What it is**: Over-relying on the first piece of information encountered.
**How it shows up**: The first market size estimate found was $5B, and all subsequent analysis treats this as the baseline — even though later sources suggest $3-7B range.
**How to check**: Note the first number found for each key metric. Then check whether later, potentially better estimates were given equal weight.

### Survivorship Bias
**What it is**: Drawing conclusions from successes while ignoring failures.
**How it shows up**: "Companies that adopted strategy X grew 20%" — but this ignores the companies that adopted strategy X and failed or exited the market.
**How to check**: For every success story cited, ask "what happened to the ones that tried and failed?"

### Availability Bias
**What it is**: Overweighting information that is easily recalled or recently encountered.
**How it shows up**: A dramatic recent event (a competitor's bankruptcy, a viral product launch) dominates the analysis even though structural factors matter more.
**How to check**: Separate recent events from structural trends. Ask "would this conclusion change if the recent event hadn't happened?"

### Sunk Cost Fallacy
**What it is**: Continuing a course of action because of past investment rather than future value.
**How it shows up**: Recommending the client continue investing in a failing initiative because they have already spent $100M on it.
**How to check**: Reframe: "If we were starting fresh today with no prior investment, would we choose this path?"

## Logical Errors

### False Dichotomy
**What it is**: Presenting only two options when more exist.
**How it shows up**: "The client must either expand internationally OR invest in domestic market share." Reality: they could do both, or neither, or pursue an entirely different strategy.
**How to check**: Challenge every "either/or" framing. Are there options not being considered?

### Correlation vs. Causation
**What it is**: Assuming that because two things move together, one causes the other.
**How it shows up**: "Markets with higher digital penetration have higher margins, so digital investment drives margin improvement." (Maybe both are caused by a third factor like market maturity.)
**How to check**: Ask "is there a plausible mechanism?" and "could a third factor explain both?"

### Composition Fallacy
**What it is**: Assuming what is true of the parts is true of the whole.
**How it shows up**: "Each of these three initiatives generates positive ROI individually, so doing all three together will generate even more ROI." (Ignores resource constraints, cannibalization, and organizational capacity.)
**How to check**: Test whether the combined scenario works, not just the individual pieces.

### Base Rate Neglect
**What it is**: Ignoring the overall probability when evaluating a specific case.
**How it shows up**: "This startup has an amazing product, so it will succeed." (Ignoring that 90% of startups fail regardless of product quality.)
**How to check**: Always start with the base rate for the category, then adjust based on specific factors.

## Data Quality Traps

### Cherry-Picking
Selecting data points that support the narrative while ignoring those that do not. Check: plot all data points, not just the favorable ones.

### False Precision
Presenting "$4.237B" when the underlying assumptions have a ±20% margin of error. Check: does the precision of the output match the precision of the inputs?

### Apples-to-Oranges Comparisons
Comparing metrics across different geographies, time periods, or definitions without adjustment. Check: are the comparison terms defined the same way in every source?

### Denominator Games
Making a percentage look large or small by choosing the denominator. "10% of revenue" vs. "0.5% of total assets" can describe the same dollar amount. Check: is the denominator the right one for this decision?

### Extrapolation Beyond Range
Projecting historical trends far beyond the period they were observed. A 20% CAGR over 3 years does not mean 20% CAGR over 10 years. Check: what would the extrapolated number imply at the endpoint, and does that make physical/economic sense?
