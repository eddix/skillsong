# Progressive Disclosure Guide

## Core Principle

Progressive disclosure means showing only what is needed at each level. The agent reads `SKILL.md` first. It loads additional resources only when the workflow requires them. This keeps the context window lean and focused.

## Three Layers

### Layer 1: YAML Frontmatter

The entry point. Determines whether the skill is activated.

**Contains:**
- `name`: identifier
- `description`: what + when

**Rule:** If the description does not clearly state when to trigger, the skill will fire at wrong times or not fire at all.

### Layer 2: SKILL.md Body

The control layer. Defines behavior, workflow, and gates.

**Contains:**
- Goal statement
- Working method (numbered steps)
- Rules and constraints
- Gate conditions
- Load instructions for references and assets

**Rule:** If you cannot fit it in two screen-lengths, move detail to `references/`.

### Layer 3: Linked Resources

The knowledge layer. Loaded on demand.

| Directory | Purpose | Examples |
| --- | --- | --- |
| `references/` | Domain knowledge, checklists, rubrics, decision tables | `conventions.md`, `review-checklist.md` |
| `assets/` | Templates, starter files, output skeletons | `template.md`, `scaffold/` |
| `scripts/` | Deterministic automation | `validate.sh`, `generate.py` |

**Rule:** If the content becomes part of the generated output, it belongs in `assets/`. If it guides the agent's behavior, it belongs in `references/`.

## Decision Flowchart

```
Is this information needed on every invocation?
├─ Yes -> SKILL.md
└─ No
   ├─ Is it domain knowledge, rules, or criteria?
   │  └─ Yes -> references/
   ├─ Is it a template or becomes part of the output?
   │  └─ Yes -> assets/
   └─ Is it a repeatable script?
      └─ Yes -> scripts/
```

## Common Mistakes

1. **Monolithic SKILL.md**: Pasting an entire style guide into SKILL.md. The agent loads it every time even when unrelated tasks trigger.
   - Fix: Move the style guide to `references/style-guide.md` and add a load instruction.

2. **Empty references/**: Writing everything inline and leaving `references/` unused.
   - Fix: Extract checklists, rubrics, and long examples into separate files.

3. **Missing load instructions**: Creating reference files but never telling the agent to load them.
   - Fix: Add explicit `Load references/foo.md before...` instructions in `SKILL.md`.

4. **Overloaded assets/**: Putting behavioral instructions in `assets/`.
   - Fix: `assets/` is for content that becomes part of the output. Move behavioral rules to `references/`.
