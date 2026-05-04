---
description: Continuation only — resumes problem-definition inside an active engagement. To start a new engagement, use /engagement.
argument-hint: "<business challenge, client brief, or RFP>"
---

## CONTINUATION COMMAND — do not use as a fresh entry point

This command continues an existing engagement. Before any other tool call:

  1. Check for an engagement workspace (`./engagements/<slug>-<date>/engagement-state.json`,
     or — for legacy engagements — `./engagement/precision-anchor.md`).
  2. If a workspace exists → continue from this phase using its state.
  3. If a workspace does NOT exist → STOP. Invoke /engagement instead. engagement-manager
     creates the workspace and routes to the correct starting phase, including this one if
     appropriate.

Do not attempt to run this phase cold. The workspace setup, slug, dating convention, and
state file are owned by engagement-manager — reconstructing them here rebuilds the
orchestrator piecemeal.

# /define-problem — Problem Definition (continuation)

> If you see unfamiliar placeholders or need to check which tools are connected, see [CONNECTORS.md](../CONNECTORS.md).

**Important**: This plugin assists with strategic analysis and research but does not constitute professional consulting, financial, or legal advice. All outputs should be reviewed by qualified professionals before use in decision-making.

Resume problem-definition inside an active engagement — refining the problem statement, Precision Anchor, Client Question Checklist, and Deliverable Blueprint when the engagement-manager has routed back here.

## Usage

```
/define-problem <business challenge or brief>
```

The argument is informational only — the authoritative scope and prior artifacts come from the active engagement workspace, not from the argument string.

If no engagement workspace exists, do not attempt to start one. Stop and route the user to `/engagement`.

## Workflow

This command resumes the **problem-definition** skill inside an active engagement. The skill's preflight gate verifies that engagement-state.json exists. The detailed steps (raw extraction, targeted clarifying questions, problem-statement drafting, Deliverable Blueprint, stress-tests, Client Question Checklist, Precision Anchor) live in `skills/problem-definition/SKILL.md`. This command file does not duplicate them.

## Output

Updated problem-definition artifacts in the active workspace: problem-statement, Deliverable Blueprint, Client Question Checklist, and Precision Anchor.
