# Auditing and improving an existing skill

Use this reference for a substantive audit, simplification, or rewrite. Read the complete skill and its linked resources before editing; partial reading produces contradictory half-rewrites.

## Eleven audit dimensions

Score each dimension from 1 to 5 when a comparative audit would help. The lowest scores guide effort; the numbers are diagnostic, not a substitute for behavioral evaluation.

| # | Dimension | A strong result |
| ---: | --- | --- |
| 1 | Trigger coverage | Description covers realistic positive phrasing and avoids neighboring requests |
| 2 | Boundary clarity | Scope and adjacent owners are explicit where collision is plausible |
| 3 | Structure conformity | The chosen pattern matches the work and resources live in purposeful locations |
| 4 | Signal density | Every line changes a decision, preserves an opinion, or prevents a concrete failure |
| 5 | Gotchas quality | Warnings name an observed failure, relevant value or action, and consequence |
| 6 | Freshness | Commands, paths, tool capabilities, and assumptions match the current target environment |
| 7 | Progressive disclosure | Every supporting file has a useful load condition and avoids duplicating the entrypoint |
| 8 | Workflow integrity | Multi-step work has clear transitions, stopping conditions, and observable terminal evidence |
| 9 | Cross-skill coherence | Sibling descriptions and repository policy do not conflict or compete ambiguously |
| 10 | Content-pattern fit | Templates, examples, conditions, and rules are used only where they improve the task |
| 11 | Constraint calibration | Instruction strength matches risk and does not duplicate the harness, sibling skills, or tool interfaces |

## Rewrite order

1. **Correctness:** fix stale facts, broken links, invalid commands, unsafe behavior, and repository-policy conflicts.
2. **Discovery:** repair the name, description, triggers, and likely near-miss boundaries.
3. **Structure:** select the appropriate pattern, move conditional material, and update every reference.
4. **Signal density:** remove generic guidance, duplicated rules, unused resources, and examples that narrow the model without benefit.
5. **Constraint calibration:** convert unnecessary absolutes to outcomes while preserving safety, permissions, format contracts, and distinctive opinions.
6. **Observed gotchas:** retain concrete failures and remove hypothetical warnings that have never earned their cost.
7. **Evidence:** validate mechanically, rerun relevant routing and execution evals, and re-score if the audit used scores.

Report before/after scores only for dimensions actually inspected. A higher structural score does not justify worse behavioral results.

## Rightsizing rules

- Remove an instruction if a capable target model reliably behaves the same without it and it encodes no deliberate preference.
- Keep a house style, product opinion, or domain decision even when it cannot be objectively graded; that opinion may be the skill's reason to exist.
- Ablate one suspected constraint at a time so a regression can be attributed.
- A large ruleset should be sampled by category after its shared schema and index are checked; rewriting every correct rule creates unnecessary risk.
- After moving a file, search the repository for the old path and repair every caller.
