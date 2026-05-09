---
base_model: Qwen/Qwen3.5-9B
library_name: peft
license: apache-2.0
tags:
  - recommendation
  - lora
  - sft
  - dpo
  - preference-optimization
  - semantic-id
language:
  - zh
  - en
---

# Qwen3.5-9B KuaiRand Recommendation Explanation LoRA

This is a LoRA adapter for `Qwen/Qwen3.5-9B`, tuned for recommendation-scene explanation and preference-aware item reasoning on KuaiRand-27K-style prompts.

## Intended Use

The adapter is intended for research and demonstration in:

- User interest summarization.
- Candidate item recommendation explanation.
- Preference-aware reasoning over user histories, item metadata, and Semantic ID tokens.

It is not intended as a general-purpose assistant.

## Training Summary

The adapter was trained with:

- Teacher-enhanced SFT.
- Warm-start DPO over hard/medium/random negative preference pairs.
- Teacher-judged student-aware DPO over sampled student responses.

The final released adapter corresponds to the student-aware DPO model selected by held-out generation and preference-ranking evaluation.

## Evaluation

| Metric | SFT | Released Adapter | Gain |
| --- | ---: | ---: | ---: |
| Candidate item grounding | `94.5%` | `97.5%` | `+3.0 pp` |
| Preference seq accuracy | `65.8%` | `~99.8%` | `+34.0 pp` |

## Loading Example

```python
from peft import PeftModel
from transformers import AutoModelForCausalLM, AutoTokenizer

base_model = "Qwen/Qwen3.5-9B"
adapter = "plumliu/qwen35-9b-kuairand-recexplain-lora"

tokenizer = AutoTokenizer.from_pretrained(adapter, trust_remote_code=True)
model = AutoModelForCausalLM.from_pretrained(
    base_model,
    torch_dtype="auto",
    device_map="auto",
    trust_remote_code=True,
)
model = PeftModel.from_pretrained(model, adapter)
```

## Limitations

- The adapter is domain-specific and optimized for recommendation explanation prompts.
- It does not include raw training data, teacher API outputs, or item-level Semantic ID mappings.
- Output quality depends on prompt format and the availability of grounded item/user context.
