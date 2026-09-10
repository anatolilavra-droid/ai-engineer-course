# How to Build Cross-Encoder Re-Ranking

- URL: https://oneuptime.com/blog/post/2026-01-30-cross-encoder-reranking/view
- Type: blog
- Published: 2026-01-30
- Topic: rag

Explains cross-encoder rerankers as transformer models that take a concatenated query-document pair as input and output a relevance score, contrasting them with bi-encoders that embed queries and documents independently. Describes the two-stage retrieval pipeline pattern: a first-stage retriever returns top-K candidates (e.g., K=100), and a cross-encoder reranks every query-document pair for the final ordering.
