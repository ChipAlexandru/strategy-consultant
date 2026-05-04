# Counter-argument sources — three required tributaries

This is the canonical specification of where counter-arguments come from. Referenced by `sense-check` (Step 3), `synthesis` (Step 4), `client-report` (Counter-Argument section), `synthesis-critic` (Check 4), and `deliverable-validator` (Check C). Skills should LINK to this reference rather than re-explaining; they retain their phase-specific actions (write, verify, audit).

## The three tributaries

A counter-argument section that draws from only the analyst's own reasoning will sound clever but will miss what actually matters to the client. Every counter-argument section in this plugin must draw from THREE sources:

1. **Steel-man counter-narrative.** The strongest possible analytical case against the emerging recommendation. Constructed in `sense-check` Step 3 Part A. If you cannot articulate a strong opposing case, the conclusion may be trivially true (and therefore not very useful) — or you have not thought hard enough.

2. **Client-Raised Objections Inventory.** Every concern, hesitation, objection, or risk the client raised — in their call, brief, messages, or any source material. Extracted systematically in `sense-check` Step 3 Part B. Logged as a numbered table with source location, addressed-status, and action needed. **Client-raised concerns that go unaddressed in the deliverable are a credibility risk — the client will notice their own question was not answered.** Do not skip "minor" concerns; address them briefly rather than ignoring them.

3. **Evidence-Implied Risks.** Risks, threats, or caveats the client did NOT raise but that the evidence itself surfaces. Extracted in `sense-check` Step 3 Part C. Examples: phased deployment implies operational complexity; sales-team-needed implies a staffing prerequisite; third-party-adoption-dependent implies an external dependency.

## Format for the counter-argument section in the deliverable

For each counter-argument, structure as:

> "The risk is [X]. We considered this carefully. The evidence suggests [Y], and we recommend [mitigation Z] as a safeguard."

The structure shows the reader that the team:
- Considered the objection seriously
- Has evidence-based reasoning for why it does not derail the recommendation (or that it represents a manageable risk)
- Has a mitigation plan if the risk materializes

## Where this is enforced

| Phase | What it does with the three tributaries |
|-------|------------------------------------------|
| sense-check, Step 3 | Produces all three: steel-man, Client-Raised Objections Inventory table, Evidence-Implied Risks table |
| synthesis, Step 4 | Storyline counter-argument section addresses all three |
| client-report, Counter-Argument Section | Document includes all three with the structured format above |
| synthesis-critic, Check 4 | FAILs the storyline if any client-raised objection or evidence-implied risk is missing |
| deliverable-validator, Check C | FAILs the deliverable if any item from the sense-check tables is silently omitted |

A storyline or report that addresses only the most obvious analytical objection — while ignoring client-raised concerns or operational risks — fails this doctrine.
