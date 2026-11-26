# Niklas Lenz

Wuppertal, Germany. Local AI on 832 GB of memory. I rank what runs best on the machine you own: LLMs, image, video.
Bringing the fire home.

Hardware: four NVIDIA GB10 systems of the DGX Spark class (two ASUS Ascent GX10, one Gigabyte AI TOP ATOM,
one Lenovo ThinkStation PGX; 128 GB each), one Mac Studio M5 Ultra (256 GB), one RTX 5090 (32 GB)
and two RTX 5060 Ti (16 GB each).

## What I do

Independent, reproducible measurements of public local-LLM recipes and models. Commands and results are public.
Fixes and findings go back to the recipe authors as issues and pull requests.

## Highlights

- **2 merged TensorFold PRs for the Qwen3.8-27B TP=2 plan** —
  [#3383](https://github.com/ashhart/TensorFold/pull/3383) (merged 2026-11-16) and
  [#3602](https://github.com/ashhart/TensorFold/pull/3602) (merged 2026-11-20).
  - Step 1 and the first part of step 2 of [#3325](https://github.com/ashhart/TensorFold/issues/3325) (issue still open): host-only rank plan and weight-cut plan, shard spans pinned in tests at TP=1, 2 and 4.
  - They move no token yet; `--tp 2` is still refused.
- **15.96 s → 3.14 s to the first token** of a 217K-token resume while another prompt prefills —
  [prompt-cache issue #81](https://github.com/MiaAI-Lab/Qwen3.8-Flash-Next-Single-DGX-Spark-TensorFold/issues/81) (closed as completed 2026-11-18).
  - My diagnosis on one GB10: the scheduler ranked a cached resume like a cold 220K prompt (A-B-B-A run).
  - The fix is upstream's (`882ca0a`, devopsfortunato); the recipe now pins TensorFold v1.2.7.
- **GPQA Diamond 58.1 % → 82.8 %** with thinking on and `--thinking-budget 4096` —
  [issue #3323](https://github.com/ashhart/TensorFold/issues/3323) (closed as completed), recipe note merged as
  [PR #3373](https://github.com/ashhart/TensorFold/pull/3373) (2026-11-19).
  - Qwen3.8-27B, TensorFold 1.2.7, MLX 4-bit, DFlash2 drafter, one GB10, 198 questions.
  - Without a budget 78 replies hit the 16,384-token limit; with 4096, none.
- **2,243 lines in 22 files** — [PR #3578](https://github.com/ashhart/TensorFold/pull/3578) (merged 2026-11-19):
  host-only family package for Inkling 2 Small (config, weight map checked against the release headers, layer plan, template and tokenizer checks).
  - Nothing is served yet. It is slice 1 of 6 in [issue #3476](https://github.com/ashhart/TensorFold/issues/3476) (open).
  - Follow-up [PR #4367](https://github.com/ashhart/TensorFold/pull/4367) is open.
- **36.35 tok/s** on [four GB10 systems in a ring, no switch](https://github.com/Nipale-ai/dgx-spark-4x-switchless-ring) —
  the full GLM-5.3 (753B), using vcruz305's recipe.
  - Mean of the recipe's 6 test prompts: 37.07 on his switch + NCCL and 41.42 on his switch + RoCE reduce, so the ring is 2 % and 12 % lower.
  - The setups are not identical; the repo lists the differences, the ring profile, a ring check and every step.
- **+10 to 12 % cold prefill on an M5 Ultra** — [TensorFold PR #1738](https://github.com/ashhart/TensorFold/pull/1738) (merged 2026-10-31):
  Qwen3.8-27B prompt chunks, 2k to 64k tokens, per the PR; replies are token-identical.
- **180.0 → 274.6 tok/s** code decode on one RTX 5090 —
  [PR #15](https://github.com/MiaAI-Lab/Qwen3.8-27B-16gb-NVIDIA-GPUs-one-click-install/pull/15) (merged 2026-10-09):
  opt-in `DRAFT=dflash2` (ExLlamaV3 1.6.0 + the DFlash2 drafter; credits to turboderp, z-lab and r0b0tlab, as in the PR) in MiaAI-Lab's Qwen3.8-27B one-click kit.
  - RigMark, median of 5; MMLU-200 80.0 → 79.5 %. The gain shrinks with context depth; see the PR.

## Other upstream work

- **Landed upstream:**
  - TensorFold [#610](https://github.com/ashhart/TensorFold/issues/610) (closed as completed): RTX 5090 receipt; the Linux x86_64 archive carries sm_120 kernels since 1.0.6, credited in the release notes.
  - TensorFold [#489](https://github.com/ashhart/TensorFold/pull/489) (2026-10-09, credited in v1.0.3): a streamed tool reply no longer sends whitespace that the whole reply does not have.
  - TensorFold [#3371](https://github.com/ashhart/TensorFold/pull/3371) (2026-11-20): Metal scheduling of replies that are still reasoning; the order changes, no token does.
  - Imagination Studio [#147](https://github.com/Keys-Wasserman/Imagination-Studio-by-keys-Wasserman/pull/147) and [#158](https://github.com/Keys-Wasserman/Imagination-Studio-by-keys-Wasserman/pull/158) (2026-10-26): opt-in video on a 32 GB RTX 5090.
  - ThinkingCap [#1](https://github.com/0xWhiteMage/thinkingcap-qwen3.8-27b-exl3-tandemllm/pull/1) (2026-10-19): independent RTX 5090 and DGX Spark receipts.
- **Findings that helped:**
  - TensorFold [#112](https://github.com/ashhart/TensorFold/issues/112) (closed as completed): my startup-budget trace helped the maintainer check why Qwen3.8-27B with the DFlash2 drafter was refused on an RTX 5090 (the fp32-versus-packed numbers came from jkuepker's PR #100).
  - Measurement for [PR #70](https://github.com/MiaAI-Lab/Qwen3.8-Flash-Next-Single-DGX-Spark/pull/70) (usmaneth's k=6 MTP guard): code decode +20 to 28 %, prose flat to slightly lower; the change landed on `main` through #72.
  - [Issue #53](https://github.com/MiaAI-Lab/Qwen3.8-Flash-Next-Single-DGX-Spark/issues/53) (open): tested the three open fixes for the first-start crash; all three work.
  - RTX 5090 recipe: [issue #4](https://github.com/MiaAI-Lab/Qwen3.8-27B-NVFP4-RTX-5090/issues/4) (measurement report, 104/118 tok/s single-stream) and the measured flashinfer RAM peak (80.2 GiB unbounded, 30.6 GiB with `MAX_JOBS=4`) in [issue #1](https://github.com/MiaAI-Lab/Qwen3.8-27B-NVFP4-RTX-5090/issues/1).
- **Open:**
  - Flash Next [PR #76](https://github.com/MiaAI-Lab/Qwen3.8-Flash-Next-Single-DGX-Spark/pull/76): keeps JSON arguments intact through the launcher's re-parse; seven launches on a GB10.
  - One-click kit PRs [#19](https://github.com/MiaAI-Lab/Qwen3.8-27B-16gb-NVIDIA-GPUs-one-click-install/pull/19), [#20](https://github.com/MiaAI-Lab/Qwen3.8-27B-16gb-NVIDIA-GPUs-one-click-install/pull/20) and [#21](https://github.com/MiaAI-Lab/Qwen3.8-27B-16gb-NVIDIA-GPUs-one-click-install/pull/21): DFlash2 on 16 GB cards, tensor parallel on two GPUs, parallel requests.
  - MTPLX [#715](https://github.com/youssofal/MTPLX/issues/715) (Inkling 2 Mini HTTP 500) and drama-tensorfold [#68](https://github.com/plotarmordev/drama-tensorfold/issues/68) (RTX 5060 Ti 16 GB check).

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

<!-- Upstream status checked live on 2026-11-26 (gh api). Update the status words when you change this file. -->
