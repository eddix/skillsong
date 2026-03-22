---
name: google-5-agent-skill-design-pattern
description: "Design, review, or refactor agent skills and SKILL.md content using Google's five recurring skill design patterns: tool wrapper, generator, reviewer, inversion, and pipeline. Use when Codex needs to choose a skill structure, map a workflow to one or more patterns, draft a new skill folder, critique an existing skill's logic, or decide what belongs in SKILL.md, references/, assets/, and scripts/."
---

# Google 5 Agent Skill Design Pattern

## Goal

Turn a raw workflow into a reusable skill design. Focus on content behavior, trigger quality, progressive disclosure, and guardrails. Prefer the smallest pattern that reliably enforces the intended behavior.

## Working Method

1. Load `references/selection-and-composition.md` first.
2. Diagnose the workflow before drafting anything:
   - Identify the main source of value: domain knowledge, output structure, evaluation, discovery, or orchestration.
   - Identify the main failure mode: hallucinated requirements, skipped steps, inconsistent outputs, shallow reviews, or missing conventions.
   - Identify whether the target skill needs strong gates, user approvals, or multi-turn questioning.
3. Choose one primary pattern. Add secondary patterns only when they solve distinct failure modes.
4. Load only the relevant sections from `references/pattern-playbook.md` for the chosen pattern(s).
5. Plan the resource split:
   - Keep `SKILL.md` for triggers, workflow, gates, and references to bundled resources.
   - Put long conventions, rubrics, and examples in `references/`.
   - Put templates, starter projects, and output skeletons in `assets/`.
   - Add `scripts/` only for deterministic, repetitive, or error-prone operations.
6. Draft or revise the skill using imperative instructions and explicit gates where needed.

## Pattern Selection Rules

- Choose **Tool Wrapper** when the skill must inject library rules, internal conventions, or domain truth on demand.
- Choose **Generator** when the output must be stable, templated, and assembled from known variables.
- Choose **Reviewer** when the job is to score, audit, or report findings against a rubric or checklist.
- Choose **Inversion** when acting too early is risky and the skill must interview the user before producing a result.
- Choose **Pipeline** when the workflow has non-skippable stages, approvals, or checkpoints.

## Composition Rules

- Use **Inversion -> Generator** when the skill must gather missing variables before filling a template.
- Use **Tool Wrapper** inside any pattern when specialized rules must be loaded only for that task.
- Use **Reviewer** at the end of a **Pipeline** when the output needs a final quality gate.
- Keep composition minimal. If one pattern is sufficient, do not add more.

## Output Requirements

When asked to design or refactor a skill, produce:

1. The chosen pattern or pattern combination with a short rationale.
2. The proposed folder structure.
3. A precise frontmatter `description` that includes trigger conditions.
4. A `SKILL.md` outline or full draft with explicit workflow instructions.
5. The recommended contents for `references/`, `assets/`, and `scripts/`.
6. Any mandatory gates, approvals, or clarifying questions the target skill should enforce.

## Guardrails

- Do not mistake formatting for design. The hard problem is behavior design.
- Do not inline large domain documents in `SKILL.md`; move them to `references/`.
- Do not use **Pipeline** when a simple **Generator** or **Reviewer** would be enough.
- Do not use **Inversion** if one or two missing fields can be requested inline without phase-based interviewing.
- For **Reviewer**, keep the checklist separate from the review protocol.
- For **Generator**, keep the template and style guide outside `SKILL.md`.
- For **Pipeline** and **Inversion**, write blocking language explicitly: `Do not proceed until...`, `Wait for user confirmation`, `Do not synthesize the final output before...`.
