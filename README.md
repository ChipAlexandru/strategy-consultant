# Strategy Consultant

A Cowork plugin that performs the analytical work of a strategy consultant. Takes a business problem from definition through research, validation, synthesis, and delivers an executive-grade client report.

## What It Does

This plugin runs a complete consulting-grade analytical workflow:

1. **Define the problem** — Sharpens a vague business challenge into a decision-oriented question with clear scope
2. **Structure hypotheses** (optional) — Builds a testable hypothesis tree when the problem benefits from structured decomposition
3. **Research** — Deploys two independent research agents in parallel, then validates findings with a third agent for consistency and source quality
4. **Sense-check** — Pressure-tests all findings through triangulation, steel-manning the counter-argument, math checks, and bias scanning
5. **Synthesize** — Builds a storyline that directly answers the client question, organized by the logic of the answer (not a rigid framework)
6. **Deliver** — Produces an executive-grade Word document with clear language, sourced claims, and zero consulting clichés

## Skills

| Skill | Purpose |
|-------|---------|
| **engagement-manager** | Orchestrator — runs the full end-to-end workflow |
| **problem-definition** | Scopes and sharpens the client question |
| **hypothesis-tree** | Builds MECE hypothesis trees (optional, when it adds value) |
| **research** | Dispatches 3 agents for parallel research and validation |
| **sense-check** | Pressure-tests findings for robustness |
| **synthesis** | Builds the client-facing storyline and argument |
| **client-report** | Produces the final .docx deliverable |

## Agents

| Agent | Role |
|-------|------|
| **analyst-alpha** | Independent research thread A — direct angle (market data, financials, benchmarks) |
| **analyst-bravo** | Independent research thread B — complementary angle (competitive dynamics, case studies, contrarian evidence) |
| **research-validator** | Cross-checks both analysts for consistency, source quality, and gaps |

## Usage

**Full engagement**: Ask Claude to "run a full analysis on [business question]" or "do a consulting engagement on [topic]" — the engagement-manager orchestrator will guide you through all phases.

**Individual skills**: Use any skill independently:
- "Help me define this problem" → problem-definition
- "Research the European EV market" → research
- "Sense-check these findings" → sense-check
- "Build the storyline from this analysis" → synthesis
- "Package this into a client report" → client-report

## Connectors (Optional)

This plugin works without any external integrations. See `CONNECTORS.md` for optional connectors (document storage, data platforms, project trackers, chat) that enhance team workflows.

## Design Principles

- **Delivery mode only** — produces outputs directly, no Socratic coaching
- **Evidence-traced** — every claim in the final report traces back to a sourced finding
- **Bias-resistant** — two independent research threads + validation reduces confirmation bias
- **No forced frameworks** — the storyline structure follows the logic of the answer
- **No clichés** — a comprehensive banned-language list ensures clear, direct executive writing
