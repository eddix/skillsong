# Selection and Composition Guide

## Table of Contents

- Core thesis
- Diagnosis questions
- Primary selector
- Composition order
- Resource placement
- Failure signals

## Core Thesis

This pattern set treats skill design as a content-architecture problem, not a formatting problem. The folder layout is mostly standardized already. The real design work is deciding how the skill should control behavior:

- inject knowledge,
- enforce output structure,
- apply a rubric,
- gather requirements before acting, or
- force a multi-stage workflow.

Start with the control problem. Then choose the smallest pattern that solves it.

## Diagnosis Questions

Answer these before drafting a skill:

1. What is the skill really doing: teaching, generating, reviewing, interviewing, or orchestrating?
2. What is the biggest failure risk: wrong conventions, inconsistent output, shallow critique, premature action, or skipped steps?
3. Can the agent safely act on the first request, or must it gather more context first?
4. Does the output need a fixed template or only general guidance?
5. Does the workflow require explicit approvals between stages?
6. Which details are core instructions, and which belong in bundled resources?

## Primary Selector

| Primary need | Choose | Typical resources | Instruction style |
| --- | --- | --- | --- |
| Load domain rules only when relevant | Tool Wrapper | `references/conventions.md` | "Load rules, then write/review against them." |
| Fill a repeatable structure | Generator | `assets/template.*`, `references/style-guide.md` | "Load template, gather variables, fill every section." |
| Audit against explicit criteria | Reviewer | `references/checklist.md` | "Apply each rule, classify findings, explain fixes." |
| Interview before acting | Inversion | Optional `assets/template.*` for final output | "Ask one question at a time; do not proceed before answers." |
| Enforce a strict sequence | Pipeline | Step-specific references and assets | "Execute each step in order; stop on failure or missing approval." |

## Composition Order

Use composition deliberately. Good combinations solve distinct problems:

- `Inversion -> Generator`
  Gather missing requirements first, then fill a stable template.
- `Tool Wrapper -> Reviewer`
  Review code or content against domain-specific conventions instead of generic taste.
- `Pipeline -> Reviewer`
  Add a final quality gate after assembly.
- `Pipeline + Tool Wrapper`
  Load different references only at the step where they matter.

Avoid these weak combinations:

- `Pipeline` for a two-step task with no real checkpoint.
- `Inversion` when a single clarifying question is enough.
- `Generator` without a template or output contract.
- `Reviewer` when the task is actually to rewrite or generate.

## Resource Placement

Keep progressive disclosure clean:

- Put trigger conditions, workflow steps, and gate language in `SKILL.md`.
- Put detailed conventions, rubrics, examples, and decision tables in `references/`.
- Put templates, starter files, or boilerplate in `assets/`.
- Put deterministic utilities in `scripts/`.

Use this rule of thumb:

- If the agent must always remember it, keep it in `SKILL.md`.
- If the agent should load it only for certain paths, move it to `references/`.
- If the content becomes part of the generated output, it probably belongs in `assets/`.
- If the task keeps re-implementing the same code, create a script.

## Failure Signals

Use these signals to refactor an existing skill:

- The skill keeps missing library conventions.
  Add a Tool Wrapper with a dedicated conventions reference.
- The output shape changes from run to run.
  Add a Generator with an explicit template.
- Reviews feel subjective or incomplete.
  Add a Reviewer with a checklist and severity buckets.
- The agent invents requirements before understanding the task.
  Add Inversion and phase-based questioning.
- The agent skips validation or jumps to the end.
  Add a Pipeline with hard checkpoints.
