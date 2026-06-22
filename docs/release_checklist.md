# Release Checklist

## Hugging Face Adapter

- [x] Copy LoRA release files into a clean model repository.
- [x] Update `adapter_config.json`:
  - `base_model_name_or_path`: `Qwen/Qwen3.5-9B`
- [x] Replace placeholder namespace in the model card.
- [x] Upload:
  - `adapter_config.json`
  - `adapter_model.safetensors`
  - `tokenizer.json`
  - `tokenizer_config.json`
  - `chat_template.jinja`
  - `README.md`
- [x] Verify uploaded adapter hash matches student-aware checkpoint-600.

## Hugging Face Dataset

- [x] Create [`plumliu/kuairand-recexplain-sft-dpo-data`](https://huggingface.co/datasets/plumliu/kuairand-recexplain-sft-dpo-data).
- [x] Upload final SFT train/eval JSONL.
- [x] Upload warm-start DPO train/eval JSONL.
- [x] Upload student-aware DPO train/eval and selected pairs JSONL.
- [x] Upload compact evaluation summaries and manifest.
- [x] Exclude raw KuaiRand logs, teacher raw API outputs, candidate caches, full judge logs, model weights, and RQ-VAE weights.

## GitHub Landing Repo

- [x] Replace the Hugging Face TODO link in `README.md`.
- [x] Add the Hugging Face dataset link in `README.md`.
- [ ] Add badges only after the Hugging Face repo is public.
- [ ] Do not commit model weights, large training data, teacher outputs, logs, or intermediate artifacts.
- [ ] Keep technical details high-level; reserve implementation details for interviews or future paper-style documentation.
