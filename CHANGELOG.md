# Changelog

## 1.5.1 — 2026-05-03 (cleanup)

Surgical consistency pass over the v1.5.0 release. No architectural changes; no shared references, agents, or phase gates were modified. The patch only fixes user-facing wording and one routing inconsistency that contradicted the v1.5.0 architecture.

- **Research sequencing wording.** `README.md`, `commands/engagement.md`, and `skills/engagement-manager/SKILL.md` previously described research as "three agents in parallel," lumping research-validator with the analysts. The validator runs sequentially after both analyst memos are complete. All three files now say "two analysts in parallel, then research-validator validates their memos."
- **`commands/engagement.md` brought up to v1.5 architecture.** The command file's Workflow section previously listed Phases 1–8 and missed the four phases added in v1.5.0 (Data Source Inquiry, Deliverable Format Confirmation, Storyline Critique, Deliverable Validation). The command file now mirrors the orchestrator's Phases 1, 2, 2.5, 2.7, 3, 3.5, 4, 5, 5.5, 6, 6.5 — concise summaries only; the orchestrator skill remains the source of truth for phase logic. The Output section now reflects user-selectable Word / Excel / PowerPoint formats with required source traceability in all three.
- **Workflow-plugin checklist in `README.md`.** The "Checklist when adding a new skill" item that referenced the legacy `./engagement/` workspace is now updated to the v1.5.0 convention: continuation commands check for `./engagements/<slug>-<date>/engagement-state.json`, with `./engagement/precision-anchor.md` retained as a backward-compatible fallback only. Migration language elsewhere in the file is unchanged.
- **`skills/problem-definition/SKILL.md` Routing Check.** Previously, `commands/define-problem.md` claimed the skill had a preflight gate, but the skill itself did not. A lightweight Routing Check section has been added near the top — explicitly NOT a hard upstream preflight (problem-definition is Phase 1; there is no upstream state to gate on for fresh runs). The check distinguishes (a) fresh `/engagement` Phase 1 invocation (proceed; engagement-manager owns workspace creation) from (b) `/define-problem` continuation (require active workspace). Subcommands must not create workspaces.
- **Subcommand frontmatter parallelism.** `commands/research.md` previously said "Continuation only — runs the research phase…" while `commands/define-problem.md` and `commands/interview-guide.md` said "resumes." All three now use "resumes" for consistency. No behavioral change.

## 1.5.0 — 2026-05-03

This release improves entry-point discipline, adds explicit engagement state and resume logic, hardens the phase gates, splits validation roles by phase, and consolidates duplicated doctrine into shared references. The architecture is preserved; the changes are reliability and maintainability passes.

### Prompt 1 — Command surface
- README: `/engagement` is the only fresh-start command. The Commands table now distinguishes "Fresh start (sole entry point)" from "Continuation only".
- Frontmatter `description:` for `/research`, `/define-problem`, and `/interview-guide` rewritten to read as continuation-only ("Continuation only — runs/resumes …").
- Sub-command workflow sections shortened. Step-by-step content lives in the SKILL.md, not duplicated in the command file.
- `engagement-manager`: collapsed nine repeated "Invoke the skill. Its internal gates are authoritative — do not bypass." preambles into a single rule near the top ("Skill invocation rule").

### Prompt 2 — State, resume logic, namespaced workspaces
- New convention: every engagement gets `./engagements/<slug>-<YYYY-MM-DD>/`.
- New file: `engagement-state.json` (engagement_id, topic, workspace_path, current_phase, completed_phases, artifact_paths, checkpoint_status, next_required_action, deliverable_format, scenario, created_at, last_updated). Schema documented in `skills/engagement-manager/SKILL.md`.
- Resume protocol: scan `./engagements/`, single-or-multiple workspace handling, state reconstruction from artifacts when state file is missing, legacy `./engagement/` migration that preserves the original folder.
- README updated with Workspace and state section pointing to the schema.

### Prompt 3 — Hard preflight gates
Each downstream skill received a "Preflight Gate" section that checks `engagement-state.json` + `completed_phases` + required artifact paths and STOPs (routing back to `engagement-manager`) when any item is missing or empty. Gates added to:
- `research/SKILL.md` — requires problem-definition + precision-anchor.md, client-question-checklist.md, source-material-extraction-log.md, step0-answers.md.
- `expert-interview/SKILL.md` — requires research + research-validated.md, precision-anchor.md.
- `sense-check/SKILL.md` — requires research + research-validated.md, precision-anchor.md, client-question-checklist.md.
- `synthesis/SKILL.md` — requires sense-check + sense-check.md, research-validated.md, precision-anchor.md. Also blocks DRIFTED upstream verdicts.
- `client-report/SKILL.md` — requires synthesis AND storyline-critique + storyline.md, research-validated.md, sense-check.md, precision-anchor.md, client-question-checklist.md.
- `agents/deliverable-validator.md` — requires client-report + final deliverable, storyline.md, research-validated.md, sense-check.md, precision-anchor.md, client-question-checklist.md.

Each gate also defines the state-file update on successful exit.

### Prompt 4 — Dedicated deliverable-validator
- New: `agents/deliverable-validator.md` — final-deliverable QA (counts, traceability, counter-argument coverage, client-question coverage, headline fidelity, altitude qualification, banned language, assumption labeling, expert-anchor / strategic-conflict, format-specific checks). Produces `deliverable-gap-report.md` with binary PASS/FAIL.
- Phase 6.5 in `engagement-manager` now dispatches `deliverable-validator` (not `research-validator`).
- `agents/research-validator.md` description tightened to scope it explicitly to ANALYST MEMOS. Added a "scope boundary" paragraph telling the agent to stop and reroute if dispatched against a final deliverable.
- README Agents table updated.

### Prompt 5 — Independent synthesis critique
- New: `agents/synthesis-critic.md` — Phase 5.5. Eight checks against the storyline (governing-message altitude, evidence backing, [ADJACENT] vs. [DIRECT] handling, client-objection carry-forward, headline-sequence-as-argument, gap qualification, Deliverable Blueprint coverage, value-add precedence). Produces `storyline-critique.md` with binary PASS/FAIL.
- New phase in `engagement-manager`: Phase 5.5 dispatches synthesis-critic. Client-report cannot begin until critique returns PASS OR the user explicitly accepts open risks at Checkpoint 4.
- New checkpoint: CHECKPOINT 5 — Validated Deliverable.
- Quick Reference skill sequence updated: `… → synthesis → storyline-critique → deliver → deliverable-validation`.
- Critic deliberately scoped to synthesis only (not added to every phase) to avoid process inflation.

### Prompt 6 — Audit and consolidate duplication
Audit (sources counted across SKILLs and agents):
- Altitude / precision references: 30+ mentions across 6+ files.
- Three-question Data Source Inquiry: duplicated nearly verbatim in `engagement-manager` Phase 2.5 and `research/SKILL.md` Step 0.
- Counter-argument three-source rule: present in 5 SKILLs + 2 agents.
- Expert-anchor and strategic conflict: present in 5+ files.
- Research Notes / source traceability: present in 5+ SKILLs + 5 agents.
- CS-1 to CS-4 scoring: already concentrated in `skills/research/references/research-source-guide.md`; do not duplicate.

Consolidation:
- New plugin-root `references/` directory with four shared specifications:
  - `references/data-source-inquiry.md`
  - `references/altitude-and-precision.md`
  - `references/counter-argument-sources.md`
  - `references/expert-anchor-and-conflicts.md`
  - `references/research-notes-and-traceability.md`
- `engagement-manager` gains a "Shared references" section listing all references and the existing skill-level references.
- `research/SKILL.md` Data Source Inquiry collapsed from ~40 lines to a pointer; Data Source Priority Hierarchy + Scenarios collapsed from ~40 lines to a pointer. Phase-specific actions retained.
- `engagement-manager` Phase 2.5 collapsed to a pointer + 5-step orchestration list. The three required questions now live only in `references/data-source-inquiry.md`.
- `sense-check`, `synthesis`, `client-report`: added a concise "References" section near the top pointing to the shared specs. Phase-specific gates and quality checks retained verbatim.
- Process not weakened: gates remain hard, sense-check still produces all eight required sections, client-report still runs all 12 quality checks (5a–5l), counter-argument three-source rule still enforced (now via reference + per-phase check).

## Migration notes for users

- v1.4.0 engagements with a `./engagement/` workspace will continue to work. On first `/engagement` invocation under v1.5.0, the orchestrator reconstructs `engagement-state.json` from artifacts and writes it into the legacy folder. New engagements use `./engagements/<slug>-<date>/`.
- No commands renamed. No skills removed.
- Agents added: `deliverable-validator`, `synthesis-critic`. Existing agents retained with tightened scope on `research-validator`.
