# Kuai Recommendation Explanation LoRA

Lightweight LLM distillation and preference alignment for recommendation-scene explanation on KuaiRand-27K.

This repository is a **landing page** for the released adapter, derived post-training dataset, and project summary.

## Repository Layout

- GitHub repository: project overview, method notes, examples, and evaluation summary.
- Hugging Face model repository: released LoRA adapter, tokenizer files, and model card.
- Hugging Face dataset repository: final derived SFT / DPO post-training JSONL files and compact evaluation summaries.
- Hugging Face RQ-VAE repository: Semantic ID RQ-VAE checkpoint and compact health-check summaries.
- Not distributed: KuaiRand raw logs, teacher raw API outputs, candidate generation caches, full judge logs, or full training artifacts.

## Model

- Base model: `Qwen/Qwen3.5-9B`
- Released artifact: LoRA adapter
- Recommended adapter: teacher-judged student-aware DPO checkpoint-600
- Hugging Face: [plumliu/qwen35-9b-kuairand-recexplain-lora](https://huggingface.co/plumliu/qwen35-9b-kuairand-recexplain-lora)

## Dataset

- Released artifact: derived SFT / DPO post-training data
- Contents: SFT train/eval, warm-start DPO train/eval, student-aware DPO train/eval, selected student-aware pairs, Semantic ID assets, and compact evaluation summaries
- Hugging Face: [plumliu/kuairand-recexplain-sft-dpo-data](https://huggingface.co/datasets/plumliu/kuairand-recexplain-sft-dpo-data)

## Semantic ID RQ-VAE

- Released artifact: three-level RQ-VAE checkpoint for KuaiRand-27K item Semantic ID construction
- Related data: generated SID mapping, hybrid embeddings, and rewritten user sequences are in the dataset repository
- Hugging Face: [plumliu/kuairand-semantic-id-rqvae](https://huggingface.co/plumliu/kuairand-semantic-id-rqvae)

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

## Examples

The [examples](examples) directory contains two small public KuaiRand-27K item records selected from the high-frequency item universe, plus short SFT-style and long DPO-style prompt/output illustrations. These examples are meant to show input shape and response style only; they are not released training records, teacher judge outputs, or evaluation samples.

## Why Only A Landing Repo?

The full training workflow depends on large KuaiRand artifacts, teacher API outputs, intermediate embeddings, LoRA checkpoints, and AutoDL run logs. The GitHub repository intentionally stays small and navigates to the Hugging Face artifacts instead of storing large files directly.

This repository keeps the public surface focused:

- Project motivation.
- High-level method.
- Evaluation results.
- Links to the Hugging Face adapter, derived dataset, and RQ-VAE checkpoint.

## Citation

If this project is useful, please cite the adapter repository, dataset repository, and the KuaiRand dataset.
