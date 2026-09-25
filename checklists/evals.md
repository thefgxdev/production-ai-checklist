# Evaluation checklist

If it is not measured on every change, it is not engineering.

## The golden set

- [ ] Fifty to a few hundred cases with inputs and expected outputs, written by people who know the domain.
- [ ] Covers each source, each user intent, each known failure mode, and the refusal cases.
- [ ] Versioned in the repository next to the prompts.
- [ ] Grows from production: every human-flagged mistake becomes a case.

## What to measure

| Layer | Metric |
|---|---|
| Retrieval | recall@k, precision@k, duplicate rate |
| Answer | correctness (graded), groundedness (claims supported by context), citation validity, refusal accuracy |
| Format | schema validity, length, language |
| Agent | task success, steps per task, cost per task, override rate |
| Safety | injection resistance, sensitive-data leakage, toxicity where relevant |

## How to grade

- [ ] Deterministic checks first (schema, citations exist, forbidden strings absent).
- [ ] Model-graded checks second, with a rubric, calibrated against human grades on a sample. Re-calibrate when the grader model changes.
- [ ] Human grading on a rotating sample, always. The graders are the ground truth.

## When to run

- [ ] On every change to prompt, model, retrieval parameters, chunking or tools: full golden set, blocking the merge on regressions.
- [ ] Nightly against the live index to catch data drift.
- [ ] In production: sample 1 to 5 % of traffic for human review; more for new features.

## Reporting

- [ ] One dashboard with the metrics over time and the version that produced each point.
- [ ] Regressions are incidents: they have an owner and a postmortem.
- [ ] Cost per eval run known; the set is pruned of cases that never fail and never inform.
