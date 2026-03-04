# Prompt Templates For AI-Assisted Experiments

## 1) Failure Diagnosis Prompt

Use when a run fails or metric drops.

```
You are helping with a paper experiment.
Goal claim: <claim>
Baseline setup: <command/config/seed/dataset>
Observed issue: <error or metric regression>
Evidence: <log snippets, metric table>
Constraints: <time/compute/file scope>

Task:
1) Propose top 3 hypotheses ranked by likelihood.
2) For each, provide one minimal validation step.
3) Recommend the smallest safe intervention first.
Return in a table: hypothesis | evidence | test | expected result.
```

## 2) Minimal Patch Prompt

Use after choosing a single hypothesis.

```
Given this hypothesis: <hypothesis>
Apply only the minimal patch needed to validate it.
Requirements:
- Avoid unrelated refactors.
- Preserve backward compatibility where possible.
- Add brief comments only where logic is non-obvious.
Return:
1) files changed
2) exact behavior change
3) rollback instructions
```

## 3) Verification Prompt

Use after implementation.

```
I need a strict verification plan for this experiment change.
Baseline metrics: <numbers>
New metrics: <numbers or pending>
Run command: <command>

Return checklist with three sections:
- Functional pass/fail checks
- Metric comparisons (absolute and relative)
- Robustness checks (repeat runs/seeds)
Include stop conditions if results are inconclusive.
```

## 4) Paper Summary Prompt

Use when writing method/result updates.

```
Convert the experiment outcome into a paper-ready paragraph.
Inputs:
- Intervention:
- Reasoning:
- Quantitative outcomes:
- Threats to validity:
- Next ablation:

Constraints:
- No over-claiming.
- Every claim must map to a measured artifact.
- Keep to 80-140 words.
```
