# Skill Authoring Checklist

Use this checklist to validate a skill before shipping. Every item should pass.

## Frontmatter

- [ ] `name` uses only lowercase letters, numbers, and hyphens.
- [ ] `description` states what the skill does in third person.
- [ ] `description` includes when to trigger the skill.
- [ ] `description` is one to two sentences, not a paragraph.

## Structure

- [ ] `SKILL.md` contains only triggers, workflow, gates, and load instructions.
- [ ] Large domain documents live in `references/`, not inline in `SKILL.md`.
- [ ] Templates and output skeletons live in `assets/`.
- [ ] Deterministic utilities live in `scripts/`.
- [ ] No unnecessary files — every file has a clear purpose.

## Instructions

- [ ] Instructions are imperative ("Load the checklist", not "You should load the checklist").
- [ ] Only information the model does not already know is included.
- [ ] No filler, preamble, or redundant explanations.
- [ ] Freedom level matches the task type (high/medium/low).
- [ ] Multi-step workflows use numbered lists.
- [ ] Feedback loops are present: execute -> verify -> fix -> repeat.
- [ ] Blocking gates use explicit language: "Do not proceed until..."

## Content Quality

- [ ] No time-sensitive information in `SKILL.md` (versions, dates).
- [ ] Terminology is consistent throughout all files.
- [ ] No magic numbers — all values are explained.
- [ ] POSIX paths only (forward slashes).
- [ ] Examples are concrete with clear input/output pairs.

## Multi-Model

- [ ] Instructions work for Sonnet without modification.
- [ ] Haiku can follow the steps without implicit reasoning gaps.
- [ ] Opus is not annoyed by over-explanation.
- [ ] Critical steps have examples that help weaker models without cluttering.

## Verification

- [ ] The skill has a way to validate its output (checklist, test, diff).
- [ ] Error cases are handled explicitly, not ignored.
- [ ] The skill has been tested with at least one real scenario.

## Anti-Pattern Check

- [ ] No full documents pasted into `SKILL.md`.
- [ ] No vague descriptions without trigger conditions.
- [ ] No excessive choices that cause decision fatigue.
- [ ] No pipeline pattern when a simple checklist would suffice.
- [ ] No Windows-style paths.
