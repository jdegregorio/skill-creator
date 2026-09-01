---
name: skill-creator
description: Create, audit, improve, and behaviorally evaluate portable Agent Skills. Use when users ask to create a skill, edit or review SKILL.md, structure a skill bundle, test skill routing or execution, compare revisions, simplify an over-constrained skill, or turn an observed workflow into a proposed skill. Do not use for installing, updating, vendoring, distributing, or tracking upstream skills.
metadata:
  short-description: Create and evaluate portable skills
---

# Skill Creator

Engineer small, portable instruction bundles whose behavior is observable and maintainable across agent harnesses.

- **IS:** skill design, authoring, auditing, focused improvement, routing tests, execution evals, and revision comparison.
- **IS NOT:** skill installation, activation, discovery-root mutation, upstream tracking, vendoring, release packaging, or distribution. Those are separate lifecycle concerns; a future skill manager may own them, but this skill does not implement one.

## Choose the mode

- **Create:** turn a clear capability or an observed successful workflow into a new skill.
- **Improve:** audit or revise an existing skill without erasing the opinions that make it useful.
- **Evaluate:** test whether a skill routes correctly and improves task outcomes.
- **Benchmark:** compare revisions with repeated or blind trials when the decision warrants the extra cost.

Use the narrowest mode that satisfies the request. A small copy edit does not need a benchmark; a new skill with fragile outputs may.

## Read references selectively

| Reference | Read when |
| --- | --- |
| [architecture.md](references/architecture.md) | Creating a skill, changing its structure, calibrating constraints, or deciding which resources belong in the bundle |
| [audit.md](references/audit.md) | Auditing, simplifying, rightsizing, or substantially rewriting an existing skill |
| [evaluation.md](references/evaluation.md) | Designing routing tests, execution evals, comparisons, benchmarks, or constraint ablations |
| [openai_yaml.md](references/openai_yaml.md) | Creating or changing `agents/openai.yaml` |
| [sources.md](references/sources.md) | Maintaining this canonical creator or reviewing its design lineage; do not load for ordinary skill work |
| [evals/cases.json](evals/cases.json) | Regression-testing this canonical creator's routing and execution behavior; do not load for ordinary skill work |

## Work from evidence

Before writing, inspect the target repository instructions, the complete existing skill if any, linked resources, sibling skill descriptions, and any validator or format contract supplied by the target harness.

Extract useful evidence from the current conversation before asking questions: the task sequence, corrections, chosen tools, observed failures, expected artifacts, and user preferences. Treat these as candidate requirements, not automatically universal rules. Ask only for missing information that would materially change scope, triggers, outputs, dependencies, permissions, or evaluation.

Define the contract in plain language:

1. What capability should the skill add?
2. Which realistic requests should and should not trigger it?
3. What observable outcome indicates success?
4. Which knowledge, scripts, tools, inputs, or permissions does it genuinely require?
5. Which neighboring workflow owns requests outside its boundary?

## Create or revise the skill

1. Choose a simple/hub, workflow, rules-based, or mixed structure using [architecture.md](references/architecture.md).
2. For a new Codex-compatible skill, use the initializer when it saves mechanical setup:

   ```bash
   scripts/init_skill.py <skill-name> --path <output-directory> [--resources scripts,references,assets]
   ```

3. Write a lowercase hyphenated name and a discriminating description. The description is a routing interface: say what the skill does, when it applies in language users actually use, and a boundary only when it prevents a likely collision.
4. Keep `SKILL.md` as the shared map and essential workflow. Move conditional detail to references, repeated deterministic work to scripts, output ingredients to assets, and categorized audit criteria to rules.
5. Match instruction strength to fragility. Preserve exact commands and absolutes for safety, destructive operations, permissions, schemas, and format contracts; otherwise describe the desired outcome and let context choose the path.
6. Prefer code, tests, or an existing implementation as the contract when they are more precise than prose. Do not duplicate policy already owned by the harness, repository instructions, a sibling skill, or a script interface.
7. Add no placeholder directory, README, changelog, installer, manifest, or packaging machinery unless the request or actual runtime contract requires it.

When updating `agents/openai.yaml`, preserve unrelated fields and follow [openai_yaml.md](references/openai_yaml.md). Keep automatic invocation unless the user explicitly requests explicit-only behavior.

## Validate the artifact

Run the validator supplied with this skill for Codex-compatible bundles:

```bash
scripts/quick_validate.py <path-to-skill-folder>
```

Then verify the parts a static validator cannot:

- The description distinguishes the skill from its siblings.
- Every reference has a useful read condition and no required file is orphaned.
- New or changed scripts execute successfully on representative inputs.
- Instructions preserve the user's scope and authorization boundaries.
- The skill changes decisions or outcomes rather than restating model defaults.

Use the target repository's validator instead when it defines stricter or different rules. Do not rewrite third-party or harness-owned skills merely to satisfy this validator.

## Evaluate proportionally

Treat routing and execution as separate failure classes:

- **Routing:** does the harness select the skill for realistic positive cases and avoid it for realistic near-misses?
- **Execution:** once loaded, does the skill improve the observable result or workflow?

For a narrow edit, realistic prompt review and focused checks may be enough. For a new, complex, fragile, or frequently used skill, read [evaluation.md](references/evaluation.md) and create a durable eval set. Compare against no skill for a new capability or against a snapshot of the old skill for a revision. Keep task inputs, model, tools, permissions, and environment equivalent where possible.

Use independent executors, graders, or blind comparators only when the harness supports them, delegation is authorized, and independence materially improves confidence. Otherwise run a smaller inline evaluation and state its limitations. Ask before tests that create external side effects, affect live systems, incur material cost, or require new access.

## Improve from observed behavior

Change the smallest thing supported by evidence. Fix stale or incorrect facts first, then triggers, structure, signal density, constraint calibration, and polish. Generalize from failures without coding the test prompt into the instructions.

When a rule looks unnecessary, ablate it: remove one suspected constraint, rerun representative evals, and keep it only if behavior regresses. Do not ablate the explicit taste or domain opinion the skill exists to encode merely because it lacks an objective failure case.

Stop iterating when the requested behavior is reliable enough for its risk, the user is satisfied, or further revisions produce no meaningful gain. Report the artifact path, validation evidence, behavioral evidence actually gathered, and any deferred uncertainty.

## Gotchas

- A syntactically valid description can still route badly; only positive and near-miss routing cases reveal that failure.
- A skill can raise pass rate by teaching to weak assertions; graders should cite evidence and challenge non-discriminating checks.
- A cleaner audit score with worse task outcomes is a regression; form supports behavior but does not replace it.
- Editing a repository copy does not prove the active harness loaded that copy. Activation and installed-copy reconciliation are outside this skill's scope.
