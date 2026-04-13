# Submission Guide

This repository is packaged to support benchmark-style submissions.

## Recommended Submission Form

Use three linked pieces:

1. **Notebook**
   - Use `notebooks/frontier_local_metacognition_submission.ipynb`
   - This is the primary execution and presentation artifact

2. **GitHub Repository**
   - Use this repository as the public code and artifact reference
   - It contains the frozen task set, runner, scoring, release docs, and result snapshots

3. **Short Writeup**
   - Use the material in `docs/releases/`
   - Include the task taxonomy, metric definitions, main result table, figure, limitations, and reproduction commands

## Submission Assets In This Repo

- `docs/releases/frontier_local_submission_bundle.md`
- `docs/releases/frontier_local_metacognition_first_results.md`
- `docs/releases/frontier_local_metacognition_expansion.md`
- `docs/releases/frontier_local_metacognition_expansion_abstract.md`
- `notebooks/frontier_local_metacognition_submission.ipynb`
- `submission/frontier_local_metacognition/`

## Core Claim

Small open models can avoid bluffing and silent failure while still failing metacognitively by collapsing ordinary uncertainty into escalation instead of using abstention correctly.

## Expanded Post-Submission Claim

The benchmark separates multiple metacognitive failure modes, including:
- over-escalation collapse
- under-escalation / over-abstention tradeoff
- parse / bluff fragility
