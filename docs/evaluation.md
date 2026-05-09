# Evaluation Summary

The project uses two complementary evaluation routes.

## Generation Quality Evaluation

This route evaluates free-form recommendation explanations on held-out prompts.

| Model | Format Valid | Leak Rate | Candidate Grounding | History Relevance | Generic Rate | Mean Chars |
| --- | ---: | ---: | ---: | ---: | ---: | ---: |
| SFT final | `1.000` | `0.000` | `0.945` | `1.000` | `0.000` | `130.68` |
| Warm-start DPO | `1.000` | `0.000` | `0.970` | `1.000` | `0.000` | `133.13` |
| Student-aware DPO | `1.000` | `0.000` | `0.975` | `1.000` | `0.000` | `140.87` |

Main takeaway: candidate item grounding reaches `97.5%`, a `+3.0` percentage-point improvement over SFT.

## Preference Ranking Evaluation

This route evaluates whether the model assigns higher log probability to the preferred response in held-out chosen/rejected pairs.

| Model | Seq Accuracy | Mean-token Accuracy | Seq Margin | Token Margin |
| --- | ---: | ---: | ---: | ---: |
| SFT final | `0.658` | `0.850` | `6.188` | `0.4035` |
| Warm-start DPO | `0.999` | `0.998` | `66.976` | `2.3758` |
| Student-aware DPO | `0.998` | `0.999` | `67.770` | `2.4336` |

Main takeaway: preference seq accuracy reaches about `99.8%`, a roughly `+34.0` percentage-point improvement over SFT.

## Interpretation

Warm-start DPO learns a strong teacher preference boundary. Student-aware DPO preserves that boundary while improving free-generation grounding and reducing student-specific failure modes such as formatting drift and internal Semantic ID leakage.

