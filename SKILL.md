---
name: model-handoff
description: Create a concise engineering state checkpoint before switching models or handing a coding task to a new agent. Use when the user asks to prepare a handoff, checkpoint the current work, preserve session state, switch models, or make the current coding task resumable by another model.
---

Create a compact but complete engineering handoff for another model or agent.

The goal is not to summarize the conversation. The goal is to preserve enough
verified project state, decisions, and negative knowledge that a fresh model can
continue the work without repeating investigation or making avoidable mistakes.

## Before writing the handoff

Inspect the actual working state whenever possible.

At minimum, when applicable:

- Inspect `git status`.
- Inspect relevant staged and unstaged diffs.
- Identify the current branch and repository root.
- Review files that are central to the current work.
- Review recent build, test, lint, or diagnostic results that are still available.
- Run inexpensive commands needed to distinguish remembered state from actual
  repository state.
- Do not make unrelated code changes merely to prepare the handoff.

Prefer repository state and tool output over recollection from the conversation.
If remembered information conflicts with observed state, record the observed
state and explicitly note the discrepancy.

## Write the handoff

Unless the user specifies another location, write or update:

`HANDOFF.md`

Do not overwrite useful prior handoff information silently. If `HANDOFF.md`
already exists, read it first and update it to reflect the current state,
removing stale information where appropriate.

Use approximately this structure, omitting sections that genuinely do not apply:

# Engineering Handoff

## Objective

State the current goal and the concrete definition of success.

## Current State

Record the important repository and execution state, including as relevant:

- current branch
- working-tree status
- important modified or newly created files
- current implementation status
- build/test status
- environment or tooling assumptions that matter

Do not dump a complete diff or file listing. Include only state useful to the
successor.

## What Has Been Done

Summarize completed work and meaningful implementation decisions.

Distinguish clearly between:

- implemented and verified
- implemented but not yet verified
- investigated only

## Important Decisions and Constraints

Record architectural decisions, invariants, compatibility requirements,
performance constraints, user requirements, and other choices the successor
should preserve.

For important decisions, briefly record why they were made when the reason is
not obvious from the code.

## Verified Facts

Record facts established by inspection, experiments, builds, tests, logs, or
other evidence.

Prefer concrete evidence such as:

- command and result
- failing test name
- measured behavior
- relevant file/function/module

Do not promote speculation to fact.

## Failed or Rejected Approaches

Preserve negative knowledge aggressively.

For each significant abandoned approach, record:

- what was tried or considered
- what happened
- why it was rejected
- whether it might become viable under different assumptions

This section is especially important. A successor should not waste time
rediscovering known dead ends.

## Current Problems / Open Questions

List unresolved issues.

For each, distinguish among:

- known bug with unknown fix
- hypothesis needing verification
- design choice still open
- external dependency or missing information

Include current leading hypotheses when useful, but label them as hypotheses.

## Reproduction / Verification

Give the smallest useful set of commands for continuing the work, such as:

- build command
- relevant tests
- lint/typecheck command
- reproduction command
- useful diagnostic command

Prefer commands that were actually used and verified.

## Recommended Next Steps

Give the successor a short ordered list of concrete next actions.

The first item should normally be the best immediate action, not a vague goal.

## Relevant Files

List only the files or directories the successor is likely to need first, with
a short explanation of why each matters.

## Handoff Rules

Keep the document concise enough that a new model can read it before acting.

Prioritize, in order:

1. Actual current project state.
2. Constraints and decisions that must be preserved.
3. Negative knowledge and failed approaches.
4. Reproduction and verification information.
5. Current hypotheses and next steps.
6. Historical narrative only when needed to explain one of the above.

Do not include conversational filler, chronology for its own sake, or exhaustive
descriptions of routine edits.

Do not claim something is tested, fixed, or working unless there is evidence.

When uncertainty remains, state it explicitly.

After writing the handoff, report:

- where the handoff was written
- whether the working tree was modified solely by the handoff file
- any important state you could not verify