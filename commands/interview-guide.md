---
description: Continuation only — resumes the expert-interview phase of an active engagement. To start a new engagement, use /engagement.
argument-hint: "<topic or research context>"
---

## CONTINUATION COMMAND — do not use as a fresh entry point

This command continues an existing engagement. Before any other tool call:

  1. Check for an engagement workspace (`./engagements/<slug>-<date>/engagement-state.json`,
     or — for legacy engagements — `./engagement/precision-anchor.md`).
  2. If a workspace exists → continue from the expert-interview phase using its state.
  3. If a workspace does NOT exist → STOP. Invoke /engagement instead. engagement-manager
     will route to the correct starting phase, including this one if appropriate.

Do not attempt to run this phase cold. Expert-interview planning is meaningful only against
research gaps already identified by the validator — without them, the interview guides
collapse into generic questionnaires.

# /interview-guide — Expert Interview (continuation)

> If you see unfamiliar placeholders or need to check which tools are connected, see [CONNECTORS.md](../CONNECTORS.md).

**Important**: This plugin assists with strategic analysis and research but does not constitute professional consulting, financial, or legal advice. All outputs should be reviewed by qualified professionals before use in decision-making.

Resume the expert-interview phase of an active engagement — either creating interview guides mapped to research gaps, or processing uploaded interview notes back into the research base.

## Usage

```
/interview-guide <topic or context>
```

The argument is informational only — the authoritative scope and gaps come from the active engagement's research-validated.md, not from the argument string.

If no engagement workspace exists, do not attempt to start one. Stop and route the user to `/engagement`.

## Workflow

This command resumes the **expert-interview** skill inside an active engagement. The skill's preflight gate verifies that research has completed and that research-validated.md and precision-anchor.md exist. The detailed steps (gap identification, expert profile definition, guide construction, claim extraction, cross-reference) live in `skills/expert-interview/SKILL.md`. This command file does not duplicate them.

## Output

**Pre-interview**: Expert profiles (prioritized) + structured interview guides with gap mapping, written into the active workspace.

**Post-interview**: Extracted claims with CS scores, cross-reference against public research, updated Source Registry entries, gap closure assessment.
