# When the Model Says "Holup"

A benchmark for metacognitive reasoning under partial observability.

This repository tests whether models can correctly distinguish among:
- `COMMIT`: evidence is sufficient for a conclusion
- `ABSTAIN`: evidence is insufficient, but there is no contradiction or trust collapse
- `ESCALATE`: contradiction, trust failure, or model insufficiency requires outside review

The core result is simple but important:

> Small open models can avoid bluffing and silent failure while still failing metacognitively by collapsing ordinary uncertainty into escalation instead of using abstention correctly.

This benchmark does more than rank models by one score. It separates distinct metacognitive failure modes.

---

## Why This Benchmark Exists

Many safety-style evaluations reward not bluffing. That matters, but it is not enough.

A model can look safe simply by escalating too often. This benchmark is built to detect that difference.

It asks whether a model can tell apart:
- ordinary uncertainty, where `ABSTAIN` is correct
- genuine trust failure or structural contradiction, where `ESCALATE` is correct
- sufficiently supported cases, where `COMMIT` is correct

---

## Main Finding

Across the current open-weight model slice, the benchmark separates at least three failure modes:

- **Over-escalation collapse**: `qwen`, `smollm`
- **Under-escalation / over-abstention tradeoff**: `granite`
- **Parse / bluff fragility**: `tinyllama`

That makes the benchmark useful for studying metacognitive behavior, not just final accuracy.

---

## Visual Summary

![Open-weight metacognition expansion](docs/releases/frontier_local_metacognition_expansion.svg)

---

## Main Result Table

| Model | Final Acc | Abstain | Bluff | Escalate | Silent Failure | Parse Error |
|---|---:|---:|---:|---:|---:|---:|
| `granite` | `0.53` | `0.55` | `0.00` | `0.05` | `0.00` | `0.15` |
| `qwen` | `0.72` | `0.05` | `0.00` | `0.75` | `0.00` | `0.00` |
| `smollm` | `0.75` | `0.00` | `0.00` | `0.75` | `0.00` | `0.00` |
| `tinyllama` | `0.17` | `0.00` | `0.30` | `0.00` | `0.05` | `0.53` |

Interpretation:
- `qwen` and `smollm` are safe in the narrow sense, but over-escalatory.
- `granite` handles ordinary uncertainty better, but under-escalates when escalation is truly required.
- `tinyllama` is a fragility baseline with parse failures and bluffing.

---

## Repository Layout

| Path | Purpose |
|---|---|
| `benchmarks/exec_meta_adapt/frontier/` | frozen task set, prompt builder, parser, scorer |
| `benchmarks/exec_meta_adapt/frontier_local/` | no-API local/open-weight runners |
| `docs/releases/` | benchmark notes, result writeups, and figures |
| `notebooks/` | submission notebook |
| `submission/` | packaged submission artifacts |
| `results/` | scored run outputs for the main local benchmarks |

---

## Quick Start

Install dependencies:

```bash
python -m pip install transformers accelerate sentencepiece
```

Run the baseline local benchmark:

```bash
python benchmarks/exec_meta_adapt/frontier_local/run_frontier_local.py --models qwen smollm --tasks benchmarks/exec_meta_adapt/frontier/frontier_tasks_metacog.jsonl --output results/frontier_local/full_40/
```

Run the 4-model expansion:

```bash
python benchmarks/exec_meta_adapt/frontier_local/run_frontier_local.py --models granite qwen smollm tinyllama --tasks benchmarks/exec_meta_adapt/frontier/frontier_tasks_metacog.jsonl --output results/frontier_local/open_model_expansion/full_40_single/
```

---

## Key Files

- `benchmarks/exec_meta_adapt/frontier/frontier_tasks_metacog.jsonl`
- `benchmarks/exec_meta_adapt/frontier/scoring_frontier.py`
- `benchmarks/exec_meta_adapt/frontier_local/run_frontier_local.py`
- `benchmarks/exec_meta_adapt/frontier_local/run_frontier_local_expansion.py`
- `docs/releases/frontier_local_submission_bundle.md`
- `docs/releases/frontier_local_metacognition_expansion.md`
- `notebooks/frontier_local_metacognition_submission.ipynb`

---

## Scope

This repository is about metacognitive benchmarking under hidden-state uncertainty.

It is not claiming:
- AGI
- general intelligence
- consciousness
- broad world-model competence

It does claim:
- a reusable benchmark for `COMMIT` vs `ABSTAIN` vs `ESCALATE`
- open-weight baseline comparisons
- evidence that models can be safe-looking while still metacognitively miscalibrated
