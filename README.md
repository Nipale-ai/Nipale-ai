# Niklas Lenz

Wuppertal, Germany. I run local AI at home on my own hardware: an RTX 5090,
two RTX 5060 Ti and four DGX Sparks (GB10).

## What I do

Independent, reproducible measurements of public local-LLM recipes and models.
I rank what runs best on the machine you own. Raw data and exact commands stay
public, and fixes go back upstream as issues and PRs.

## Upstream contributions

- [PR #15](https://github.com/MiaAI-Lab/Qwen3.8-27B-16gb-NVIDIA-GPUs-one-click-install/pull/15)
  (merged): opt-in `DRAFT=dflash2` for 32 GB cards in the Qwen3.8-27B one-click kit.
- [PR #76](https://github.com/MiaAI-Lab/Qwen3.8-Flash-Next-Single-DGX-Spark/pull/76)
  — keeps JSON args intact in the launcher, tested with seven launches on a DGX Spark.
- Independent measurement for [PR #70](https://github.com/MiaAI-Lab/Qwen3.8-Flash-Next-Single-DGX-Spark/pull/70)
  (k=6 MTP guard): +20–28 % code confirmed — the PR merged into `main` via #72.
- Tested all three crash-fix PRs in
  [issue #53](https://github.com/MiaAI-Lab/Qwen3.8-Flash-Next-Single-DGX-Spark/issues/53)
  on a fresh install; the winning fix also landed.
- Full measurement report for the RTX-5090 recipe:
  [issue #4](https://github.com/MiaAI-Lab/Qwen3.8-27B-NVFP4-RTX-5090/issues/4)
  — incl. the explanation for the build-time OOM in #1.

## Repos

- **[local-llm-field-reports](https://github.com/Nipale-ai/local-llm-field-reports)** —
  reports and raw data behind my measurements.
- **[qwen-image-21-turbo-compare](https://nipale-ai.github.io/qwen-image-21-turbo-compare/)** —
  Qwen-Image-2.1 Turbo vs base on one RTX 5090, with a slider.
- One-shot builds & model comparisons: [local-voxel-benchmark](https://github.com/Nipale-ai/local-voxel-benchmark),
  [fable-5-1-one-prompt-game](https://github.com/Nipale-ai/fable-5-1-one-prompt-game),
  [glm-5-3-one-prompt-game](https://github.com/Nipale-ai/glm-5-3-one-prompt-game),
  [blocks-openworld](https://github.com/Nipale-ai/blocks-openworld),
  [galaxy](https://github.com/Nipale-ai/galaxy).

## Transparency

Measurements and comment drafts are produced by AI agents (Claude Code,
Devin) running on my hardware. Every number gets checked against the raw
receipts before it is posted — the receipts live in the repos above.

## Elsewhere

X: [@niklaslenz_ai](https://x.com/niklaslenz_ai)
