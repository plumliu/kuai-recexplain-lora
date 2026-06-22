# Method

## Goal

The goal is to adapt a lightweight LLM to recommendation-scene explanation. Given a user's behavior history and a candidate short video, the model should produce grounded, concise, and preference-aware explanations.

## Semantic ID Representation

Each item is represented using both content and behavior information:

- Qwen3-Embedding-8B encodes standardized item text and category metadata.
- SASRec learns item behavior embeddings from user interaction sequences.
- Text and behavior embeddings are fused into a hybrid item representation.
- A three-level RQ-VAE discretizes the hybrid representation into Semantic ID tokens.

Example:

```text
<SID_0_42> <SID_1_187> <SID_2_91>
```

These tokens provide a compact structure signal for user interest histories and candidate item reasoning.

## Alignment Recipe

The adapter is trained in three stages:

1. **Teacher-enhanced SFT**: supervised recommendation explanation data generated with a teacher LLM.
2. **Warm-start DPO**: preference pairs covering hard, medium, and random negatives teach an initial preference boundary.
3. **Teacher-judged student-aware DPO**: the warm-start student samples multiple responses for the same prompt; a teacher scores and filters real student failures into high-confidence chosen/rejected pairs.

The student-aware stage is the key alignment step because it targets errors the student model actually makes, rather than only teacher-constructed obvious negatives.

## Released Artifacts

The public model artifact is a LoRA adapter for `Qwen/Qwen3.5-9B`, hosted at [`plumliu/qwen35-9b-kuairand-recexplain-lora`](https://huggingface.co/plumliu/qwen35-9b-kuairand-recexplain-lora). The released adapter corresponds to the teacher-judged student-aware DPO checkpoint-600.

The public dataset artifact is hosted at [`plumliu/kuairand-recexplain-sft-dpo-data`](https://huggingface.co/datasets/plumliu/kuairand-recexplain-sft-dpo-data). It contains the final derived SFT / DPO post-training JSONL files and compact evaluation summaries.

The release still does not publish:

- Raw KuaiRand data.
- Teacher API request/response logs.
- Student candidate generation caches.
- Full teacher judge logs.
- RQ-VAE checkpoint or item-level Semantic ID mapping.
- Full training scripts or AutoDL logs.
