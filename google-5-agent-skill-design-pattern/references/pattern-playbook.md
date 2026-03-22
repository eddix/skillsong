# Pattern Playbook

## Table of Contents

- Tool Wrapper
- Generator
- Reviewer
- Inversion
- Pipeline
- Composition notes

## Tool Wrapper

### Best fit

Use when the main value is domain truth: framework conventions, internal standards, API rules, or library-specific patterns.

### Resource layout

- `SKILL.md`: trigger conditions and how to apply the rules
- `references/conventions.md`: authoritative guidance

### Instruction shape

1. Tell the agent to load the conventions reference when the task touches that technology.
2. Treat the reference as the source of truth.
3. Apply the rules while writing, debugging, or reviewing.

### Good wording pattern

```md
Load `references/conventions.md` before writing or reviewing code.
Follow the conventions exactly.
When reviewing, cite the violated rule and suggest a concrete fix.
```

### Common mistake

Do not paste the full conventions guide into `SKILL.md`.

## Generator

### Best fit

Use when the output must have a repeatable structure: reports, plans, docs, summaries, or scaffolds.

### Resource layout

- `SKILL.md`: orchestration steps
- `references/style-guide.md`: tone, formatting, and quality rules
- `assets/template.md`: fixed output structure

### Instruction shape

1. Load the style guide.
2. Load the template.
3. Ask for missing variables.
4. Fill every required section.
5. Return one complete artifact.

### Good wording pattern

```md
Load the style guide first.
Load the template next.
Ask for any missing variables.
Fill every section in the template.
Return the completed document as a single artifact.
```

### Common mistake

Do not describe a generator without providing a real template or output contract.

## Reviewer

### Best fit

Use when the job is to assess quality, risk, compliance, or correctness against explicit criteria.

### Resource layout

- `SKILL.md`: review protocol
- `references/review-checklist.md`: criteria or rubric

### Instruction shape

1. Load the checklist.
2. Understand the artifact before judging it.
3. Apply every rule systematically.
4. Group findings by severity.
5. Explain why each issue matters and how to fix it.

### Good wording pattern

```md
Load `references/review-checklist.md`.
Review the artifact against every rule in the checklist.
Group findings by severity.
Explain the risk and propose a concrete fix for each finding.
```

### Common mistake

Do not merge the checklist and the review output format into one vague paragraph.

## Inversion

### Best fit

Use when the agent should ask before acting: planning, discovery, requirement gathering, or ambiguous greenfield work.

### Resource layout

- `SKILL.md`: phased interview
- optional `assets/template.md`: final synthesis format

### Instruction shape

1. Define interview phases.
2. Ask one question at a time.
3. Wait for an answer before moving on.
4. Block final synthesis until all required answers exist.

### Good wording pattern

```md
Do not start building until all phases are complete.
Ask one question at a time and wait for the user's answer.
Do not synthesize the final plan until every required answer has been gathered.
```

### Common mistake

Do not claim to use inversion if the agent still rushes into a plan after one partial answer.

## Pipeline

### Best fit

Use when the workflow has mandatory stages, approvals, or quality gates that cannot be skipped.

### Resource layout

- `SKILL.md`: ordered step definitions and gate conditions
- step-specific `references/` or `assets/` files

### Instruction shape

1. Define numbered steps in order.
2. State the artifact or decision produced at each step.
3. Add explicit stop conditions.
4. Prevent later steps from running early.

### Good wording pattern

```md
Execute each step in order.
Do not skip steps or proceed if a step fails.
Do not move to the next step until the required approval is received.
```

### Common mistake

Do not use a pipeline when there is no real checkpoint or branch that needs enforcement.

## Composition Notes

Use composition to solve multiple failure modes, not to make the skill sound sophisticated.

- Let `Inversion` gather requirements before a `Generator`.
- Let a `Pipeline` call a `Tool Wrapper` only in the steps that need specialized knowledge.
- Let a `Reviewer` sit at the end of a `Pipeline` as the final gate.
- Prefer one dominant pattern and at most one or two supporting patterns.
