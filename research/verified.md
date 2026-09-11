# Verified Research Sources — AI Engineer Course

Every link collected in `research/raw/` was checked by actually calling WebFetch on it — nothing here (or in "Не проверено") was kept based on the title or the two-line description already sitting in the raw file. Hard rule: only what genuinely loaded gets a verdict.

**Result of the automated pass:** this session's network egress policy allows outbound traffic only to GitHub-related hosts (`github.com`, `raw.githubusercontent.com`) and a couple of official blog subdomains that happened to be allow-listed (`blog.modelcontextprotocol.io`, `www.microsoft.com`). Every other domain — arxiv.org, medium.com, redis.io, even control domains like `google.com` and `en.wikipedia.org` — was rejected at the proxy with `403 organization policy`, confirmed independently by multiple verification runs and by raw `curl` against the proxy. This is an infrastructure restriction of the session, not a judgment on the sources' quality. Of 183 links, only 7 could actually be opened by WebFetch in this session, and all 7 passed.

**Manual follow-up pass (11.09.2026):** the user independently opened and read 5 more sources from outside this session's network restriction (embeddings, prompt engineering ×2, evals, prompt injection) and confirmed all 5 as genuine, concrete, first-party or canonical material — added below with the same citation format. Total verified now: **12 of 183**. See `research/urls-to-verify.md` for the triage of the remaining 171 (40 flagged worth opening next, ~76-78 filtered out by source genre without being opened — exact count has a small unreconciled gap noted there, ~53 still fully unsorted across topics this pass didn't touch).

Rejection criteria applied per-source, when a fetch/manual open did succeed: broken/dead link, redirect to a generic homepage, paywall, a page that's mainly a funnel toward a paid course, an unexplained "top-10" listicle, text with no code example and no concrete specifics, or a GitHub repo with no commits in the last 12 months. These were applied to the 12 sources that actually loaded (7 via WebFetch on 2026-09-10, 5 manually on 2026-09-11); the rest could not be evaluated against them at all and are listed as "Не проверено" with the fetch failure as the reason.

**Quality legend:** A = primary source (official docs/blog from the vendor, the original paper, the tool's own repo) · B = useful with caveats (solid secondary source) · C = overview only (passed the bar but doesn't go deep).

---

## Основы LLM и токенизация

### Verified

#### GitHub - openai/tiktoken: a fast BPE tokeniser for use with OpenAI's models
- URL: https://github.com/openai/tiktoken
- Quality: A
- Level: intermediate
- Price: free
- Time: ~20 min to read README + try examples
- Verified: 2026-09-10
- Note: Confirmed live official OpenAI repo (19.2k stars, 79 commits on main, most recent commit "Release 0.14.0 (#597)" on 2026-08-17 — well within 12 months). README gives concrete API usage (`encoding_for_model`, `get_encoding`, cl100k_base/o200k_base), benchmark claims (3-6x faster than comparable tokenizers), and code examples — passes all filters.

### Не проверено

- What is Tokenization in LLMs? BPE, SentencePiece, tiktoken in 2026 — https://futureagi.com/blog/what-is-tokenization-llms-2026/ — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Inside the LLM Word Factory — https://arxiv.org/pdf/2606.08562 — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Parity-Aware Byte-Pair Encoding: Improving Cross-lingual Fairness in Tokenization — https://arxiv.org/abs/2508.04796 — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Byte-Pair Encoding tokenization · Hugging Face LLM Course — https://huggingface.co/learn/llm-course/en/chapter6/5 — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Tokenization and byte pair encoding — https://sebastianraschka.com/faq/docs/tokenization-bpe.html — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- LLM Concepts Explained 2026 | Attention, RLHF, MoE, KV Cache — https://www.buildfastwithai.com/blogs/collection/llm-concepts — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- LLM Fundamentals — Tokens, Attention & Transformers (2026) — https://myengineeringpath.dev/genai-engineer/llm-fundamentals/ — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- A Beginner's Reading List for Large Language Models for 2026 — https://machinelearningmastery.com/a-beginners-reading-list-for-large-language-models-for-2026/ — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Transformer Explainer: Learning LLM Transformers with Interactive Visual Explanation and Experimentation — https://research.ibm.com/publications/transformer-explainer-learning-llm-transformers-with-interactive-visual-explanation-and-experimentation — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Transformer Architectures in 2026: Foundations, Code, and Practical Resources — https://medium.com/@angelosorte1/transformer-architectures-in-2026-foundations-code-and-practical-resources-88022b521369 — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Context Window Optimization: 6 LLM Strategies for 2026 — https://neuraltrust.ai/blog/context-window-optimization — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- LLM Context Window Comparison (2026): 20 Models From 200K to 10M Tokens, Priced per Full Window — https://www.morphllm.com/llm-context-window-comparison — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- How do temperature, top-k, and top-p sampling differ? — https://sebastianraschka.com/faq/docs/temperature-topk-topp-sampling.html — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- LLM Sampling Parameters Explained: Intuition to Math — https://letsdatascience.com/blog/llm-sampling-temperature-top-k-top-p-and-min-p-explained — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Tokenizer Quirks: Claude, GPT, and Gemini Don't Count the Same Text the Same Way — https://dev.to/gabrielanhaia/tokenizer-quirks-claude-gpt-and-gemini-dont-count-the-same-text-the-same-way-1522 — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Let's build the GPT Tokenizer (Andrej Karpathy) — https://x.com/karpathy/status/1759996549109776702 — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- What Is KV Cache in LLMs? A 2026 Guide — https://www.buildfastwithai.com/blogs/kv-cache-llms-explained — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- AI 101: Your Ultimate Guide to Attention: Mechanism, QKV, and KV Cache — https://www.turingpost.com/p/your-ultimate-guide-to-attention-mechanism-qkv-and-kv-cache — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- 12 Free Courses to Master Large Language Models in 2026 — https://www.turingpost.com/p/llms-courses — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
## Эмбеддинги и векторный поиск

### Verified

#### Hierarchical Navigable Small Worlds (HNSW) — Pinecone
- URL: https://www.pinecone.io/learn/series/faiss/hnsw/
- Quality: A
- Level: intermediate
- Price: free
- Time: ~2-3 hours with working through the code
- Verified: 2026-09-11 (manual check)
- Note: Устройство HNSW от skip-list и NSW-графов до слоёной структуры; реализация на Faiss с реальными параметрами (M, efConstruction, efSearch); замеры recall/времени поиска/памяти на Sift1M; ссылки на оригинальные работы Малкова; есть рабочий ноутбук на GitHub. Часть серии "Faiss: The Missing Manual" (см. `research/raw/embeddings-vector-search/16-faiss-missing-manual-series.md` для остальных глав — LSH, product quantization, композитные индексы — не открывались отдельно, но та же серия/качество).

### Не проверено

- The Best Open-Source Embedding Models in 2026 — https://www.bentoml.com/blog/a-guide-to-open-source-embedding-models — Reason: fetch failed: EGRESS_BLOCKED (network egress proxy in this environment blocked all access to this domain; page content could not be inspected)
- How to Choose the Best Embedding Model for RAG in 2026: 10 Models Benchmarked — https://milvusio.medium.com/how-to-choose-the-best-embedding-model-for-rag-in-2026-10-models-benchmarked-4efc9508a193 — Reason: fetch failed: EGRESS_BLOCKED (network egress proxy in this environment blocked all access to this domain; page content could not be inspected)
- Comparing the best open source vector databases (2026) — https://redis.io/blog/best-open-source-vector-databases-comparison/ — Reason: fetch failed: EGRESS_BLOCKED (network egress proxy in this environment blocked all access to this domain; page content could not be inspected)
- Hybrid Search Guide: Vectors & Full-Text (April 2026) — https://supermemory.ai/blog/hybrid-search-guide/ — Reason: fetch failed: EGRESS_BLOCKED (network egress proxy in this environment blocked all access to this domain; page content could not be inspected)
- Hybrid Search in Production: Why BM25 Still Wins on the Queries That Matter — https://tianpan.co/blog/2026-04-12-hybrid-search-production-bm25-dense-embeddings — Reason: fetch failed: EGRESS_BLOCKED (network egress proxy in this environment blocked all access to this domain; page content could not be inspected)
- RAG Chunking Strategies 2026: 8 Methods Compared with Code Examples — https://denser.ai/blog/rag-chunking-strategies/ — Reason: fetch failed: EGRESS_BLOCKED (network egress proxy in this environment blocked all access to this domain; page content could not be inspected)
- RAG Chunking Strategies: The 2026 Benchmark Guide — https://www.premai.io/blog/rag-chunking-strategies-the-2026-benchmark-guide/ — Reason: fetch failed: EGRESS_BLOCKED (network egress proxy in this environment blocked all access to this domain; page content could not be inspected)
- MTEB Leaderboard 2026: Best Embedding Models for RAG — https://www.codesota.com/benchmarks/mteb — Reason: fetch failed: EGRESS_BLOCKED (network egress proxy in this environment blocked all access to this domain; page content could not be inspected)
- Embedding Fine-Tuning for RAG: Synthetic Data Guide — https://www.llamaindex.ai/blog/fine-tuning-embeddings-for-rag-with-synthetic-data-e534409a3971 — Reason: fetch failed: EGRESS_BLOCKED (network egress proxy in this environment blocked all access to this domain; page content could not be inspected)
- Product Quantization: Compressing high-dimensional vectors by 97% — https://www.pinecone.io/learn/series/faiss/product-quantization/ — Reason: fetch failed: EGRESS_BLOCKED (network egress proxy in this environment blocked all access to this domain; page content could not be inspected)
- Scaling Vector Search to 1 Billion on PostgreSQL — https://blog.vectorchord.ai/scaling-vector-search-to-1-billion-on-postgresql — Reason: fetch failed: EGRESS_BLOCKED (network egress proxy in this environment blocked all access to this domain; page content could not be inspected)
- Matryoshka Vector Embeddings: Flexible Embeddings for Cost-Efficient AI Systems — https://vast.ai/article/matryoshka-vector-embeddings — Reason: fetch failed: EGRESS_BLOCKED (network egress proxy in this environment blocked all access to this domain; page content could not be inspected)
- Best Multimodal Embedding Models in 2026 - Tested & Ranked — https://mixpeek.com/curated-lists/best-multimodal-embedding-models — Reason: fetch failed: EGRESS_BLOCKED (network egress proxy in this environment blocked all access to this domain; page content could not be inspected)
- Top Reranking Models to Boost RAG Accuracy in 2026 — https://redis.io/blog/top-reranking-models-rag-accuracy/ — Reason: fetch failed: EGRESS_BLOCKED (network egress proxy in this environment blocked all access to this domain; page content could not be inspected)
## RAG

### Verified

### Не проверено

- RAG Architectures Every AI Developer Must Know in 2026: A Complete Guide with Examples — https://medium.com/@angelosorte1/rag-architectures-every-ai-developer-must-know-in-2026-a-complete-guide-with-examples-ea59471aeb01 — Reason: fetch failed: EGRESS_BLOCKED — medium.com is blocked by this session's network egress proxy; WebFetch never received page content.
- 20 Advanced RAG Types to Know in 2026 — https://www.turingpost.com/p/ragtypes — Reason: fetch failed: EGRESS_BLOCKED — turingpost.com is blocked by this session's network egress proxy.
- RAG in 2026: Architecture Shifts, Emerging Patterns, and What It Means for Java Developers — https://medium.com/@elammarisoufiane/rag-in-2026-architecture-shifts-emerging-patterns-and-what-it-means-for-java-developers-6f2803e39787 — Reason: fetch failed: EGRESS_BLOCKED — medium.com is blocked by this session's network egress proxy.
- Engineering the RAG Stack: A Comprehensive Review of the Architecture and Trust Frameworks for Retrieval-Augmented Generation Systems — https://arxiv.org/pdf/2601.05264 — Reason: fetch failed: EGRESS_BLOCKED — arxiv.org is blocked by this session's network egress proxy.
- 9 advanced RAG techniques to know & how to implement them [2026] — https://www.meilisearch.com/blog/rag-techniques — Reason: fetch failed: EGRESS_BLOCKED — meilisearch.com is blocked by this session's network egress proxy.
- What is Agentic RAG? Everything You Need to Know in 2026 — https://www.lyzr.ai/blog/agentic-rag/ — Reason: fetch failed: EGRESS_BLOCKED — lyzr.ai is blocked by this session's network egress proxy.
- Agentic RAG in 2026: Patterns, Code, Observability — https://futureagi.com/blog/agentic-rag-systems-2025/ — Reason: fetch failed: EGRESS_BLOCKED — futureagi.com is blocked by this session's network egress proxy.
- What is GraphRAG? - Neo4j Graph Intelligence Platform — https://neo4j.com/blog/genai/what-is-graphrag/ — Reason: fetch failed: EGRESS_BLOCKED — neo4j.com is blocked by this session's network egress proxy.
- GraphRAG Architecture: Components, Workflow & Implementation Guide — https://www.puppygraph.com/blog/graphrag-architecture — Reason: fetch failed: EGRESS_BLOCKED — puppygraph.com is blocked by this session's network egress proxy.
- RAG Evaluation Metrics in 2026: Faithfulness & More — https://futureagi.com/blog/rag-evaluation-metrics-2025/ — Reason: fetch failed: EGRESS_BLOCKED — futureagi.com is blocked by this session's network egress proxy.
- RAG Evaluation: Metrics, Tools, and the Context Gap (2026) — https://atlan.com/know/how-to-evaluate-rag-systems-explained/ — Reason: fetch failed: EGRESS_BLOCKED — atlan.com is blocked by this session's network egress proxy.
- RAG at Scale: How to Build Production AI Systems in 2026 — https://redis.io/blog/rag-at-scale/ — Reason: fetch failed: EGRESS_BLOCKED — redis.io is blocked by this session's network egress proxy.
- How to Build Cross-Encoder Re-Ranking — https://oneuptime.com/blog/post/2026-01-30-cross-encoder-reranking/view — Reason: fetch failed: EGRESS_BLOCKED — oneuptime.com is blocked by this session's network egress proxy.
- RAG vs. long-context LLMs: A side-by-side comparison — https://www.meilisearch.com/blog/rag-vs-long-context-llms — Reason: fetch failed: EGRESS_BLOCKED — meilisearch.com is blocked by this session's network egress proxy.
- RAG failure modes: common pitfalls and solutions — https://snorkel.ai/blog/retrieval-augmented-generation-rag-failure-modes-and-how-to-fix-them/ — Reason: fetch failed: EGRESS_BLOCKED — snorkel.ai is blocked by this session's network egress proxy.
- Hybrid Search for RAG: Combining BM25 and Dense Vector Search (2026 Guide) — https://denser.ai/blog/hybrid-search-for-rag/ — Reason: fetch failed: EGRESS_BLOCKED — denser.ai is blocked by this session's network egress proxy.
## Evals

### Verified

#### Evaluation concepts — LangSmith / LangChain docs
- URL: https://docs.langchain.com/langsmith/evaluation-concepts
- Quality: A
- Level: intermediate
- Price: free (documentation; the LangSmith product itself is paid)
- Time: ~1.5-2 hours
- Verified: 2026-09-11 (manual check)
- Note: Разделение offline (до деплоя, на датасетах с эталонными ответами) и online (на живом трафике, без эталонов); типы оценщиков — человек, код, LLM-as-judge, попарное сравнение; reference-free vs reference-based и где каждый применим; как строить датасеты (10-20 ручных примеров → исторические трейсы → синтетика); различие оценки и тестирования. Концептуальный костяк модуля evals, применим и без самого продукта LangSmith.

### Не проверено

- Top 9 LLM Evaluation Tools in 2026 - Confident AI — https://www.confident-ai.com/knowledge-base/compare/best-llm-evaluation-tools — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- The Complete Guide for LLM Evaluations in 2026 - Galtea Blog — https://galtea.ai/blog/llm-evaluation-complete-guide — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- LLM-as-a-Judge in 2026: Top Evaluation Techniques and Best Practices - DeepEval — https://deepeval.com/blog/llm-as-a-judge — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- LLM-as-a-Judge: A Complete Guide to Using LLMs for Evaluations - Evidently AI — https://www.evidentlyai.com/llm-guide/llm-as-a-judge — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Top 5 LLM Evaluation Frameworks in 2026, Compared - DeepEval — https://deepeval.com/blog/top-5-llm-evaluation-frameworks — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Top 5 Agent Evaluation Tools in 2026 - MLflow — https://mlflow.org/top-5-agent-evaluation-frameworks/ — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- AI Benchmarks 2026: Top Evaluations and Their Limits - Kili Technology — https://kili-technology.com/blog/ai-benchmarks-guide-the-top-evaluations-in-2026-and-why-theyre-not-enough — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- AI Agent Benchmarks: The 2026 Enterprise Evaluation Guide - Automation Anywhere — https://www.automationanywhere.com/company/blog/ai-agent-benchmarks — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Prompt Regression Testing: Preventing Quality Decay - Statsig — https://www.statsig.com/perspectives/slug-prompt-regression-testing — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Building Agent & LLM Evaluation Datasets - MLflow AI Platform Docs — https://mlflow.org/docs/latest/genai/datasets/ — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- LLM Evaluation: Methods, Metrics, RAG & Agent Evals Guide - Arize — https://arize.com/llm-evaluation/ — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- RAG Evaluation: Complete Guide 2026 - SuperAnnotate — https://www.superannotate.com/blog/rag-evaluation — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- How to Calibrate Your LLM Judge With Human Annotations - Galileo — https://galileo.ai/blog/calibrate-llm-judge-human-annotations — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Illusions of the Gold Standard: A Large-scale Analysis of Human Evaluation Protocols for Long-form Text Generation — https://arxiv.org/pdf/2606.07936 — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Best AI Eval Tools for CI/CD Pipelines (2026 Review) - Braintrust — https://www.braintrust.dev/articles/best-ai-evals-tools-cicd-2025 — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Online vs Offline AI Evals: When to Use Each - Inngest Blog — https://www.inngest.com/blog/online-vs-offline-ai-evals-when-to-use-each — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Your CI/CD Pipeline Is Your Last Line of Defence for LLM Quality — https://medium.com/@srinib100/your-ci-cd-pipeline-is-your-last-line-of-defence-for-llm-quality-3fef6a86208b — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
## Проектирование промптов

### Verified

#### Prompt engineering best practices for 2026 | Claude by Anthropic
- URL: https://claude.com/blog/best-practices-for-prompt-engineering
- Quality: A
- Level: beginner → intermediate
- Price: free
- Time: ~1 hour
- Verified: 2026-09-11 (manual check)
- Published: 2025-11-10
- Note: Базовые техники (явность, контекст, конкретность, примеры, разрешение на "не знаю"), продвинутые (prefill, три вида chain-of-thought, контроль формата, prompt chaining), и раздел про устаревшие техники — XML-теги и role prompting уже не обязательны. Таблица "что нужно → какая техника" и список типичных ошибок. Показывает сдвиг индустрии от prompt engineering к context engineering.

#### Few-Shot Prompting — Prompt Engineering Guide (DAIR.AI)
- URL: https://www.promptingguide.ai/techniques/fewshot
- Quality: A
- Level: beginner
- Price: free (материал; курсы на сайте платные)
- Time: ~30 min на страницу, весь раздел техник — 6-8 часов
- Verified: 2026-09-11 (manual check)
- Note: Few-shot с примерами из Brown et al. 2020, выводы Min et al. 2022 (важен формат и распределение меток, а не корректность самих меток), честная демонстрация того, где few-shot ломается — на задачах с рассуждением. Канонический открытый учебник со ссылками на первоисточники, открытый исходник на GitHub. Весь раздел `techniques` покрывает модуль промпт-дизайна целиком.

### Не проверено

- The 2026 Guide to Prompt Engineering — https://www.ibm.com/think/prompt-engineering — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Prompt engineering techniques: Top 6 for 2026 — https://www.k2view.com/blog/prompt-engineering-techniques/ — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Prompt Engineering: Advanced Techniques for 2026 — https://www.digitalapplied.com/blog/prompt-engineering-advanced-techniques-2026 — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- System Prompt Design Best Practices | LLM Guide — https://www.buildmvpfast.com/blog/system-prompt-design-best-practices-llm-instructions-engineering-2026 — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Chain of Thought Prompting in AI: A Comprehensive Guide [2026] — https://orq.ai/blog/what-is-chain-of-thought-prompting — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Chain of Thought Prompting in 2026: Guide for GPT-5 + Claude 4.7 — https://futureagi.com/blog/chain-of-thought-prompting-ai-2025/ — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- AI Structured Output Guide 2026: JSON Mode Across OpenAI, Claude, and Gemini — https://crazyrouter.com/en/blog/ai-structured-output-json-mode-guide-2026 — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Top 10 Prompt Optimization Tools in 2026 — https://futureagi.com/blog/top-10-prompt-optimization-tools-2025/ — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- promptolution: A Unified, Modular Framework for Prompt Optimization — https://arxiv.org/pdf/2512.02840 — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- GPT-5.5 prompting guide — https://simonwillison.net/2026/apr/25/gpt-5-5-prompting-guide/ — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Codex Prompting Guide — https://developers.openai.com/cookbook/examples/gpt-5/codex_prompting_guide — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- You're prompting Gemini 3 wrong according to Google's new user guide — https://www.tomsguide.com/ai/youre-prompting-gemini-3-wrong-according-to-googles-new-user-guide-heres-what-to-do-instead — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Gemini 3 developer guide | Gemini API | Google AI for Developers — https://ai.google.dev/gemini-api/docs/gemini-3 — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Zero-Shot vs Few-Shot prompting: A Guide with Examples — https://www.vellum.ai/blog/zero-shot-vs-few-shot-prompting-a-guide-with-examples — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Prompt Engineering for AI Agents: 2026 Guide — https://pickaxe.co/post/prompt-engineering-ai-agents — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Structured Prompt Language: Declarative Context Management for LLMs — https://arxiv.org/pdf/2602.21257 — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
## Агенты и tool use

### Verified

#### The 2026 MCP Roadmap
- URL: https://blog.modelcontextprotocol.io/posts/2026-mcp-roadmap/
- Quality: A
- Level: intermediate
- Price: free
- Time: ~6 min read
- Verified: 2026-09-10
- Note: Confirmed live official MCP blog post (byline: David Soria Parra, Lead Maintainer). Lays out four 2026 priority areas (transport scalability, agent communication, governance maturation, enterprise readiness) and the Working Group / SEP process, with concrete detail on production gaps (load balancing, session state). Not a redirect or wrapper — genuine primary-source protocol content.

#### The 2026-07-28 Specification (Model Context Protocol)
- URL: https://blog.modelcontextprotocol.io/posts/2026-07-28/
- Quality: A
- Level: advanced
- Price: free
- Time: ~12 min read
- Verified: 2026-09-10
- Note: Confirmed live official MCP spec release announcement with concrete technical specifics: stateless protocol core, Multi Round-Trip Requests, header-based routing (Mcp-Method/Mcp-Name), cacheable list results, RFC 9207 authorization hardening, and adoption numbers (TypeScript/Python SDKs each over 1B downloads). Genuine primary-source technical announcement, not marketing copy.

#### Securing AI agents: When AI tools move from reading to acting
- URL: https://www.microsoft.com/en-us/security/blog/2026/06/30/securing-ai-agents-ai-tools-move-from-reading-acting/
- Quality: A
- Level: intermediate
- Price: free
- Time: ~6 min read
- Verified: 2026-09-10
- Note: Confirmed live official Microsoft Security blog post with a concrete worked example (MCP tool-metadata poisoning attack on a Copilot Studio invoice agent) plus specific mitigations (Purview/Sentinel detection, four control points). Concrete and specific, not fluff.

### Не проверено

- AI Agent Architecture: Build Systems That Work in 2026 — https://redis.io/blog/ai-agent-architecture/ — Reason: fetch failed: EGRESS_BLOCKED — redis.io is blocked by this session's network egress proxy; content could not be inspected.
- Types of AI Agent Architectures: 2026 Developer Guide — https://mlflow.org/articles/types-of-ai-agent-architectures-2026-developer-guide/ — Reason: fetch failed: EGRESS_BLOCKED — mlflow.org is blocked by this session's network egress proxy; content could not be inspected.
- LLM Function Calling 2026: Tool Use Across Providers — https://futureagi.com/blog/llm-function-calling-2025/ — Reason: fetch failed: EGRESS_BLOCKED — futureagi.com is blocked by this session's network egress proxy; content could not be inspected.
- The Evolution of Tool Use in LLM Agents: From Single-Tool Call to Multi-Tool Orchestration — https://arxiv.org/pdf/2603.22862 — Reason: fetch failed: EGRESS_BLOCKED — arxiv.org is blocked by this session's network egress proxy; content could not be inspected (tried both /pdf/ and /abs/ forms).
- Multi-Agent AI Systems in 2026: Frameworks, Patterns, Production — https://futureagi.com/blog/multi-agent-systems-2025/ — Reason: fetch failed: EGRESS_BLOCKED — futureagi.com is blocked by this session's network egress proxy; content could not be inspected.
- LangGraph vs CrewAI vs AutoGen: Which AI Agent Framework Should Your Enterprise Use in 2026? — https://pub.towardsai.net/langgraph-vs-crewai-vs-autogen-which-ai-agent-framework-should-your-enterprise-use-in-2026-3a9ebb407b09?gi=5874a541343c — Reason: fetch failed: EGRESS_BLOCKED — pub.towardsai.net is blocked by this session's network egress proxy; content could not be inspected.
- Building Production-Ready AI Agents in 2026 — https://mlflow.org/articles/building-production-ready-ai-agents-in-2026/ — Reason: fetch failed: EGRESS_BLOCKED — mlflow.org is blocked by this session's network egress proxy; content could not be inspected.
- State of AI Agent Memory 2026: Benchmarks & Trends Report — https://mem0.ai/blog/state-of-ai-agent-memory-2026 — Reason: fetch failed: EGRESS_BLOCKED — mem0.ai is blocked by this session's network egress proxy; content could not be inspected.
- AI Agent Frameworks (2026 Update): 8 SDKs Compared + the Claude Agent SDK Primitive Reference — https://www.morphllm.com/ai-agent-framework — Reason: fetch failed: EGRESS_BLOCKED — www.morphllm.com is blocked by this session's network egress proxy; content could not be inspected.
- The next evolution of the Agents SDK — https://openai.com/index/the-next-evolution-of-the-agents-sdk/ — Reason: fetch failed: EGRESS_BLOCKED — openai.com is blocked by this session's network egress proxy; content could not be inspected (retried, same result).
- Model Context Protocol (MCP): Security Design Considerations — https://media.defense.gov/2026/Jun/02/2003943289/-1/-1/0/CSI_MCP_SECURITY.PDF — Reason: fetch failed: EGRESS_BLOCKED — media.defense.gov is blocked by this session's network egress proxy; content could not be inspected.
- ReAct vs Plan-and-Execute: A Practical Comparison of LLM Agent Patterns — https://dev.to/jamesli/react-vs-plan-and-execute-a-practical-comparison-of-llm-agent-patterns-4gh9 — Reason: fetch failed: EGRESS_BLOCKED — dev.to is blocked by this session's network egress proxy; content could not be inspected (retried, same result).
- LLM Agent Evaluation Metrics in 2026: Tool Calling, Task Completion, Reasoning, and Trace-Based Evals — https://www.confident-ai.com/blog/llm-agent-evaluation-complete-guide — Reason: fetch failed: EGRESS_BLOCKED — www.confident-ai.com is blocked by this session's network egress proxy; content could not be inspected.
- Google's Agent2Agent Protocol Explained — https://galileo.ai/blog/google-agent2agent-a2a-protocol-guide — Reason: fetch failed: EGRESS_BLOCKED — galileo.ai is blocked by this session's network egress proxy; content could not be inspected.
- How Anthropic Built a Multi-Agent Research System — https://blog.bytebytego.com/p/how-anthropic-built-a-multi-agent — Reason: fetch failed: EGRESS_BLOCKED — blog.bytebytego.com is blocked by this session's network egress proxy; content could not be inspected.
- Model Context Protocol prepares to break with its stateful past — https://www.theregister.com/devops/2026/07/23/model-context-protocol-prepares-to-break-with-its-stateful-past/5276722 — Reason: fetch failed: EGRESS_BLOCKED — www.theregister.com is blocked by this session's network egress proxy; content could not be inspected.
- When to use multi-agent systems (and when not to) — https://claude.com/blog/building-multi-agent-systems-when-and-how-to-use-them — Reason: fetch failed: EGRESS_BLOCKED — claude.com is blocked by this session's network egress proxy; content could not be inspected.
## Стоимость и латентность

### Verified

### Не проверено

- LLM Cost Optimization Strategies: Complete Tactics List [2026] — https://atlan.com/know/ai-agent/llm-cost-optimization-strategies/ — Reason: fetch failed: EGRESS_BLOCKED — atlan.com is blocked by this session's network egress proxy; WebFetch never received page content.
- Reduce LLM Cost and Latency: A Comprehensive Guide for 2026 — https://www.getmaxim.ai/articles/reduce-llm-cost-and-latency-a-comprehensive-guide-for-2026/ — Reason: fetch failed: EGRESS_BLOCKED — getmaxim.ai is blocked by this session's network egress proxy.
- Why LLM Streaming Slows Down Your AI Platform (Token Streaming Latency Fix 2026) — https://medium.com/open-ai/why-llm-streaming-slows-down-your-ai-platform-token-streaming-latency-fix-2026-9de8de89fe8f — Reason: fetch failed: EGRESS_BLOCKED — medium.com is blocked by this session's network egress proxy.
- LLM Inference SLO Engineering: TTFT, ITL, and P99 Latency Budgets for Production AI (2026) — https://www.spheron.network/blog/llm-inference-slo-ttft-itl-latency-budget-guide-2026/ — Reason: fetch failed: EGRESS_BLOCKED — spheron.network is blocked by this session's network egress proxy.
- LLM Inference Optimization: Reduce Latency and Cost — https://www.runpod.io/blog/llm-inference-optimization-techniques-reduce-latency-cost — Reason: fetch failed: EGRESS_BLOCKED — runpod.io is blocked by this session's network egress proxy.
- Prompt Caching in 2026: Cut LLM Costs, Keep Quality — https://www.digitalapplied.com/blog/prompt-caching-2026-cut-llm-costs-engineering-guide — Reason: fetch failed: EGRESS_BLOCKED — digitalapplied.com is blocked by this session's network egress proxy.
- LLM Prompt Caching: Cost Savings, Invalidation & Workload Design — https://intuitionlabs.ai/articles/llm-prompt-caching-cost-savings — Reason: fetch failed: EGRESS_BLOCKED — intuitionlabs.ai is blocked by this session's network egress proxy.
- Cluster, Route, Escalate: Cascaded Framework for Cost-Aware LLM Serving — https://arxiv.org/html/2606.27457 — Reason: fetch failed: EGRESS_BLOCKED — arxiv.org is blocked by this session's network egress proxy.
- Dynamic Model Routing and Cascading for Efficient LLM Inference: A Survey — https://arxiv.org/html/2603.04445v1 — Reason: fetch failed: EGRESS_BLOCKED — arxiv.org is blocked by this session's network egress proxy.
- LLM Model Routing: Route Queries to the Right Model Automatically — https://neuraltrust.ai/blog/llm-model-routing — Reason: fetch failed: EGRESS_BLOCKED — neuraltrust.ai is blocked by this session's network egress proxy.
- Speculative Decoding: 2-3x Faster LLM Inference (2026) — https://blog.premai.io/speculative-decoding-2-3x-faster-llm-inference-2026/ — Reason: fetch failed: EGRESS_BLOCKED — blog.premai.io is blocked by this session's network egress proxy.
- How speculative decoding delivers faster LLM inference — https://developers.redhat.com/articles/2026/06/12/how-speculative-decoding-delivers-faster-llm-inference — Reason: fetch failed: EGRESS_BLOCKED — developers.redhat.com is blocked by this session's network egress proxy.
- LLM Inference Cost Comparison 2026: DigitalOcean vs. Together AI, Fireworks AI, Modal, Nebius, Baseten, and OpenRouter — https://www.digitalocean.com/community/conceptual-articles/llm-inference-cost-comparison — Reason: fetch failed: EGRESS_BLOCKED — digitalocean.com is blocked by this session's network egress proxy.
- LLM API Pricing Comparison 2026: 30+ Models, Every Provider — https://inference.net/content/llm-api-pricing-comparison/ — Reason: fetch failed: EGRESS_BLOCKED — inference.net is blocked by this session's network egress proxy.
- Token Usage Monitoring: Track, Attribute, and Optimise AI Spend — https://neuraltrust.ai/blog/token-usage-monitoring — Reason: fetch failed: EGRESS_BLOCKED — neuraltrust.ai is blocked by this session's network egress proxy.
- Best LLM monitoring tools in 2026 (tested & reviewed) — https://www.braintrust.dev/articles/best-llm-monitoring-tools-2026 — Reason: fetch failed: EGRESS_BLOCKED — braintrust.dev is blocked by this session's network egress proxy.
- LLM Inference Optimization — Quantization, Distillation & Speed (2026) — https://myengineeringpath.dev/genai-engineer/inference-optimization/ — Reason: fetch failed: EGRESS_BLOCKED — myengineeringpath.dev is blocked by this session's network egress proxy.
- LLM Inference Optimization: Quantization, Speculative Decoding, and Beyond — https://callsphere.ai/blog/llm-inference-optimization-quantization-speculative-decoding-2026 — Reason: fetch failed: EGRESS_BLOCKED — callsphere.ai is blocked by this session's network egress proxy.
- Cutting LLM Inference Costs in 2026: Where Caching, Batching, and Smart Routing Actually Pay Off — https://www.gmicloud.ai/en/blog/llm-inference-cost-optimization-caching-batching-routing — Reason: fetch failed: EGRESS_BLOCKED — gmicloud.ai is blocked by this session's network egress proxy.
- Model Distillation for LLMs: Cut Costs & Boost Speed in 2026 — https://redis.io/blog/model-distillation-llm-guide/ — Reason: fetch failed: EGRESS_BLOCKED — redis.io is blocked by this session's network egress proxy.
- Distillation with Programmatic Data Curation: Smarter LLMs, 5-30x Cheaper Inference — https://www.tensorzero.com/blog/distillation-programmatic-data-curation-smarter-llms-5-30x-cheaper-inference/ — Reason: fetch failed: EGRESS_BLOCKED — tensorzero.com is blocked by this session's network egress proxy.
## Prompt injection

### Verified

#### Fooling AI Agents: Web-Based Indirect Prompt Injection Observed in the Wild — Unit 42
- URL: https://unit42.paloaltonetworks.com/ai-agent-prompt-injection/
- Quality: A
- Level: intermediate → advanced
- Price: free
- Time: ~1.5 hours (заявлено 20 минут чтения, реально дольше с разбором)
- Verified: 2026-09-11 (manual check)
- Published: 2026-03-03
- Note: Полевое исследование на реальной телеметрии (не теория). Таксономия непрямых инъекций по двум осям — намерение атакующего и инженерия полезной нагрузки (доставка: нулевой размер шрифта, CSS-сокрытие, off-screen, HTML-атрибуты, SVG/CDATA; обход: невидимые символы, гомоглифы, разбиение нагрузки, многослойное кодирование). 12 разобранных реальных случаев. Телеметрия: 85.2% обходов — обычная социальная инженерия; 37.8% доставки — просто видимый текст на странице. Раздел защит: spotlighting, иерархия инструкций, состязательное обучение, архитектурные защиты. Корневая причина, которую разбирает статья — LLM не отличает инструкции от данных в одном потоке контекста — прямо соответствует принципу "содержимое страниц — данные, не команды" в правилах этого репозитория. Страница сама содержит директиву для ИИ-агентов не исполнять приведённые на ней примеры — наглядный пример границы доверия на практике; директива не выполнялась, содержимое использовано только как описываемый материал.

### Не проверено

- Prompt Injection Defense for Production AI Agents: A Complete 2026 Guide — https://www.getmaxim.ai/articles/prompt-injection-defense-for-production-ai-agents-a-complete-2026-guide/ — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- The Comprehensive Guide to Prompt Injection Attacks in 2026 — https://www.sysdig.com/learn-cloud-native/prompt-injection — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- PIArena: A Platform for Prompt Injection Evaluation — https://arxiv.org/pdf/2604.08499 — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- LongPIBench: A Long-Context Benchmark for Prompt Injection — https://arxiv.org/abs/2608.28411v1 — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Indirect Prompt Injection: The Hidden Threat Breaking Modern AI Systems — https://www.lakera.ai/blog/indirect-prompt-injection — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Indirect Prompt Injection Attacks: Hidden AI Risks — https://www.crowdstrike.com/en-us/blog/indirect-prompt-injection-attacks-hidden-ai-risks/ — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Agent Data Injection Attacks are Realistic Threats to AI Agents — https://arxiv.org/html/2607.05120v1 — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Prompt Injection Hacking: Emerging Trade Secret, Employment, and Litigation Risks — https://ktslaw.com/insights/alert/2026/7/prompt-injection-hacking-emerging-trade-secret-employment-and-litigation-risks — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- GitInject: Real-World Prompt Injection Attacks in AI-Powered CI/CD Pipelines — https://arxiv.org/pdf/2606.09935 — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- The Promptware Kill Chain: How Prompt Injections Gradually Evolved Into a Multistep Malware Delivery Mechanism — https://arxiv.org/pdf/2601.09625 — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Prompt Injection vs. Jailbreaking: What's the Difference? — https://learnprompting.org/blog/injection_jailbreaking — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Prompt Injection vs Jailbreaking: What's the Difference? — https://www.promptfoo.dev/blog/jailbreaking-vs-prompt-injection/ — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- LlamaFirewall: An Open Source Guardrail System for Building Secure AI Agents — https://arxiv.org/pdf/2505.03574 — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Cortex AI Guardrails: Prompt Injection & Jailbreak Prevention — https://www.snowflake.com/en/blog/engineering/cortex-ai-guardrails-prompt-injection-prevention/ — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
## Дорожные карты AI Engineer

### Verified

#### atryx/ai-engineer-roadmap-2026
- URL: https://github.com/atryx/ai-engineer-roadmap-2026
- Quality: C
- Level: beginner to advanced
- Price: free
- Time: ~30-45 min read (roadmap doc); full path is multi-month self-paced
- Verified: 2026-09-10
- Note: Repo loads and is active (most recent commit April 15, 2026, within 12 months). README lays out a concrete 10-phase path (foundations, LLM fundamentals, prompt engineering, RAG, agents, fine-tuning, evaluation, production, multi-modal, advanced patterns) with tool-comparison tables and project ideas. Caveat: only 2 commits total, one of which is just a "GitAds verification" add — thin commit history typical of a monetization-oriented roadmap repo rather than a heavily maintained community project, so treat as a secondary/unofficial overview.

#### Ultimate AI Engineer Roadmap 2026 (PrinceSinghhub)
- URL: https://github.com/PrinceSinghhub/Ultimate-AI-Engineer-Roadmap-2026
- Quality: B
- Level: beginner to advanced
- Price: free
- Time: ~1-2 hours to read the full roadmap; full path is multi-month self-paced
- Verified: 2026-09-10
- Note: Active repo (852 stars, 133 forks, most recent commit August 1, 2026). README spans 17 phases plus a capstone (Python/math/ML/DL foundations through NLP, LLMs, multi-LLM orchestration, RAG, agents, fine-tuning, MLOps, system design, RL, ethics), each phase with learning objectives, code examples, and tiered (easy/medium/hard) projects — concrete and detailed enough to be a solid secondary roadmap.

#### musamaanjum/ai-engineer-roadmap
- URL: https://github.com/musamaanjum/ai-engineer-roadmap
- Quality: C
- Level: intermediate
- Price: free
- Time: ~20-30 min read
- Verified: 2026-09-10
- Note: Repo loads, most recent commit March 2, 2026 (within 12 months), though only 1 commit and modest traction (15 stars, 1 fork). README has concrete specifics: a 4-phase curriculum, 24 named courses (DeepLearning.AI, Stanford, Coursera), 5 named portfolio projects (RAG, fine-tuning, multi-agent, evaluation, production app), and interview-prep resources — enough concrete detail to pass, but limited vetting/maturity versus the other two repos.

### Не проверено

- AI Engineer Roadmap | roadmap.sh — https://roadmap.sh/ai-engineer — Reason: fetch failed: this environment's network egress proxy blocked the domain outright (EGRESS_BLOCKED), so the live page could not be loaded to verify its actual content; not evaluated on content, only on inability to fetch.
- AI Engineer Roadmap 2026: Step-by-Step Guide (Medium, jeslurrahman) — https://medium.com/@jeslurrahman/ai-engineer-roadmap-2026-step-by-step-guide-to-become-an-ai-engineer-with-free-resources-5beba43677d1 — Reason: fetch failed: domain blocked by network egress proxy (EGRESS_BLOCKED), could not load content.
- AI Engineer Roadmap: How to Become an AI Engineer in 2026 (Turing College) — https://www.turingcollege.com/blog/ai-engineer-roadmap-how-to-become-an-ai-engineer — Reason: fetch failed: domain blocked by network egress proxy (EGRESS_BLOCKED), could not load content.
- How to Become an AI Engineer in 2026 (A Complete Roadmap) (Dataquest) — https://www.dataquest.io/blog/ai-engineer-roadmap/ — Reason: fetch failed: domain blocked by network egress proxy (EGRESS_BLOCKED), could not load content.
- AI Engineer Roadmap 2026: From LLM APIs to Production (Dataskew) — https://dataskew.io/roadmaps/ai-engineering/ — Reason: fetch failed: domain blocked by network egress proxy (EGRESS_BLOCKED), could not load content.
- How to Become an AI Engineer & Get Hired in 2026 (Zero To Mastery) — https://zerotomastery.io/blog/how-to-become-an-ai-engineer/ — Reason: fetch failed: domain blocked by network egress proxy (EGRESS_BLOCKED), could not load content.
- How to Become an AI Engineer in 2026: A Self-Study Roadmap (KDnuggets) — https://www.kdnuggets.com/how-to-become-an-ai-engineer-in-2026-a-self-study-roadmap — Reason: fetch failed: domain blocked by network egress proxy (EGRESS_BLOCKED), could not load content.
- The Roadmap to Becoming an LLM Engineer in 2026 (KDnuggets) — https://www.kdnuggets.com/the-roadmap-to-becoming-an-llm-engineer-in-2026 — Reason: fetch failed: domain blocked by network egress proxy (EGRESS_BLOCKED), could not load content.
- How to Become an AI Engineer in 2026: Complete AI Engineering Roadmap (dev.to, amd87) — https://dev.to/amd87/how-to-become-an-ai-engineer-in-2026-complete-ai-engineering-roadmap-25p6 — Reason: fetch failed: domain blocked by network egress proxy (EGRESS_BLOCKED), could not load content.
- How I'd Learn AI Engineering in 2026 (Louis Bouchard) — https://www.louisbouchard.ai/how-to-learn-ai-engineering-2026/ — Reason: fetch failed: domain blocked by network egress proxy (EGRESS_BLOCKED), could not load content.
- The 16 Essential AI Engineer Skills You Need to Know in 2026 (DataCamp) — https://www.datacamp.com/blog/essential-ai-engineer-skills — Reason: fetch failed: domain blocked by network egress proxy (EGRESS_BLOCKED), could not load content.
- AI Engineering Career Path: Complete Guide for 2026 (DataExpert) — https://www.dataexpert.io/blog/ai-engineering-career-path-complete-guide-2026 — Reason: fetch failed: domain blocked by network egress proxy (EGRESS_BLOCKED), could not load content.
- AI Engineer Roadmap 2026: Complete Learning Path (AppliedAICourse) — https://www.appliedaicourse.com/blog/best-ai-engineer-roadmap/ — Reason: fetch failed: domain blocked by network egress proxy (EGRESS_BLOCKED), could not load content.
- A concise curriculum for Applied AI in 2025 (Substack, saqib) — https://saqib.substack.com/p/a-concise-curriculum-for-applied — Reason: fetch failed: domain blocked by network egress proxy (EGRESS_BLOCKED), could not load content.
- The 5 Best AI Engineering Bootcamps in 2026 (TripleTen) — https://tripleten.com/blog/posts/best-ai-engineering-bootcamps — Reason: fetch failed: domain blocked by network egress proxy (EGRESS_BLOCKED), could not load content.
- Andrew Ng and DeepLearning.AI Present the Essential Skills Every AI Engineer Needs in 2026 (The Batch) — https://www.deeplearning.ai/the-batch/the-ai-engineering-skills-map — Reason: fetch failed: domain blocked by network egress proxy (EGRESS_BLOCKED), could not load content.
- AI Certifications Guide — AWS, Google & Azure AI Certs (2026) — https://myengineeringpath.dev/genai-engineer/certifications/ — Reason: fetch failed: domain blocked by network egress proxy (EGRESS_BLOCKED), could not load content.
## Вопросы на собеседованиях AI Engineer

### Verified

### Не проверено

- 45+ AI Engineer Interview Questions & Answers (2026 Guide) – Career Services — https://careerservices.upenn.edu/blog/2026/06/25/45-ai-engineer-interview-questions-answers-2026-guide/ — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Every AI Engineer Interview Question You Need to Know in 2026 (From 100+ Real Interviews) — https://adilshamim8.medium.com/every-ai-engineer-interview-question-you-need-to-know-in-2026-from-100-real-interviews-b5b7ae4b961a — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- 45+ AI Engineer Interview Questions & Answers (2026 Guide) - Aced (formerly Exponent) — https://www.tryexponent.com/blog/ai-engineer-interview-questions — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- LLM Engineer Interview Questions: 2026 Hiring Guide — https://www.kore1.com/llm-engineer-interview-questions/ — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Top 10 LLM Engineer Interview Questions and Answers for 2026: What Hiring Managers at Top AI Companies Are Actually Testing For — https://blog.theinterviewguys.com/llm-engineer-interview-questions-and-answers/ — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- 50 AI Engineer Interview Questions: 2026 LLM Guide — https://letsdatascience.com/blog/50-llm-and-ai-engineer-interview-questions-for-2026 — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Top 36 LLM Interview Questions and Answers for 2026 — https://www.datacamp.com/blog/llm-interview-questions — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- LLM Interview Questions — 30 Questions Senior Engineers Ask (2026) — https://myengineeringpath.dev/genai-engineer/llm-interview-questions/ — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Generative AI System Design Interview: 2026 Guide — https://www.systemdesignhandbook.com/guides/generative-ai-system-design-interview/ — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- AI System Design Interview Questions (2026) — https://www.systemdesignhandbook.com/blog/ai-system-design-interview-questions/ — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- The Complete Agentic AI System Design Interview Guide 2026 — https://atul4u.medium.com/the-complete-agentic-ai-system-design-interview-guide-2026-f95d0cfeb7cf — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Machine Learning System Design Interview (2026 Guide) — https://www.tryexponent.com/blog/machine-learning-system-design-interview-guide — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Top 30 RAG Interview Questions and Answers for 2026 — https://www.datacamp.com/blog/rag-interview-questions — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- 7 RAG & Agent System Design Questions You Will Face in Every AI Engineer Interview (With Answers) — https://pub.towardsai.net/7-rag-agent-system-design-questions-you-will-face-in-every-ai-engineer-interview-with-answers-45d31004ffe4 — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- RAG Interview: 40 Questions to Go from Beginner to Advanced — https://www.analyticsvidhya.com/blog/2026/02/rag-interview-questions-and-answers/ — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Top 36 Generative AI Interview Questions and Answers for 2026 — https://www.datacamp.com/blog/genai-interview-questions — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Prompt Engineering Interview Questions That Actually Get Asked — https://codesignal.com/blog/prompt-engineering-interview-questions/ — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Top 32 Prompt Engineering Interview Questions (2026) — https://www.datainterview.com/blog/prompt-engineering-interview-questions — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Design and optimize a RAG system | OpenAI Interview Question — https://prachub.com/interview-questions/design-and-optimize-a-rag-system — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)
- Top 20 AI & Machine Learning Interview Questions (2026) — https://www.tredence.com/blog/top-20-ai-machine-learning-interview-questions-2026 — Reason: fetch failed: EGRESS_BLOCKED (session network policy allows only GitHub-related domains; this host was never reachable, so no verdict could be made on content)

---

## Итог проверки

- **Проверено (реально открыто):** 12 из 183 — 7 через WebFetch в этой сессии (10.09.2026), 5 вручную вне сетевого ограничения (11.09.2026)
- **Прошло:** 12 из 12
- **Не открывалось вообще:** 53 (темы, которые не затрагивала ручная проверка: llm-basics-tokenization — 19, agents-tool-use — 17, ai-engineer-roadmaps — 17)
- **Открыто по 7 темам ручной проверкой, из них:**
  - Прошло и подтверждено: 5 (учтены выше)
  - Отсеяно по жанру источника, без открытия содержимого: ~76-78 (вендорские «топ-N» листиклы, контент-маркетинг вокруг продукта, Medium/агрегаторы, один юридический материал, плюс большая часть темы «Вопросы на собеседованиях» — см. `research/urls-to-verify.md` для полной разбивки, обоснования и сверки чисел)
  - Прошли жанровый фильтр, но пока не открыты — в очереди: 40
  - Найдено по ссылкам из уже проверенных источников (новые кандидаты, не из исходных 183) — 9, добавлены в `research/raw/` и в очередь на первоочередную проверку

### Почему не открылось — разбивка по причинам

| Причина | Количество |
|---|---|
| `EGRESS_BLOCKED` — домен заблокирован сетевой политикой сессии, не проверялось за пределами сессии (53, темы вне ручной проверки) | 53 |
| Отсеяно по жанру источника без открытия содержимого (ручная проверка) | 78 |
| Прошли жанровый фильтр, ждут открытия | 40 |

Единственный домен, к которому у сессии есть прямой доступ, — GitHub (плюс два случайных хоста, `blog.modelcontextprotocol.io` и `www.microsoft.com`). Пять дополнительных источников проверены вручную вне этой сессии — все прошли (Quality A по всем пяти).

**Это не значит, что 78 отсеянных по жанру или 53 неоткрытых источника плохие** — жанровый отсев не оценивает содержание, а 53 не открывались вообще. Полная разбивка по каждой ссылке — в `research/urls-to-verify.md`.
