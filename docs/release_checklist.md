# Release Checklist

## Hugging Face Adapter

- [ ] Copy LoRA release files into a clean model repository.
- [ ] Update `adapter_config.json`:
  - `base_model_name_or_path`: `Qwen/Qwen3.5-9B`
- [ ] Replace placeholder namespace in the model card.
- [ ] Upload:
  - `adapter_config.json`
  - `adapter_model.safetensors`
  - `tokenizer.json`
  - `tokenizer_config.json`
  - `chat_template.jinja`
  - `README.md`
- [ ] Verify loading with `AutoTokenizer`, `AutoModelForCausalLM`, and `PeftModel`.
- [ ] Run one small recommendation-explanation prompt before making the repo public.

## GitHub Landing Repo

- [x] Replace the Hugging Face TODO link in `README.md`.
- [ ] Add badges only after the Hugging Face repo is public.
- [ ] Do not commit model weights, training data, teacher outputs, logs, or intermediate artifacts.
- [ ] Keep technical details high-level; reserve implementation details for interviews or future paper-style documentation.
