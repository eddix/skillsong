# Freedom Calibration Guide

## Why It Matters

A skill's freedom level controls how tightly the agent follows instructions versus making its own decisions. Miscalibrated freedom is the most common cause of disappointing skill output.

- Too much freedom on a strict task -> inconsistent, unreliable output.
- Too little freedom on an open task -> rigid, unhelpful output that misses context.

## Three Levels

### High Freedom

**Use for:** Open-ended, judgment-heavy tasks.

**Examples:** Code review, architecture advice, research synthesis, brainstorming.

**Instruction style:**
- Provide guidelines and rubrics as guardrails.
- Let the agent decide how to structure and sequence its work.
- Focus on what to evaluate, not how to evaluate it.

**Sample wording:**
```md
Review the code against the conventions in `references/conventions.md`.
Group findings by severity.
Explain why each issue matters and propose a fix.
```

### Medium Freedom

**Use for:** Template-based or scaffold tasks where structure is fixed but content varies.

**Examples:** Document generation, PR descriptions, release notes, test plans.

**Instruction style:**
- Provide a template with required sections.
- Allow flexible content within each section.
- Specify what must be present, not how to phrase it.

**Sample wording:**
```md
Load `assets/template.md`.
Fill every required section.
Adapt tone to the audience described in `references/style-guide.md`.
```

### Low Freedom

**Use for:** Strict, sequential processes where skipping steps is dangerous.

**Examples:** Database migrations, production deployments, compliance workflows, data backups.

**Instruction style:**
- Number every step.
- Add explicit gates between steps.
- Use blocking language: "Do not proceed until..."
- Require user confirmation at critical points.

**Sample wording:**
```md
1. Create a backup of the current schema.
2. Do not proceed until the backup is verified.
3. Run the migration script.
4. Validate the migration output against `references/expected-schema.md`.
5. Do not mark as complete until validation passes.
```

## Diagnosis

Ask these questions to determine the right level:

| Question | High | Medium | Low |
| --- | --- | --- | --- |
| Can the output vary significantly and still be correct? | Yes | Partially | No |
| Is there a fixed template? | No | Yes | Yes + strict order |
| Are there dangerous side effects if a step is skipped? | No | Unlikely | Yes |
| Does the task require subjective judgment? | Yes | Some | No |
| Is user confirmation needed mid-workflow? | No | Maybe | Yes |

## Multi-Model Impact

Freedom level interacts with model capability:

- **Haiku + High Freedom**: Risky. Haiku may not make good judgment calls without explicit guidance. Add more examples and guardrails.
- **Opus + Low Freedom**: Feels restrictive. Opus follows low-freedom instructions well but may feel over-constrained. This is acceptable — correctness over comfort.
- **Sonnet + Medium Freedom**: The sweet spot. Sonnet handles medium freedom naturally.
