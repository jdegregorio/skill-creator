# Design lineage

Read this file only when maintaining the canonical creator or reviewing why its architecture differs from a harness-supplied implementation.

This skill synthesizes three primary approaches:

- [mblode Agent Skills Creator](https://github.com/mblode/agent-skills/tree/main/skills/agent-skills-creator): structural patterns, progressive disclosure, constraint calibration and ablation, and the eleven-dimension audit.
- [Anthropic Skill Creator](https://github.com/anthropics/skills/tree/main/skills/skill-creator): separate routing and execution evaluation, baseline/treatment runs, evidence-backed grading, blind comparison, analysis, and benchmarking.
- [OpenAI Skill Creator](https://github.com/openai/skills/tree/main/skills/.system/skill-creator): Codex-compatible bundle anatomy, UI metadata, initializer, and static validator.

The OpenAI helper scripts, icons, and license are retained as the local compatibility baseline. The canonical instructions are intentionally harness-neutral and keep evaluation responsibilities portable rather than depending on one vendor's runner.

Deliberate exclusions:

- No skill manager, installer, upstream tracker, vendoring workflow, release pipeline, or distribution adapter.
- No mandatory multi-agent harness or browser-based eval viewer.
- No broad session-mining system. The creator may extract candidate requirements from the current task, while a future distillation workflow can own systematic learning from history.
- No separate skill evaluator yet. This creator owns proportionate behavioral evaluation until that boundary proves useful in practice.
