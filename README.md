# Niklas Lenz

Wuppertal, Germany. I test local AI on my own hardware: one RTX 5090 (32 GB), two RTX 5060 Ti (16 GB each)
and four NVIDIA GB10 systems of the DGX Spark class (two ASUS Ascent GX10, one Gigabyte AI TOP ATOM,
one Lenovo ThinkStation PGX).

## What I do

Independent, reproducible measurements of public local-LLM recipes and models. Commands and results are public.
Fixes and findings go back to the recipe authors as issues and pull requests.

## Highlights

- **[Four GB10 systems in a ring, no switch](https://github.com/Nipale-ai/dgx-spark-4x-switchless-ring)** —
  the full GLM-5.3 (753B) on a four-cable ring, using vcruz305's recipe. Mean of the recipe's 6 test prompts:
  36.35 tok/s on the ring, against 37.07 (his switch + NCCL) and 41.42 (his switch + RoCE reduce), so 2 % and 12 % lower.
  The setups are not identical; the repo lists the differences, the ring profile, a ring check and every step.
- **[PR #15](https://github.com/MiaAI-Lab/Qwen3.8-27B-16gb-NVIDIA-GPUs-one-click-install/pull/15) (merged 2026-10-09)** —
  opt-in `DRAFT=dflash2` (ExLlamaV3 1.6.0 + the DFlash2 drafter; credits to turboderp, z-lab and r0b0tlab, as in the PR)
  for 32 GB cards in MiaAI-Lab's Qwen3.8-27B one-click kit. On one RTX 5090, code decode
  180.0 → 274.6 tok/s (RigMark, median of 5), MMLU-200 80.0 → 79.5 %. The gain shrinks with context depth; see the PR.
- **[TensorFold PR #489](https://github.com/ashhart/TensorFold/pull/489) (merged 2026-10-09)** —
  a streamed tool reply no longer sends whitespace that the whole reply does not have (chat, Messages and Responses routes).
  Credited in the TensorFold v1.0.3 release notes.
- **[TensorFold issue #112](https://github.com/ashhart/TensorFold/issues/112) (closed as completed)** —
  Qwen3.8-27B with the DFlash2 drafter was refused at startup on an RTX 5090. My trace of the startup budget helped the
  maintainer check the cause (drafter counted at fp32; the fp32-versus-packed numbers came from jkuepker's PR #100).
  The fix shipped in TensorFold 0.6.0, credited to jkuepker's ROCm work in the release notes.
- **[Measurement for PR #70](https://github.com/MiaAI-Lab/Qwen3.8-Flash-Next-Single-DGX-Spark/pull/70)** (usmaneth's k=6 MTP guard) —
  independent run on one GB10, k=6 + BF16 KV against main (k=3, FP8 KV): code decode +20–28 %, prose flat to slightly lower. The change landed on `main` through #72.

## Other upstream work

- [PR #76](https://github.com/MiaAI-Lab/Qwen3.8-Flash-Next-Single-DGX-Spark/pull/76) (open): keeps JSON arguments intact
  through the launcher's re-parse; seven launches on a GB10.
- [Issue #53](https://github.com/MiaAI-Lab/Qwen3.8-Flash-Next-Single-DGX-Spark/issues/53): tested the three open fixes for the
  first-start crash on a fresh install; all three work. The commit of #65 landed on `main` through #72.
- RTX 5090 recipe: [issue #4](https://github.com/MiaAI-Lab/Qwen3.8-27B-NVFP4-RTX-5090/issues/4) is a measurement report
  (104/118 tok/s single-stream, scaling to 8 streams); [issue #1](https://github.com/MiaAI-Lab/Qwen3.8-27B-NVFP4-RTX-5090/issues/1)
  has the measured RAM peak of the flashinfer build (80.2 GiB unbounded, 30.6 GiB with `MAX_JOBS=4`).

## Repos

- **[local-llm-field-reports](https://github.com/Nipale-ai/local-llm-field-reports)** —
  reports with raw data behind my measurements.
- **[local-ai-10-apps](https://nipale-ai.github.io/local-ai-10-apps/)** —
  the same 10 app tasks for every local setup. The AI builds each app alone, an automatic checker clicks through it.
- **[qwen-image-21-turbo-compare](https://nipale-ai.github.io/qwen-image-21-turbo-compare/)** —
  Qwen-Image-2.1 Turbo vs base on one RTX 5090, with a slider.
- One-prompt builds: [local-voxel-benchmark](https://github.com/Nipale-ai/local-voxel-benchmark) (three local LLMs on two DGX Sparks).
  Other one-prompt builds: [opus-5-5-overnight-builds](https://github.com/Nipale-ai/opus-5-5-overnight-builds),
  [blocks-openworld](https://github.com/Nipale-ai/blocks-openworld),
  [fable-5-1-one-prompt-game](https://github.com/Nipale-ai/fable-5-1-one-prompt-game),
  [glm-5-3-one-prompt-game](https://github.com/Nipale-ai/glm-5-3-one-prompt-game).

## Transparency

Measurements, fixes and comment drafts are produced by AI agents (Claude Code, Devin) running on my hardware.
Numbers are checked against the raw output before I post them. Raw data for the field reports is in
local-llm-field-reports and the linked issues. The ring repo and PR #15 give the per-prompt tables and the exact
commands; their raw logs are not published.

## Elsewhere

X: [@niklaslenz_ai](https://x.com/niklaslenz_ai)

<!-- Upstream status checked live on 2026-10-10 (gh api). Update the status words when you change this file. -->
