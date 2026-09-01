# Behavioral evaluation

Use this reference when static validation is insufficient to establish that a skill routes correctly or improves work.

## Separate routing from execution

Routing evaluation asks whether the skill is selected. Execution evaluation assumes it is loaded and asks whether it improves the task. A perfect body cannot repair under-triggering, and an excellent description cannot repair a weak workflow.

### Routing cases

Build realistic prompts that resemble actual user requests:

- positive cases spanning formal, casual, abbreviated, and implicit phrasing;
- uncommon but valid cases near the skill's boundary;
- negative near-misses that share keywords but belong to a sibling or require no specialized skill;
- ambiguous cases where a better boundary or sibling description should decide the route.

Avoid obviously unrelated negatives; they inflate accuracy without testing discrimination. Hold out some cases when optimizing a description so improvements are not selected only on the prompts that inspired them.

A portable routing fixture can use:

```json
{
  "prompt": "realistic user request",
  "should_trigger": true,
  "reason": "the capability and boundary being tested"
}
```

### Execution cases

Each case should include a realistic prompt, required input files, an expected outcome, and observable expectations. Prefer checks that are difficult to pass without genuinely completing the task.

```json
{
  "id": "descriptive-case-name",
  "prompt": "realistic user request",
  "files": [],
  "expected_outcome": "what successful work accomplishes",
  "expectations": [
    "observable and evidence-backed condition"
  ]
}
```

Do not force quantitative assertions onto taste. Use human review or a blind quality rubric for subjective writing, design, or judgment-heavy outputs.

## Compare equivalent runs

For a new skill, compare treatment with the skill against a baseline without it. For an improved skill, snapshot the old version before editing and use that as the baseline. Keep the prompt, inputs, model, tools, permissions, and environment the same where possible.

Capture outputs and enough of the execution trace to explain the result. If the harness reliably exposes them, record duration, tokens, tool calls, and errors; do not invent missing metrics.

Use these roles as evaluation responsibilities, not as mandatory implementation machinery:

- **Executor:** completes the task in a fresh context and preserves outputs and trace evidence.
- **Grader:** checks expectations against artifacts, cites evidence, verifies claims, and flags weak or unverifiable assertions.
- **Comparator:** receives anonymized outputs A and B and judges task quality without knowing which revision produced them.
- **Analyzer:** looks across cases and repetitions for non-discriminating assertions, flaky cases, regressions, variance, and cost-quality tradeoffs.

Separate contexts or agents improve independence only when the harness supports them and delegation is authorized. Inline evaluation is acceptable when independence is unavailable; state the limitation.

## Choose evaluation depth by risk

| Situation | Proportionate evidence |
| --- | --- |
| Metadata or narrow wording edit | Static validation plus a few positive and near-miss routing cases |
| Small workflow correction | Representative execution cases focused on the observed failure |
| New or substantially revised skill | Routing suite plus baseline/treatment execution cases |
| High-value, stochastic, or disputed revision | Repeated runs, blind comparison, aggregate results, and variance analysis |
| Subjective output | Human review and a task-specific rubric, optionally blind |

Do not perform live external mutations merely to test a skill. Use an isolated workspace, mocks, fixtures, or dry-run behavior where possible. Obtain approval before additional access, material cost, or unavoidable side effects.

## Grade with evidence

An expectation passes only when the artifact or trace provides concrete evidence of substantive completion. A filename, heading, or keyword is not enough if its contents can still be wrong.

For each expectation record:

- the original check;
- pass or fail;
- specific evidence;
- any important claim that could not be verified.

Challenge the eval itself. If both baseline and treatment always pass, the assertion may be non-discriminating. If important failures escape every check, add a meaningful expectation instead of merely tightening wording.

## Iterate and ablate

1. Identify a specific routing or execution failure.
2. Make the narrowest general correction.
3. Rerun the affected cases and representative regression cases.
4. Expand the set when a new failure class appears.
5. Remove one suspected dead constraint and rerun; restore it only if behavior regresses.

Stop when the treatment reliably meets the required outcome for the skill's risk, the user accepts the qualitative result, or further revisions make no meaningful improvement. Preserve the eval cases with the skill only when maintainers will actually rerun them.
