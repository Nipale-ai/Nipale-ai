# Niklas Lenz

Wuppertal, Germany. I build and measure local AI on my own hardware — a small
lab of 3× NVIDIA DGX Spark (GB10) and an RTX 5090.

## What I do

Independent, reproducible measurements of public local-LLM recipes — mostly
for [MiaAI-Lab](https://github.com/MiaAI-Lab). AI agents working for me run the benchmarks, the
raw data is kept, and the numbers go back upstream where they help close issues or
confirm PRs.

## Highlights

- My first own PR upstream: [#76](https://github.com/MiaAI-Lab/Qwen3.8-Flash-Next-Single-DGX-Spark/pull/76)
  — keeps JSON args intact in the launcher, tested with seven launches on a DGX Spark.
- Independent measurement for [PR #70](https://github.com/MiaAI-Lab/Qwen3.8-Flash-Next-Single-DGX-Spark/pull/70)
  (k=6 MTP guard): +20–28 % code confirmed — the PR merged into `main` via #72.
- Tested all three crash-fix PRs in
  [issue #53](https://github.com/MiaAI-Lab/Qwen3.8-Flash-Next-Single-DGX-Spark/issues/53)
  on a fresh install; the winning fix also landed.
- Full measurement report for the RTX-5090 recipe:
  [issue #4](https://github.com/MiaAI-Lab/Qwen3.8-27B-NVFP4-RTX-5090/issues/4)
  — incl. the explanation for the build-time OOM in #1.
- **[local-llm-field-reports](https://github.com/Nipale-ai/local-llm-field-reports)** —
  the reports and raw data behind those comments.
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

X: [@niklaslenz_ai](https://x.com/niklaslenz_ai) · Web: [niklaslenz.de](https://niklaslenz.de)
