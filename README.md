# Strategy Consultant

A Cowork plugin that performs the analytical work of a strategy consultant. Takes a business problem from definition through research, validation, synthesis, and delivers an executive-grade client report.

## Who It's For

- **Management Consultants** — Strategy and generalist consultants at firms who want to accelerate the research-to-deliverable cycle
- **Corporate Strategy Teams** — In-house strategists running internal engagements for C-suite
- **Corporate Development / M&A** — Teams scoping market entries, acquisitions, and competitive landscapes
- **Independent Advisors / Boutique Firms** — Solo or small-team consultants who need the analytical horsepower of a larger team

## How It Works

This plugin is designed to handle 80–90% of the analytical workload in a strategy engagement — research, evidence validation, structured synthesis, and report drafting — so that the consultant can focus on the 10–20% that creates unique value: client relationship judgment, proprietary insight, and final recommendations. All outputs are intended as high-quality working drafts for expert review, not finished deliverables.

## What It Does

This plugin runs a complete consulting-grade analytical workflow:

1. **Define the problem** — Sharpens a vague business challenge into a decision-oriented question with clear scope
2. **Structure hypotheses** (optional) — Builds a testable hypothesis tree when the problem benefits from structured decomposition
3. **Research** — Deploys two independent research agents in parallel, then validates findings with a third agent for consistency and source quality
4. **Sense-check** — Pressure-tests all findings through triangulation, steel-manning the counter-argument, math checks, and bias scanning
5. **Synthesize** — Builds a storyline that directly answers the client question, organized by the logic of the answer (not a rigid framework)
6. **Deliver** — Produces an executive-grade Word document with clear language, sourced claims, and zero consulting clichés

## Commands

| Command | Purpose |
|---------|---------|
| `/engagement <topic>` | Run the full end-to-end consulting engagement |
| `/research <topic>` | Deploy three research agents to investigate a topic standalone |
| `/define-problem <brief>` | Sharpen a vague question into a decision-oriented problem statement |
| `/interview-guide <topic>` | Plan expert interviews and create structured guides |

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
| **expert-interview** | Plans, guides, and processes expert interviews |

## Agents

| Agent | Role |
|-------|------|
| **analyst-alpha** | Independent research thread A — direct angle (market data, financials, benchmarks) |
| **analyst-bravo** | Independent research thread B — complementary angle (competitive dynamics, case studies, contrarian evidence) |
| **research-validator** | Cross-checks both analysts for consistency, source quality, and gaps |

## Connectors (Optional)

This plugin works without any external integrations. See `CONNECTORS.md` for optional connectors (document storage) that enhance team workflows.

## Design Principles

- **Delivery mode only** — produces outputs directly, no Socratic coaching
- **Evidence-traced** — every claim in the final report traces back to a sourced finding
- **Bias-resistant** — two independent research threads + validation reduces confirmation bias
- **No forced frameworks** — the storyline structure follows the logic of the answer
- **No clichés** — a comprehensive banned-language list ensures clear, direct executive writing
- **Expert-in-the-loop** — designed as a 80–90% accelerator, not a replacement for professional judgment
