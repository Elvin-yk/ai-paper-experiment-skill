---
name: ai-paper-experiment-playbook
description: Standardized workflow for paper experiments with Codex or other AI assistants, covering problem framing, reproducible setup, diagnosis, minimal-change fixes, and report-ready summaries. Use when planning new experiments, debugging failures, handling metric regressions, designing ablations, or revising method/result claims with evidence.
---

# AI Paper Experiment Playbook

## Overview

Run experiment work in a repeatable loop: frame the target, reproduce reliably, diagnose with explicit hypotheses, apply minimal changes, verify with evidence, and summarize for paper updates.

## Required Inputs

Collect these before making edits:
- Research objective and exact claim to support or refute
- Baseline command, config, commit, dataset split, and random seed
- Current failure signal (error log, metric regression, unstable variance, or inconsistency with paper text)
- Hard constraints (time budget, compute budget, deadline, no-risk files)

If any input is missing, state the gap and proceed with the safest assumption.

## Workflow

### 1) Define The Experiment Contract

Pin the contract for reproducibility:
- Metric names and acceptance thresholds
- Fixed run command and environment assumptions
- Required artifacts: logs, checkpoint path, evaluation table, run metadata

Reject vague goals like "improve performance". Replace with measurable criteria.

### 2) Reproduce Before Changing

Reproduce baseline or failure first.
- If reproduction fails, prioritize environment and data integrity checks.
- If reproduction succeeds, freeze the baseline record.

Do not propose fixes until the failure mode is observed directly or supported by concrete evidence.

### 3) Build A Hypothesis Table

List 2-5 ranked hypotheses.
For each hypothesis include:
- Why it is plausible from observed evidence
- Minimal validation action
- Expected outcome if true
- Exit condition if false

Prefer fast eliminations before expensive retraining.

### 4) Choose Minimal-Change Intervention

Select the smallest intervention that can falsify the top hypothesis:
- Config-only change before code rewrite
- Local patch before architecture rewrite
- Single factor ablation before multi-factor sweeps

When a change is risky, add a rollback path and scope boundary first.

### 5) Execute And Verify

After every intervention, verify in three layers:
- Functional: runtime completes and outputs artifacts
- Metric: target metric changes versus baseline
- Robustness: repeated runs or alternate seed sanity check

If functional passes but metric fails, treat as a model-quality issue, not a runtime fix.

### 6) Produce A Paper-Ready Update

Summarize outcomes with evidence:
- What changed
- Why this change was attempted
- Measured impact with absolute numbers
- Remaining threats to validity and next ablation

Use `references/experiment-record-template.md` for the standard report block.

## Failure Handling Patterns

### Runtime Error

- Reproduce with minimal command
- Isolate failing module and input sample
- Add narrow fix with regression guard
- Re-run baseline evaluation path

### Metric Regression

- Confirm same dataset split and seed policy
- Diff config and preprocessing paths
- Run targeted ablation to isolate the causing factor
- Keep the best-known-good checkpoint untouched

### High Variance / Instability

- Increase repeated trials with fixed seed list
- Report mean and variance, not single-run best
- Inspect data ordering, mixed precision, and nondeterministic ops

### Paper Text Mismatch

- Tie every claim to an artifact path and run ID
- Downgrade claim strength if evidence is partial
- Mark follow-up experiments explicitly

## Collaboration Rules For AI-Assisted Work

- Keep one canonical experiment log per run ID
- Separate "observation" from "inference"
- Prefer explicit assumptions over implicit guesses
- Propose no more than one primary intervention per iteration
- Stop broad refactors when the objective is a single claim validation

## Prompting Templates

Use concise, structured prompts from `references/prompt-templates.md` to reduce back-and-forth.

## Done Criteria

Treat a task as complete only when:
- Reproducible command and environment are recorded
- Change scope and rationale are documented
- Functional and metric verification are reported
- A paper-ready summary paragraph is available
