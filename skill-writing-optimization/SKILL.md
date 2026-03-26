---
name: skill-writing-optimization
description: "Optimize code agent skills by applying proven authoring best practices: progressive disclosure, concise instructions, proper resource placement, workflow design, and multi-model compatibility. Use when writing a new SKILL.md, refactoring an existing skill, reviewing skill quality, or deciding how to split content across SKILL.md, references/, assets/, and scripts/."
---

# Skill Writing Optimization

## Goal

Produce skills that are concise, well-structured, verifiable, and effective across Haiku, Sonnet, and Opus. Focus on behavior design over formatting.

## Working Method

1. Load `references/authoring-checklist.md` first.
2. Diagnose the skill before writing or refactoring:
   - **Freedom level**: Is the task open-ended (high), template-based (medium), or strict-process (low)?
   - **Failure mode**: What goes wrong without the skill — hallucinated steps, inconsistent output, skipped validation, or wrong conventions?
   - **Model sensitivity**: Does the instruction rely on implicit reasoning that Haiku might miss, or over-explain things Opus already knows?
3. Apply the progressive disclosure principle:
   - `SKILL.md` contains only triggers, workflow steps, gates, and load instructions for bundled resources.
   - `references/` holds conventions, checklists, rubrics, examples, and decision tables.
   - `assets/` holds templates, starter files, and output skeletons.
   - `scripts/` holds deterministic utilities that are more reliable than generated code.
4. Draft or revise the skill following the rules below.
5. Validate against `references/authoring-checklist.md` before finalizing.

## Core Rules

### 1. Conciseness

- The context window is a shared resource. Every token costs.
- Only include information the model does not already know.
- Remove filler, preamble, and redundant explanations.
- If a rule can be said in one sentence, do not use three.

### 2. Frontmatter

- `name`: lowercase letters, numbers, hyphens only.
- `description`: third-person, includes what the skill does AND when to trigger it. One to two sentences.
- Bad: `"A skill for code reviews."`
- Good: `"Review pull requests against team conventions and OWASP top-10 rules. Use when a PR is opened or when asked to review code."`

### 3. Freedom Calibration

| Freedom | Use when | Instruction style |
| --- | --- | --- |
| High | Open-ended tasks (code review, research) | Provide guidelines and rubrics, let the agent decide how to apply them. |
| Medium | Template or scaffold tasks | Provide a template with required sections; allow flexible content within sections. |
| Low | Strict processes (migrations, deployments) | Number every step; add explicit gates; use blocking language. |

### 4. Workflow Design

- Use numbered checklists for multi-step workflows.
- Build feedback loops: execute -> verify -> fix -> repeat.
- Add explicit gates with blocking language where needed:
  - `Do not proceed until...`
  - `Wait for user confirmation before...`
  - `Do not generate output before all inputs are gathered.`

### 5. Resource Placement

Apply this decision rule:

- **Always needed** -> `SKILL.md`
- **Loaded on certain paths** -> `references/`
- **Becomes part of output** -> `assets/`
- **Deterministic and error-prone** -> `scripts/`

### 6. Multi-Model Compatibility

- **Haiku**: Needs explicit step-by-step instructions. Avoid implicit reasoning chains. Provide concrete examples.
- **Sonnet**: Balanced. Works well with medium-detail instructions.
- **Opus**: Avoid over-explanation. Trust the model's reasoning. Focus on constraints and edge cases.

Write instructions that work for Sonnet, then add clarifying examples that help Haiku without annoying Opus.

### 7. Content Hygiene

- Avoid time-sensitive information (version numbers, dates). Use `references/` with "old mode" blocks if needed.
- Use consistent terminology throughout. Define domain terms once.
- Do not provide too many choices — decision fatigue hurts output quality.
- Use POSIX paths only. Never use Windows-style backslash paths.

## Anti-Patterns

Do not:

- Paste full convention documents into `SKILL.md`. Move them to `references/`.
- Write vague descriptions like `"A helpful skill."` — always include trigger conditions.
- Add magic numbers without explaining their meaning.
- Blame the user or environment for errors — handle exceptions explicitly.
- Over-engineer with pipelines when a simple checklist suffices.
- Skip verification steps — every skill should have a way to validate its output.

## Output Requirements

When asked to write or refactor a skill, produce:

1. The proposed folder structure.
2. A precise frontmatter with `name` and `description` (including trigger conditions).
3. A `SKILL.md` draft with workflow instructions calibrated to the appropriate freedom level.
4. Recommended contents for `references/`, `assets/`, and `scripts/`.
5. A validation plan: how to verify the skill works correctly.
6. Notes on multi-model compatibility if the skill has tricky implicit reasoning.

## Iteration Protocol

Follow evaluation-driven development:

1. Identify the problem the skill solves.
2. Define how to evaluate success (checklist, output diff, user feedback).
3. Establish a baseline (current behavior without the skill).
4. Write the minimal skill that improves on the baseline.
5. Test, measure, iterate.
