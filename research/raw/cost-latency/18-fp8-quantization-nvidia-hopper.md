# LLM Inference Optimization: Quantization, Speculative Decoding, and Beyond

- URL: https://callsphere.ai/blog/llm-inference-optimization-quantization-speculative-decoding-2026
- Type: blog
- Published: 2026
- Topic: cost-latency

Discusses FP8 as a stable quantization format on NVIDIA Hopper GPUs with native Transformer Engine support, citing near-lossless quality (0.1-0.3% perplexity increase) and 33% faster inference versus FP16. Also covers combining continuous batching with quantized models to serve substantially more requests per GPU than a naive implementation.
