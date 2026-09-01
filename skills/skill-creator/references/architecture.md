# Skill architecture and authoring

Use this reference to choose a skill shape, allocate content to files, and calibrate how prescriptive the instructions should be.

## Pick the smallest structural pattern that fits

| Pattern | Use when | Typical shape |
| --- | --- | --- |
| Simple/hub | Dispatching among a few independent tracks or modes | Short `SKILL.md` plus focused track files |
| Workflow | Guiding a sequential process with details loaded at specific steps | `SKILL.md` plus `references/` |
| Rules-based | Auditing or linting against categorized criteria | `SKILL.md` plus `rules/` and an output contract |
| Mixed | A workflow has substantial platform-, framework-, or context-specific branches | Workflow entrypoint plus conditional references or rules |

Choose workflow when uncertain; it tolerates growth without forcing every invocation to load every branch. Do not add a routing layer when the skill has only one short path.

## Allocate content by runtime purpose

| Location | Put here | Keep out |
| --- | --- | --- |
| `SKILL.md` | Purpose, boundaries, shared workflow, essential constraints, and links with read conditions | Conditional manuals, exhaustive examples, duplicated policy |
| `references/` | Domain rules, schemas, advanced procedures, evaluation methods, or variant-specific details | Files never linked or always needed |
| `scripts/` | Repeated deterministic transformations or checks whose implementation should not be recreated each run | One-off glue, opaque automation without an interface |
| `assets/` | Templates, media, fonts, or boilerplate copied into user output | Instructions the agent must reason from |
| `rules/` | One concern per rule for large categorized audit/lint skills | Ordinary workflow prose |
| `agents/` | Harness-facing metadata or reusable role prompts required by a supported runtime | General documentation for the model |
| `evals/` | Maintained regression cases and fixtures used when changing the skill | Runtime instructions for ordinary user tasks |

Split files by loading condition, not an arbitrary line count. If two topics are needed at different moments, separate them. If a reference is required on every invocation, its essential content probably belongs in `SKILL.md`.

## Calibrate constraints

Match specificity to the cost of deviation:

- **High freedom:** prose describing outcomes when several approaches are valid.
- **Medium freedom:** pseudocode, a parameterized interface, or a preferred default with a known escape hatch.
- **Low freedom:** exact commands or schemas for destructive, fragile, consistency-critical, or permission-sensitive operations.

For each instruction, ask:

1. Would a capable model already do this correctly without the skill?
2. Is this an enduring product, team, or domain opinion that makes the skill valuable?
3. Does another authority already own it?
4. What concrete failure would removing it cause?

Cut generic competence reminders. Keep real opinions, non-obvious invariants, observed gotchas, safety boundaries, and format contracts. Prefer explaining the consequence over accumulating exception lists.

## Design discovery as an interface

The name and description are the only skill content available during routing in many harnesses. Optimize them for model selection, not as marketing copy.

- Use a specific action-oriented name.
- State the capability and realistic contexts in which it applies.
- Include phrases and domain nouns users naturally supply.
- Add exclusions only for plausible neighboring requests.
- Avoid catchalls that attract work the skill does not improve.

Examples are valuable when output style is the contract. For callable tools, spend those tokens on clear parameters, allowed values, and failure behavior instead. Prefer a tested implementation or test suite over a prose retelling of its contract.

## Capture a workflow without overfitting

When creating a skill from a successful session, extract:

- decisions that changed the outcome;
- corrections the user repeated or emphasized;
- tool sequences that avoided real failure;
- stable inputs, outputs, invariants, and stopping conditions;
- context that was incidental to this one task.

Convert only the stable portion into skill guidance. Keep one-off project facts in the project and personal/runtime facts in their owning system. A single success is evidence for a candidate workflow, not proof that every step should become mandatory.
