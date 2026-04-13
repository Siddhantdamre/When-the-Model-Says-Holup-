# Contributing

Thanks for contributing.

This repository is intentionally small and benchmark-focused, so the main rule is: **preserve benchmark comparability**.

## What To Keep Stable

Unless you are fixing a factual bug, do not change:
- the task set
- prompt wording
- scoring definitions
- action semantics for `COMMIT`, `ABSTAIN`, and `ESCALATE`
- released result wording

These are part of the benchmark contract.

## Good Contributions

Strong contribution types include:
- documentation improvements
- reproducibility fixes
- local runner robustness improvements
- cleaner result aggregation and reporting
- additional open-weight model comparisons that do not alter the benchmark contract

## Changes That Need Extra Care

Please open an issue or clearly explain the rationale before changing:
- task definitions
- parser behavior
- metric definitions
- benchmark scope
- submission-facing claims

## Development Notes

Install dependencies:

```bash
python -m pip install -r requirements.txt
```

Run a local benchmark:

```bash
python benchmarks/exec_meta_adapt/frontier_local/run_frontier_local.py --models qwen smollm --tasks benchmarks/exec_meta_adapt/frontier/frontier_tasks_metacog.jsonl --output results/frontier_local/full_40/
```

## Pull Requests

Good pull requests should include:
- what changed
- why it changed
- whether the benchmark contract changed
- what you ran to validate it

If the change affects a published result, state that explicitly.
