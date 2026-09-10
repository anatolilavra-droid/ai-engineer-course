# How to Calibrate Your LLM Judge With Human Annotations - Galileo

- URL: https://galileo.ai/blog/calibrate-llm-judge-human-annotations
- Type: blog
- Published: unknown
- Topic: evals

Describes calibrating an LLM-as-judge system by computing Cohen's kappa between judge scores and a labeled human sample before shipping a new rubric, and re-sampling on a recurring schedule (e.g., monthly) to catch judge drift.
Recommends a scoring workflow where subject-matter experts score examples with the judge's verdict hidden, using a rubric that exactly matches the judge's criteria, and notes stratified sampling can reduce the volume of LLM judgments requiring human validation.
