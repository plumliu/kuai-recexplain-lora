# Kuai Recommendation Explanation LoRA

Lightweight LLM distillation and preference alignment for recommendation-scene explanation on KuaiRand-27K.

This repository is a **landing page** for the released adapter and project summary. It intentionally does not include raw data, teacher API outputs, training scripts, RQ-VAE weights, or full training logs.

## Model

- Base model: `Qwen/Qwen3.5-9B`
- Released artifact: LoRA adapter
- Recommended adapter: teacher-judged student-aware DPO checkpoint
- Hugging Face: `https://huggingface.co/plumliu/qwen35-9b-kuairand-recexplain-lora`

## What This Model Does

The adapter is tuned for recommendation explanation tasks, including:

- Summarizing a user's recent short-video interests.
- Explaining why a candidate item may match a user's behavior history.
- Reasoning over item metadata, user behavior sequences, and discrete Semantic ID tokens.

It is not intended as a general-purpose chat model.

## Method Overview

```text
KuaiRand-27K behavior logs
  -> high-frequency item universe
  -> item text standardization
  -> text embedding + behavior embedding
  -> hybrid item representation
  -> three-level Semantic ID
  -> teacher-enhanced SFT
  -> warm-start DPO
  -> teacher-judged student-aware DPO
```

See [docs/method.md](docs/method.md) for the compact method description.

## Results

Held-out evaluations show improvements over the SFT-only model:

| Metric | SFT | Final Aligned Adapter | Gain |
| --- | ---: | ---: | ---: |
| Candidate item grounding | `94.5%` | `97.5%` | `+3.0 pp` |
| Preference seq accuracy | `65.8%` | `~99.8%` | `+34.0 pp` |

See [docs/evaluation.md](docs/evaluation.md) for the evaluation summary.

## Why Only A Landing Repo?

The full training workflow depends on large KuaiRand artifacts, teacher API outputs, intermediate embeddings, LoRA checkpoints, and AutoDL run logs. Those artifacts are not redistributed here.

This repository keeps the public surface focused:

- Project motivation.
- High-level method.
- Evaluation results.
- Link to the Hugging Face adapter.

## Citation

If this project is useful, please cite the adapter repository and the KuaiRand dataset.
