# Feasibility Rubric

Use this rubric before committing to a reproduction target. Score each category from `0` to `2`.

- `0`: weak or missing
- `1`: partial or uncertain
- `2`: strong and explicit

## Categories

### 1. Public implementation

- Is there an official or widely trusted public repository?
- Is the training or evaluation entrypoint discoverable?

### 2. Public artifacts

- Are checkpoints, logs, configs, or release assets available?
- Are the released artifacts tied clearly to the reported result?

### 3. Dataset access

- Can the required dataset or benchmark be accessed by the user?
- Are the license, download steps, and split definitions clear?

### 4. Protocol clarity

- Are the label mapping, subset policy, split method, and metrics explicit?
- Is the evaluation scope described clearly enough to avoid silent mismatch?

### 5. Preprocessing transparency

- Are preprocessing steps documented end to end?
- Can the required inputs be rebuilt from raw data without hidden assets?

### 6. Environment health

- Are the dependencies still installable?
- Is the toolchain compatible with current hardware and frameworks?

### 7. Compute fit

- Can the run fit the available machine budget?
- Is there a reasonable smoke-test path before the full run?

### 8. Risk of hidden dependencies

- Is there any sign that success depends on unpublished metadata, silent manual cleanup, or private intermediate artifacts?

## Decision Bands

- `13-16`: strong reproduction candidate
- `9-12`: feasible with targeted risk
- `5-8`: research-heavy and likely blocker-prone
- `0-4`: poor candidate without extra assets or clarification

## Output Template

Use a compact table or bullet list:

- Candidate:
- Task/domain:
- Score:
- Strongest positives:
- Main blockers:
- Recommended track:
- Recommendation:

`Recommended track` should be either `official-package validation` or `raw-data reconstruction`.
