---
description: Continuation only — resumes the research phase of an active engagement. To start a new engagement, use /engagement.
argument-hint: "<research question or topic>"
---

## CONTINUATION COMMAND — do not use as a fresh entry point

This command continues an existing engagement. Before any other tool call:

  1. Check for an engagement workspace (`./engagements/<slug>-<date>/engagement-state.json`,
     or — for legacy engagements — `./engagement/precision-anchor.md`).
  2. If a workspace exists → continue from the research phase using its state.
  3. If a workspace does NOT exist → STOP. Invoke /engagement instead. engagement-manager
     will route to the correct starting phase, including this one if appropriate.

Do not attempt to run this phase cold. Upstream artifacts (Precision Anchor,
Client Question Checklist, Source Material Extraction Log, data-source answers,
engagement-state.json) are produced by earlier phases and required inputs here.
Reconstructing them inside this command is not the fix — routing through
engagement-manager is.

# /research — Parallel Research with Validation (continuation)

> If you see unfamiliar placeholders or need to check which tools are connected, see [CONNECTORS.md](../CONNECTORS.md).

**Important**: This plugin assists with strategic analysis and research but does not constitute professional consulting, financial, or legal advice. All outputs should be reviewed by qualified professionals before use in decision-making.

Resume the research phase of an active engagement. Deploys two independent research agents in parallel, then a validator, against the upstream artifacts produced by problem-definition.

## Usage

```
/research <research question or topic>
```

The `<topic>` argument is informational only — the authoritative question comes from the active engagement's Precision Anchor, not from the argument string.

If no engagement workspace exists, do not attempt to start one. Stop and route the user to `/engagement`.

## Workflow

This command resumes the **research** skill inside an active engagement. The skill's preflight gate verifies the upstream artifacts (precision-anchor.md, client-question-checklist.md, source-material-extraction-log.md, step0-answers.md, engagement-state.json) are present and that problem-definition is in `completed_phases`. If any required item is missing, the skill stops and routes back to engagement-manager.

The detailed phase steps live in `skills/research/SKILL.md`. This command file does not duplicate them.

## Output

A validated research package: consolidated findings with CS scores, precision alignment, contradictions, gaps, and Research Notes — written into the active engagement's workspace.
