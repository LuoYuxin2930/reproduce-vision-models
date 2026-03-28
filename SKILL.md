---
name: vision-model-reproduction
description: Reproduce, assess, or extend deep learning vision models from papers and public repositories. Use when Codex needs to turn a user task description into a candidate-model scan, judge reproduction feasibility before implementation, separate official-package validation from raw-data reconstruction, or deliver a structured report covering the selected model, dataset, results, blockers, and operations performed.
---

# Vision Model Reproduction

Assess whether a public vision model is worth reproducing, execute the reproduction in a controlled order, and leave behind a report that another engineer can audit. Treat this as a reproducibility workflow, not a paper-summary workflow.

## Default Posture

- Act like a reproducibility engineer. Prefer evidence over optimism.
- Prefer primary sources: official paper pages, official repositories, author-maintained checkpoints, and benchmark documentation.
- Stay inside the current project directory unless the user explicitly approves borrowing from other directories or projects.
- If a critical detail is hidden, contradictory, or missing, mark a blocker instead of guessing.

## Workflow

1. Parse the user request into a one-line target statement: task, domain, expected output, and whether the user already named a model.
2. If the user did not already name a model, search for candidate models in the relevant visual subdomain before touching code. Use primary sources and capture the scan date.
3. Score each candidate with the feasibility rubric in [references/feasibility-rubric.md](./references/feasibility-rubric.md). Favor public code, public checkpoints, transparent preprocessing, clear evaluation protocol, and realistic compute requirements.
4. If the user already named a model, still perform a compact feasibility check and note one or two fallback candidates when appropriate.
5. Before editing code or running long jobs, write an experiment card using [references/experiment-card-template.md](./references/experiment-card-template.md).
6. Choose exactly one reproduction track for the run:
   - Official-package validation track: official repository, official checkpoint, and official processed inputs or artifacts.
   - Raw-data reconstruction track: rebuild inputs from raw benchmark data using only approved sources.
7. Never mix intermediate artifacts between the two tracks. A processed artifact from one track cannot silently become the default input of the other.
8. Lock the data contract before model work:
   - dataset root
   - metadata files and column names
   - label protocol and class mapping
   - subset, split, or subject policy
   - excluded samples or classes
   - any project-specific manifest or cleaned copy, with reason
9. Reproduce the environment before reproducing the result. Record interpreter version, framework versions, key library versions, hardware availability, and any compatibility compromise.
10. Run a smoke test before any full evaluation. Confirm imports, checkpoint loading, one minimal forward pass or tiny fold, correct path resolution, and successful logging/output writes.
11. Only after the smoke test passes, run the full evaluation or training schedule.
12. If results diverge, attribute failure in this order:
   - data protocol mismatch
   - sample filtering mismatch
   - frame or image alignment mismatch
   - preprocessing mismatch
   - training or evaluation logic mismatch
   - inconsistency between public checkpoints, logs, and reported claims
13. Treat extensions conservatively. A baseline is extendable only if at least one of these is true:
   - the official package is reproducible on this machine
   - the raw-data reconstruction path is stable and repeatable
14. If the baseline is not locked, frame extra changes as a new experiment branch rather than as a direct continuation of the original method.
15. Finish with a structured report using [references/report-template.md](./references/report-template.md). The report must name the selected model, dataset, final results, blockers, and the operations performed.

## Search And Selection Rules

- Search broadly enough to compare at least a small set of realistic candidates unless the task is already pinned down.
- Down-rank candidates that depend on hidden processed inputs, unavailable metadata, dead links, private assets, or brittle legacy toolchains.
- Distinguish novelty from reproducibility. A strong result on paper does not automatically mean a strong reproduction target.
- If several candidates look viable, recommend the highest-feasibility option and briefly mention the strongest runner-up.
- When the user wants a practical baseline, optimize for reproducibility first and novelty second.

## Hard Rules

- Do not reuse code, caches, checkpoints, processed artifacts, or label copies from sibling projects by default.
- Before changing existing source files, create a same-directory backup or a clear working copy when the repo workflow allows it.
- Preserve original metadata. Put cleaning rules in a per-project manifest or cleaned copy and explain why each change exists.
- Do not guess hidden preprocessing details.
- Write down exact code paths, data paths, checkpoint paths, and any fallback or manual intervention.
- Stop and mark the run as blocked when the reproduction depends on an unverified external asset or an ambiguous protocol definition.

## Deliverables

Every meaningful run should leave behind:

- `experiment_card.md`
- `environment.txt`
- `manifest_or_subset.csv`
- `smoke_test.log`
- `full_results.json` or equivalent structured results file
- `repro_report.md`

## References

- [references/feasibility-rubric.md](./references/feasibility-rubric.md)
- [references/experiment-card-template.md](./references/experiment-card-template.md)
- [references/report-template.md](./references/report-template.md)
