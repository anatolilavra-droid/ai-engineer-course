# CORE — AI Engineer Curriculum Spine

This is the durable backbone of the course: modules, sequencing, learning objectives, and
lesson content built strictly from sources verified in `research/verified.md`. It is meant
to stay stable — it should not need rewriting every time a model or framework ships a new
version. Version-sensitive material (tool choices, pricing, 2026 roadmaps, interview trends)
lives in `CURRENT.md` and links back here by module name.

## How to read this document

Every module below has:
- **Learning objectives** — what the learner should be able to do afterward. These are
  written from general instructional-design reasoning about the topic (connective
  narrative), which the curriculum rules permit even where no citable source exists yet.
- **Prerequisites** — which earlier modules/sub-skills it assumes.
- **Lesson content** — either (a) verified-source-backed material with exact citations, or
  (b) an explicit **GAP** block. Per the hard rules governing this curriculum, a GAP is
  never papered over with unsourced "explainer" text dressed up as a lesson — if the box
  says GAP, there is no vetted resource to teach that sub-topic yet, only a description of
  what kind of source is needed and which raw candidates (by title, under
  `research/raw/<topic>/`) should be checked first once this session's network access
  widens beyond GitHub-and-two-domains.

## Note on the learner profile driving sequencing

`LEARNER.md` currently has nearly every field marked `_TBD_` (role, programming experience,
prior ML exposure, math comfort, goals, timeline, preferred stack, depth-vs-breadth
preference). Only the "Success criteria" skill list is filled in, and it is used directly as
this course's module outline. Because the background/goals fields are undetermined, this
spine is deliberately built to be **broad and adaptive rather than tuned to one archetype**:

- Every module states a **beginner-accessible on-ramp** and calls out where **intermediate/
  advanced** branches exist, instead of assuming a fixed starting level.
- Sequencing assumes only generic "can read Python-like code and call an HTTP API"
  familiarity — the most conservative assumption compatible with an "AI Engineer" audience —
  and flags anywhere a stronger math/ML background would let a learner skip ahead.
- Pacing is given as rough order-of-magnitude time (hours vs. multi-day), not a fixed
  week-by-week plan, since the learner's weekly time budget is unknown.
- Preferred format (reading/video/hands-on) is unknown, so lesson content favors whatever
  verified source exists regardless of medium (currently: READMEs and technical blog posts —
  all reading-based, which is itself a known bias in this early spine).

**This should be revisited** the moment `LEARNER.md` is filled in with real answers — in
particular, the depth of Module 1 (math/attention internals) and the ordering of Module 6 vs.
Module 5 should be adjusted once actual prior ML exposure and goals are known.

---

## Module map & sequencing

```
0. Orientation
     |
1. LLM Fundamentals & Tokenization
     |
     +--> 2. Embeddings & Vector Search --> 3. Retrieval-Augmented Generation (RAG)
     |                                            |
     +--> 5. Prompt Design & Iteration            |
     |          |                                 |
     |          v                                 v
     +--> 6. Agents & Tool Use  <------------------
                |
                +--> 8. Prompt Injection & Security
                |
     4. Evaluation (Evals)  ---- cross-cuts 3, 5, 6, 8 (teach after RAG + Agents exist to evaluate)
                |
     7. Cost & Latency  ---- cross-cuts everything (teach once learner has a working system to optimize)
                |
     9. Interview Readiness  ---- capstone, last
```

Rationale: Module 1 is the only load-bearing prerequisite for everything else (you cannot
reason about context windows, cost, or embeddings without knowing what a token is). Modules
2→3 and 5 can run in parallel tracks since embeddings/RAG and prompt design are
independent skills that both feed Module 6 (agents combine retrieval + prompting + tool
calls). Evals (4) and Cost/Latency (7) are deliberately sequenced *after* the learner has
something built (RAG pipeline, an agent) because both are about measuring and improving an
existing system, not standalone topics. Security (8) follows Agents because the concrete
attack surface (tool-metadata poisoning, indirect injection via retrieved/tool content) only
makes sense once the learner has tools/retrieval in the loop. Interview readiness (9) is the
capstone.

---

## Module 0: Orientation

**Prerequisites:** none.

**Learning objectives:**
- Understand what "AI Engineer" means as a role distinct from ML research/MLOps (building
  applications on top of foundation models via APIs, RAG, agents, and evals, rather than
  training models from scratch).
- Get oriented on the overall path and know where to find current tooling/roadmap material.

**Lesson content:** See `CURRENT.md → Roadmaps & Orientation` for the three verified
roadmap repositories this course draws sequencing inspiration from. No CORE-level narrative
duplicated here — roadmaps are inherently version-sensitive and belong entirely in the
CURRENT layer.

---

## Module 1: LLM Fundamentals & Tokenization

**Prerequisites:** none (entry point of the course).

**Learning objectives:**
- Explain what a tokenizer does and why LLMs operate on tokens, not characters or words.
- Use a real BPE tokenizer to encode/decode text and count tokens before sending a request.
- Understand why token count drives both cost and context-window budget (connects forward to
  Module 7).
- (Stretch, currently a GAP — see below) Explain context windows, sampling parameters
  (temperature/top-k/top-p), attention, and KV caching at a working level.

### Lesson 1.1 — Byte-Pair Encoding in practice (SOURCED)

Verified source:
- **GitHub - openai/tiktoken: a fast BPE tokeniser for use with OpenAI's models**
  https://github.com/openai/tiktoken — Quality A · Level: intermediate · Price: free ·
  Time: ~20 min to read README + try examples · Verified 2026-09-10.

Teach directly from this README:
- Install `tiktoken`, load an encoding with `encoding_for_model` or `get_encoding`
  (`cl100k_base`, `o200k_base`).
- Encode a string to token IDs and decode back; count tokens for a prompt before sending it
  to an API — this is the concrete skill a learner needs before Module 7 (cost/latency).
- Note the tool's own benchmark claim (3-6x faster than comparable tokenizers) as a talking
  point for why production systems use a compiled BPE tokenizer rather than a naive
  whitespace/regex splitter.
- Exercise: have the learner tokenize the same sentence in `cl100k_base` vs. `o200k_base`
  and observe the token-count difference — this is fully reproducible from the repo's own
  documented API and doesn't require any additional uncited claims.

This lesson only covers *tokenization itself*. It does not cover *why* BPE merges work the
way they do at an algorithmic level (that would need a walkthrough source), or how different
providers' tokenizers compare — those are gaps below.

### Lesson 1.2 — Context windows, sampling, attention & KV cache (GAP)

**GAP.** Zero verified sources support this sub-topic. What's needed:
1. A verified, primary or high-quality secondary explainer of **temperature/top-k/top-p
   sampling** with worked numeric examples (not just definitions).
2. A verified explainer of **context windows** — what consumes them, how providers differ,
   and practical implications for RAG/agent design.
3. A verified explainer of **attention and KV cache** at a conceptual (not necessarily
   from-scratch-math) level suitable for an engineer who will *use* LLMs via API rather than
   train them.
4. Ideally a verified source specifically comparing how different vendor tokenizers
   (Claude/GPT/Gemini) count the same text differently, since that has direct cost/prompt-
   design implications the learner will hit in practice.

Candidate raw entries to re-check first (titles, under
`research/raw/llm-basics-tokenization/`) once broader network access is available:
- "How do temperature, top-k, and top-p sampling differ?" (Sebastian Raschka FAQ) —
  `13-sampling-temperature-topk-topp-raschka.md`
- "LLM Sampling Parameters Explained: Intuition to Math" —
  `14-llm-sampling-parameters-intuition-math.md`
- "Context Window Optimization: 6 LLM Strategies for 2026" —
  `11-context-window-optimization-2026.md`
- "What Is KV Cache in LLMs? A 2026 Guide" — `18-kv-cache-llms-explained-2026.md`
- "AI 101: Your Ultimate Guide to Attention: Mechanism, QKV, and KV Cache" —
  `19-attention-qkv-kvcache-turingpost.md`
- "Tokenizer Quirks: Claude, GPT, and Gemini Don't Count the Same Text the Same Way" —
  `15-tokenizer-quirks-claude-gpt-gemini.md`
- "Tokenization and byte pair encoding" (Sebastian Raschka FAQ, algorithmic detail on BPE
  itself) — `05-tokenization-bpe-sebastian-raschka.md`
- "Byte-Pair Encoding tokenization" (Hugging Face LLM Course, likely has a worked BPE-merge
  example suitable for teaching the algorithm, not just the tool) —
  `04-byte-pair-encoding-huggingface-course.md`

None of these may be cited or taught from until a verification pass actually opens them and
records a verdict under a "### Verified" heading in `research/verified.md`.

---

## Module 2: Embeddings & Vector Search

**Prerequisites:** Module 1 (tokens are the unit embeddings are computed over; context-
window reasoning carries forward).

**Learning objectives:**
- Explain what an embedding is and why semantic similarity is computed via vector distance.
- Choose an embedding model appropriately (dimensionality, domain fit, cost) for a given
  task. (Stretch, currently a GAP.)
- Understand approximate nearest-neighbor search at a conceptual level (specifically HNSW,
  the dominant production index type) well enough to reason about recall/latency tradeoffs,
  and be able to tune its core parameters (M, efConstruction, efSearch).
- Understand hybrid search (combining sparse/BM25 with dense vector retrieval) and why pure
  vector search under-performs on exact-match/keyword-heavy queries. (Stretch, currently a
  GAP.)
- Understand chunking strategy as a first-order lever on retrieval quality. (Stretch,
  currently a GAP.)

### Lesson 2.1 — How vector search actually works: HNSW (SOURCED)

Verified source:
- **Hierarchical Navigable Small Worlds (HNSW) — Pinecone**
  https://www.pinecone.io/learn/series/faiss/hnsw/ — Quality A · Level: intermediate ·
  Price: free · Time: ~2-3 hours with the code · Verified 2026-09-11 (manual check).

Teach directly from this page:
- How HNSW is built up conceptually: skip lists → NSW graphs → the layered HNSW structure.
- The Faiss implementation with real parameters (`M`, `efConstruction`, `efSearch`) and what
  each one trades off.
- The worked benchmark on Sift1M: recall, search time, and memory tradeoffs as `efSearch`
  changes — this is the concrete "why do I get a slower/faster, more/less accurate index"
  intuition an application engineer needs before picking defaults in a real vector DB.
- Exercise: have the learner run the linked notebook, then predict (before checking) what
  raising `efSearch` does to recall and latency, then verify against the plot.
- Point at the original Malkov HNSW papers linked from the page for anyone who wants the
  primary research citation, without requiring the learner to read them to pass this lesson.
- Note for later: this page is part of Pinecone's "Faiss: The Missing Manual" series; the
  other chapters (LSH, product quantization, composite indexes) are strong secondary-priority
  candidates once re-verified — see `research/raw/embeddings-vector-search/16-faiss-missing-manual-series.md`
  and `research/raw/embeddings-vector-search/11-product-quantization-pinecone.md`.

This lesson only covers *how the index itself works*. It does not cover model selection,
hybrid search, chunking, or reranking — those remain gaps below.

### Lesson 2.2 — Model selection, hybrid search, chunking, reranking (GAP)

**GAP.** No verified source yet for these sub-topics; every other candidate under
"Эмбеддинги и векторный поиск" in `research/verified.md` is `EGRESS_BLOCKED` or was screened
out by genre without being opened (see `research/urls-to-verify.md`).

What's specifically needed, by sub-topic:
1. **Embedding model selection** — a verified, non-listicle comparison with actual benchmark
   methodology (not just a ranked table) covering open-source and API-based embedding
   models.
2. **Hybrid search** — a verified source with concrete implementation guidance for combining
   BM25 and dense retrieval (fusion method, e.g. RRF), ideally with a worked example.
3. **Chunking strategy** — a verified source comparing chunking methods with actual code,
   not just named strategies.
4. **Reranking** — a verified source explaining cross-encoder rerankers and when they're
   worth the added latency.

Candidate raw entries to re-check first (titles, under
`research/raw/embeddings-vector-search/`) — 4 flagged "worth opening next" in
`research/urls-to-verify.md`:
- "Product Quantization: Compressing high-dimensional vectors by 97%" (Pinecone, same
  verified series as 2.1) — `11-product-quantization-pinecone.md`
- "Fine-tuning embeddings for RAG with synthetic data" (LlamaIndex) —
  `10-fine-tuning-embeddings-synthetic-data-llamaindex.md`
- "Scaling Vector Search to 1 Billion on PostgreSQL" (VectorChord) —
  `12-scaling-vector-search-billion-postgresql.md`
- "Hybrid Search in Production: Why BM25 Still Wins" (tianpan.co) —
  `06-hybrid-search-production-bm25.md`

Other candidates (screened out by genre — vendor listicle/content-marketing — without being
opened; could be revisited if the topic still lacks material):
- "The Best Open-Source Embedding Models in 2026" — `01-open-source-embedding-models-2026.md`
- "How to Choose the Best Embedding Model for RAG in 2026: 10 Models Benchmarked" —
  `02-choosing-best-embedding-model-rag-2026.md`
- "MTEB Leaderboard 2026: Best Embedding Models for RAG" — `09-mteb-leaderboard-2026.md`
- "Hierarchical Navigable Small Worlds (HNSW)" (Pinecone's own explainer series — likely the
  strongest primary-ish candidate here) — `04-hnsw-pinecone-explainer.md`
- "Product Quantization: Compressing high-dimensional vectors by 97%" (Pinecone) —
  `11-product-quantization-pinecone.md`
- "Hybrid Search Guide: Vectors & Full-Text" — `05-hybrid-search-guide-supermemory.md`
- "Hybrid Search in Production: Why BM25 Still Wins on the Queries That Matter" —
  `06-hybrid-search-production-bm25.md`
- "RAG Chunking Strategies 2026: 8 Methods Compared with Code Examples" —
  `07-rag-chunking-strategies-8-methods-2026.md`
- "RAG Chunking Strategies: The 2026 Benchmark Guide" —
  `08-rag-chunking-benchmark-guide-2026.md`
- "Top Reranking Models to Boost RAG Accuracy in 2026" —
  `15-top-reranking-models-rag-2026.md`
- "Comparing the best open source vector databases (2026)" (for the practical "which vector
  DB" question learners will ask) — `03-open-source-vector-databases-comparison-2026.md`
- "Best Multimodal Embedding Models in 2026" (if the course scope extends to multimodal) —
  `14-best-multimodal-embedding-models-2026.md`

---

## Module 3: Retrieval-Augmented Generation (RAG)

**Prerequisites:** Module 2 (RAG is retrieval + generation; can't teach it without
embeddings/vector search already covered).

**Learning objectives (intended scope, not yet sourced):**
- Explain the basic RAG architecture (index → retrieve → augment prompt → generate) and why
  it exists (grounding, freshness, avoiding fine-tuning for knowledge injection).
- Distinguish naive RAG from more advanced patterns (agentic RAG, GraphRAG) and know when
  the added complexity is justified.
- Reason about RAG vs. long-context as competing/complementary strategies.
- Recognize common RAG failure modes (retrieval miss, lost-in-the-middle, stale index,
  hallucination despite grounding) and know first-line mitigations.

### Lesson content: GAP (entire module)

**GAP — no verified sources at all.** Zero verified entries under "RAG" in
`research/verified.md`; every candidate blocked as `EGRESS_BLOCKED`.

What's specifically needed, by sub-topic:
1. **Core architecture** — a verified, concrete (not listicle) walkthrough of a RAG pipeline
   with actual implementation detail.
2. **Agentic RAG** — a verified source explaining how retrieval becomes a tool call inside
   an agent loop rather than a fixed pre-generation step (this connects directly to
   Module 6).
3. **GraphRAG** — a verified source (ideally from a vendor actually shipping the pattern)
   explaining when knowledge-graph-augmented retrieval beats vector-only retrieval.
4. **RAG evaluation** — a verified source on RAG-specific metrics (faithfulness, context
   precision/recall) — this is also a direct dependency for Module 4.
5. **Failure modes** — a verified source cataloguing concrete RAG failure modes with
   mitigations, not just a checklist.
6. **RAG vs. long-context** — a verified, even-handed comparison (not a vendor pitch for
   one side).

Candidate raw entries to re-check first (titles, under `research/raw/rag/`):
- "RAG Architectures Every AI Developer Must Know in 2026: A Complete Guide with Examples" —
  `01-rag-architectures-2026-guide.md`
- "20 Advanced RAG Types to Know in 2026" — `02-advanced-rag-types-turingpost.md`
- "Engineering the RAG Stack: A Comprehensive Review of the Architecture and Trust
  Frameworks for Retrieval-Augmented Generation Systems" (arXiv survey — worth prioritizing
  if arXiv access opens up, since surveys tend to be well-sourced) —
  `04-engineering-rag-stack-survey-arxiv.md`
- "9 advanced RAG techniques to know & how to implement them [2026]" —
  `05-meilisearch-advanced-rag-techniques.md`
- "What is Agentic RAG? Everything You Need to Know in 2026" — `06-agentic-rag-lyzr.md`
- "Agentic RAG in 2026: Patterns, Code, Observability" — `07-agentic-rag-patterns-futureagi.md`
- "What is GraphRAG?" (Neo4j — vendor-primary for the pattern) — `08-graphrag-neo4j.md`
- "GraphRAG Architecture: Components, Workflow & Implementation Guide" —
  `09-graphrag-architecture-puppygraph.md`
- "RAG Evaluation Metrics in 2026: Faithfulness & More" —
  `10-rag-evaluation-metrics-futureagi.md`
- "RAG Evaluation: Metrics, Tools, and the Context Gap (2026)" — `11-rag-evaluation-atlan.md`
- "RAG failure modes: common pitfalls and solutions" (Snorkel) —
  `15-snorkel-rag-failure-modes.md`
- "RAG vs. long-context LLMs: A side-by-side comparison" —
  `14-rag-vs-long-context-meilisearch.md`
- "How to Build Cross-Encoder Re-Ranking" — `13-cross-encoder-reranking-oneuptime.md`
- "Hybrid Search for RAG: Combining BM25 and Dense Vector Search (2026 Guide)" —
  `16-hybrid-search-denser-2026.md`

---

## Module 4: Evaluation (Evals)

**Prerequisites:** Module 3 and Module 6 (you need a RAG pipeline and/or an agent to
meaningfully teach evaluation against — evals is about measuring systems that already
exist). Also draws on Module 5 (prompt regression testing).

**Learning objectives:**
- Explain why evals matter for LLM applications specifically (non-determinism, no single
  ground truth, regressions from prompt/model changes).
- Distinguish offline from online evaluation, and reference-based from reference-free
  evaluators (human, code, LLM-as-judge, pairwise comparison), and know where each applies.
- Build an offline eval dataset starting small (10-20 manual examples → historical traces →
  synthetic data) and distinguish evaluation from testing.
- (Stretch, currently a GAP) Distinguish LLM-as-judge from rule-based/reference-based metrics
  and know the failure modes of each (judge bias, calibration drift); wire evals into CI/CD
  as a regression gate; apply RAG-specific and agent-specific eval metrics (dependencies from
  Modules 3 and 6).

### Lesson 4.1 — Evaluation concepts: the conceptual backbone (SOURCED)

Verified source:
- **Evaluation concepts — LangSmith / LangChain docs**
  https://docs.langchain.com/langsmith/evaluation-concepts — Quality A · Level: intermediate
  · Price: free (docs; the LangSmith product itself is paid) · Time: ~1.5-2 hours · Verified
  2026-09-11 (manual check).

Teach directly from this page — it is framework-agnostic in substance even though it lives in
LangSmith's docs, so every idea transfers to a self-built eval harness:
- **Offline vs. online**: offline evals run pre-deployment on datasets with reference
  answers; online evals run on live traffic without references. Teach when each is the right
  tool (offline for regression-gating a prompt/model change; online for catching drift in
  production the offline set didn't anticipate).
- **Evaluator types**: human, code-based, LLM-as-judge, and pairwise comparison — with the
  reference-based vs. reference-free distinction as the axis that determines which evaluator
  type is even applicable to a given task.
- **Building a dataset incrementally**: start with 10-20 hand-written examples, graduate to
  real historical traces once the system is live, and only then consider synthetic data —
  this ordering matters because each stage catches different failure modes.
- **Evaluation vs. testing**: evals measure quality on a spectrum (how good), tests assert
  pass/fail correctness — conflating the two leads to either overly rigid evals or eval
  suites that never actually gate anything.
- Exercise: have the learner write a 10-example offline eval set for their own RAG/agent
  project (built in Modules 3/6) using code-based checks only, before introducing
  LLM-as-judge in the gap below — this forces the "can I check this without an LLM at all"
  question the source implicitly poses.

This lesson gives the concepts. It does not give LLM-as-judge calibration technique, a
framework comparison, or CI/CD wiring — those remain gaps below.

### Lesson 4.2 — LLM-as-judge, framework choice, CI/CD, calibration (GAP)

**GAP.** Every other candidate under "Evals" in `research/verified.md` is `EGRESS_BLOCKED`
or was screened out by genre without being opened.

What's specifically needed, by sub-topic:
1. **LLM-as-judge** — a verified primary source (from a framework vendor actually
   implementing it, e.g. DeepEval/Evidently) with concrete methodology and calibration
   guidance, not just a definitional overview.
2. **Framework comparison** — a verified, non-self-promotional comparison of eval
   frameworks/tools.
3. **Building eval datasets, official docs** — a verified, hands-on source (ideally official
   docs beyond LangSmith's) on constructing eval sets for agents/RAG specifically.
4. **CI/CD integration** — a verified source on wiring evals into deployment pipelines as a
   quality gate.
5. **Human-eval calibration** — a verified source on calibrating an LLM judge against human
   annotations, since this is the crux of trusting automated evals at all.

Candidate raw entries to re-check first (titles, under `research/raw/evals/`) — 4 flagged
"worth opening next" in `research/urls-to-verify.md`, plus 1 new candidate found via the
Lesson 4.1 source itself:
- "Your AI Product Needs Evals" (Hamel Husain — cited by LangSmith's own docs as a starting
  point; newly found, not from the original search pass) —
  `19-hamel-husain-your-ai-product-needs-evals.md`
- "Building Agent & LLM Evaluation Datasets" (MLflow docs — official docs) —
  `10-mlflow-docs-building-eval-datasets.md`
- "LLM Evaluation: Methods, Metrics, RAG & Agent Evals Guide" (Arize) —
  `12-arize-llm-evaluation-guide.md`
- "LLM-as-a-Judge: A Complete Guide to Using LLMs for Evaluations" (Evidently AI) —
  `04-evidentlyai-llm-as-a-judge-guide.md`
- "Illusions of the Gold Standard..." (arXiv, human-eval protocols) —
  `15-arxiv-illusions-of-the-gold-standard.md`

Other candidates (screened out by genre — vendor listicle/content-marketing — without being
opened; could be revisited if the topic still lacks material):
- "LLM-as-a-Judge in 2026: Top Evaluation Techniques and Best Practices" (DeepEval) —
  `03-deepeval-llm-as-a-judge-2026.md`
- "LLM-as-a-Judge: A Complete Guide to Using LLMs for Evaluations" (Evidently AI) —
  `04-evidentlyai-llm-as-a-judge-guide.md`
- "Top 5 LLM Evaluation Frameworks in 2026, Compared" (DeepEval) —
  `05-deepeval-top-5-llm-evaluation-frameworks.md`
- "Top 5 Agent Evaluation Tools in 2026" (MLflow) —
  `06-mlflow-top-5-agent-evaluation-tools.md`
- "Building Agent & LLM Evaluation Datasets" (MLflow docs — official docs, good verification
  candidate) — `10-mlflow-docs-building-eval-datasets.md`
- "Evaluation Concepts" (LangChain/LangSmith docs — official docs) —
  `11-langchain-docs-evaluation-concepts.md`
- "LLM Evaluation: Methods, Metrics, RAG & Agent Evals Guide" (Arize) —
  `12-arize-llm-evaluation-guide.md`
- "How to Calibrate Your LLM Judge With Human Annotations" (Galileo) —
  `14-galileo-calibrate-llm-judge-human-annotations.md`
- "Illusions of the Gold Standard: A Large-scale Analysis of Human Evaluation Protocols for
  Long-form Text Generation" (arXiv — academic, worth prioritizing) —
  `15-arxiv-illusions-of-the-gold-standard.md`
- "Online vs Offline AI Evals: When to Use Each" — `17-inngest-online-vs-offline-ai-evals.md`
- "Best AI Eval Tools for CI/CD Pipelines (2026 Review)" (Braintrust) —
  `16-braintrust-ai-eval-tools-cicd.md`
- "Prompt Regression Testing: Preventing Quality Decay" (Statsig) —
  `09-statsig-prompt-regression-testing.md`

---

## Module 5: Prompt Design & Iteration

**Prerequisites:** Module 1 (tokens/context windows inform prompt length budgeting).

**Learning objectives:**
- Apply core prompting techniques (explicitness, context, concrete examples, few-shot,
  chain-of-thought, prefill, format control, prompt chaining) and know when each is worth the
  added tokens/complexity.
- Recognize which "classic" prompting techniques (XML tags, explicit role prompting) are no
  longer load-bearing on current-generation models, per the model vendor's own guidance —
  and understand the industry shift from prompt engineering toward *context engineering*.
- Apply few-shot prompting correctly: know that example *format and label distribution*
  matter more than label correctness (Min et al. 2022), and recognize where few-shot breaks
  down (reasoning-heavy tasks).
- (Stretch, currently a GAP) Design system prompts with concrete before/after examples;
  compare structured-output mechanisms across vendors; use prompt-optimization tooling
  systematically rather than by ad hoc trial and error (connects to Module 4's eval-dataset
  sub-topic).

### Lesson 5.1 — Foundational technique: Anthropic's guide + few-shot prompting (SOURCED)

Verified sources:
- **Prompt engineering best practices for 2026 — Claude by Anthropic**
  https://claude.com/blog/best-practices-for-prompt-engineering — Quality A · Level:
  beginner → intermediate · Price: free · Time: ~1 hour · Verified 2026-09-11 (manual check)
  · Published 2025-11-10.
- **Few-Shot Prompting — Prompt Engineering Guide (DAIR.AI)**
  https://www.promptingguide.ai/techniques/fewshot — Quality A · Level: beginner · Price:
  free (material; the site's courses are paid) · Time: ~30 min this page, ~6-8 hours for the
  whole `techniques` section · Verified 2026-09-11 (manual check).

Teach these two together:
- From Anthropic's guide: the basic technique set (explicitness, context, concreteness,
  examples, permission to say "I don't know"), the advanced set (prefill, three kinds of
  chain-of-thought, output-format control, prompt chaining), and — just as important — the
  explicit "what's no longer necessary" section: XML tags and explicit role prompting are not
  required on current models the way older guidance suggested. Use its "need → technique"
  table and its list of common mistakes directly as a lesson worksheet. Flag the framing
  shift it names explicitly: prompt engineering → *context engineering* (see also the GAP
  note in `CORE.md` Module 1 Lesson 1.2, and the new candidate source
  `research/raw/prompt-engineering/19-anthropic-effective-context-engineering.md`, found via
  this same post but not yet independently verified).
- From the Prompt Engineering Guide: few-shot prompting grounded in Brown et al. 2020, then
  immediately complicated by Min et al. 2022's finding that example *format* and *label
  distribution* drive the benefit more than whether the labels are individually correct —
  teach this as a caution against over-trusting few-shot on faith. Also teach where few-shot
  demonstrably fails (multi-step reasoning tasks), setting up chain-of-thought as the next
  tool rather than "more examples."
- Exercise: take one real prompt from the learner's own project (from Module 3 or 6) and
  apply the "need → technique" table to justify one concrete change, then verify token-cost
  impact using the Module 1 tokenizer skill.
- New, not-yet-verified candidate found via Anthropic's own site, high priority for the next
  verification pass since GitHub is already reachable: Anthropic's own interactive prompting
  tutorial repo — `research/raw/prompt-engineering/20-anthropic-prompt-eng-interactive-tutorial.md`
  (https://github.com/anthropics/prompt-eng-interactive-tutorial).

This covers foundational technique and few-shot specifically. System prompt design detail,
structured output across vendors, and optimization tooling remain gaps below.

### Lesson 5.2 — System prompt design, structured output, optimization tooling (GAP)

**GAP.** Every other candidate under "Проектирование промптов" in `research/verified.md` is
`EGRESS_BLOCKED` or was screened out by genre without being opened.

What's specifically needed, by sub-topic:
1. **System prompt design** — a verified source with concrete before/after examples, not
   just a bullet list of tips.
2. **Structured output** — a verified source comparing JSON-mode/structured-output
   mechanisms across providers.
3. **Prompt optimization tooling** — a verified, non-listicle source on systematic prompt
   iteration/optimization.
4. **Vendor-specific prompting guides beyond Anthropic** (OpenAI, Google) — inherently a
   CURRENT-layer concern; see `CURRENT.md`.

Candidate raw entries to re-check first (titles, under `research/raw/prompt-engineering/`) —
5 flagged "worth opening next" in `research/urls-to-verify.md` (the OpenAI/Google
vendor guides belong in `CURRENT.md` once sourced, not here, since they track specific model
versions):
- "Codex Prompting Guide" (OpenAI developers — first-party) —
  `12-openai-codex-prompting-guide.md`
- "GPT-5.5 prompting guide" (Simon Willison — reputable independent practitioner) —
  `11-simonwillison-gpt55-prompting-guide.md`
- "Gemini 3 developer guide" (Google AI for Developers — first-party) —
  `14-google-gemini3-developer-guide.md`
- "Zero-Shot vs Few-Shot prompting: A Guide with Examples" (Vellum) —
  `16-vellum-zero-shot-vs-few-shot.md`
- "promptolution: A Unified, Modular Framework for Prompt Optimization" (arXiv) —
  `10-arxiv-promptolution-framework.md`

Also newly found via the Lesson 5.1 sources (not yet verified, see
`research/urls-to-verify.md`): Anthropic's "Effective context engineering for AI agents" and
Anthropic's own interactive prompting tutorial repo (both cited in Lesson 5.1 above).

The remaining raw candidates for this sub-topic (IBM's guide, orq's CoT guide, buildmvpfast's
system-prompt piece, crazyrouter's structured-output guide, futureagi's optimization-tools
listicle) were screened out by genre (content-marketing / unexplained listicle) without being
opened — see `research/urls-to-verify.md` for the full reasoning; revisit only if the above
five don't fill this gap.

---

## Module 6: Agents & Tool Use

**Prerequisites:** Module 5 (agents issue prompts) and, ideally, Module 2/3 (retrieval as a
tool an agent can call).

**Learning objectives:**
- Explain what distinguishes an "agent" from a single LLM call: a loop, tool calls, and
  (often) memory/state across turns.
- Understand the Model Context Protocol (MCP) as the emerging standard for exposing tools to
  agents, including its current architectural direction.
- Recognize the concrete security exposure that opening "reading" tools into "acting" tools
  creates, and name first-line mitigations.
- (Stretch, currently a GAP) Compare agent architectures/patterns (ReAct, plan-and-execute,
  multi-agent orchestration) and major frameworks.

### Lesson 6.1 — Model Context Protocol: current direction & specification (SOURCED)

Verified sources:
- **The 2026 MCP Roadmap** — https://blog.modelcontextprotocol.io/posts/2026-mcp-roadmap/ —
  Quality A · Level: intermediate · Price: free · Time: ~6 min read · Verified 2026-09-10.
  Authored by David Soria Parra (Lead Maintainer). Covers four 2026 priority areas for MCP:
  transport scalability, agent-to-agent communication, governance maturation, and enterprise
  readiness — plus concrete production gaps the protocol is closing (load balancing, session
  state) and the Working Group/SEP process for how the spec evolves.
- **The 2026-07-28 Specification (Model Context Protocol)** —
  https://blog.modelcontextprotocol.io/posts/2026-07-28/ — Quality A · Level: advanced ·
  Price: free · Time: ~12 min read · Verified 2026-09-10. Concrete technical content: a move
  to a stateless protocol core, Multi Round-Trip Requests, header-based routing
  (`Mcp-Method`/`Mcp-Name`), cacheable list results, RFC 9207 authorization hardening, and
  adoption numbers (TypeScript/Python SDKs each over 1B downloads).

Teach these two together as a single unit: the roadmap gives the "why" (what production gaps MCP
is closing), the spec post gives the "what" (the concrete mechanisms — statelessness,
routing headers, caching, auth hardening). This is enough to give a learner a real
understanding of MCP as of mid/late-2026, but it is **not** a substitute for a from-scratch
"what is an agent" or "what is a tool call" primer — that foundational layer is a gap (see
6.2 below). Sequence this lesson only after the learner already has *some* notion of agents/
tool calling in general, even an informal one, since these two sources assume that context.

### Lesson 6.2 — Agent fundamentals, architectures & frameworks (GAP)

**GAP.** No verified source teaches "what is an agent loop", ReAct vs. plan-and-execute,
multi-agent orchestration, or framework choice (LangGraph/CrewAI/AutoGen/Claude Agent SDK/
OpenAI Agents SDK). Everything under this sub-topic in `research/verified.md` is
`EGRESS_BLOCKED`.

What's specifically needed:
1. A verified, foundational explainer of the agent loop (perceive → reason → act) and
   function/tool calling mechanics, framework-agnostic.
2. A verified comparison of agent architectures (ReAct, plan-and-execute) with concrete
   tradeoffs, not just definitions.
3. A verified, even-handed framework comparison (LangGraph vs. CrewAI vs. AutoGen, and
   ideally the vendor-native Claude Agent SDK / OpenAI Agents SDK).
4. A verified source on multi-agent system design — when orchestrating multiple agents is
   worth the added complexity vs. a single agent with more tools (Anthropic's own posts on
   this exact question would be ideal primary sources if reachable).
5. A verified source on agent evaluation metrics specifically (tool-calling accuracy, task
   completion, trace-based evals) — this is also a Module 4 dependency.

Candidate raw entries to re-check first (titles, under `research/raw/agents-tool-use/`):
- "AI Agent Architecture: Build Systems That Work in 2026" (Redis) —
  `01-ai-agent-architecture-redis.md`
- "Types of AI Agent Architectures: 2026 Developer Guide" (MLflow) —
  `02-mlflow-agent-architecture-types.md`
- "LLM Function Calling 2026: Tool Use Across Providers" —
  `03-llm-function-calling-2026.md`
- "The Evolution of Tool Use in LLM Agents: From Single-Tool Call to Multi-Tool
  Orchestration" (arXiv) — `04-evolution-tool-use-multi-tool-orchestration.md`
- "Multi-Agent AI Systems in 2026: Frameworks, Patterns, Production" —
  `05-multi-agent-frameworks-2026-futureagi.md`
- "LangGraph vs CrewAI vs AutoGen: Which AI Agent Framework Should Your Enterprise Use in
  2026?" — `08-langgraph-crewai-autogen-comparison.md`
- "Building Production-Ready AI Agents in 2026" (MLflow) —
  `09-mlflow-production-ready-agents.md`
- "AI Agent Frameworks (2026 Update): 8 SDKs Compared + the Claude Agent SDK Primitive
  Reference" — `11-claude-agent-sdk-comparison-morphllm.md`
- "The next evolution of the Agents SDK" (OpenAI — first-party) —
  `12-openai-agents-sdk-next-evolution.md`
- "ReAct vs Plan-and-Execute: A Practical Comparison of LLM Agent Patterns" —
  `15-react-vs-plan-and-execute.md`
- "LLM Agent Evaluation Metrics in 2026: Tool Calling, Task Completion, Reasoning, and
  Trace-Based Evals" — `16-agent-evaluation-metrics-confident-ai.md`
- "Google's Agent2Agent Protocol Explained" — `17-google-a2a-protocol-galileo.md`
- "How Anthropic Built a Multi-Agent Research System" (Anthropic-sourced content via a
  third-party republish — re-check whether Anthropic's own original post is reachable
  instead) — `18-anthropic-multi-agent-research-system.md`
- "When to use multi-agent systems (and when not to)" (Claude/Anthropic — first-party, top
  priority to re-check) — `20-anthropic-when-to-use-multi-agent-systems.md`
- "State of AI Agent Memory 2026: Benchmarks & Trends Report" —
  `10-state-of-ai-agent-memory-2026.md`

---

## Module 7: Cost & Latency

**Prerequisites:** Module 1 (tokens), Module 3 and/or 6 (something built worth optimizing).

**Learning objectives (intended scope, not yet sourced):**
- Reason about the token-cost relationship established in Module 1 at a system level
  (prompt design, RAG context size, and agent tool-call chains all multiply cost).
- Understand prompt caching as a first-line cost/latency lever.
- Understand model routing/cascading (sending easy queries to a cheap/fast model, escalating
  hard ones) as a production pattern.
- Understand inference-side levers an application engineer should at least recognize
  (quantization, speculative decoding, distillation) even without owning the serving stack.
- Monitor token usage/spend in production.

### Lesson content: GAP (entire module)

**GAP — no verified sources at all.** Zero verified entries under "Стоимость и
латентность" in `research/verified.md`; every candidate blocked as `EGRESS_BLOCKED`.

What's specifically needed, by sub-topic:
1. **Prompt caching** — a verified source with concrete mechanics (what invalidates a
   cache, how to structure prompts to maximize cache hits) — ideally a model vendor's own
   docs.
2. **Model routing/cascading** — a verified source, ideally with a worked cost/quality
   tradeoff example, not just "route smart."
3. **Latency budgets (TTFT/ITL/P99)** — a verified source explaining these metrics
   concretely for LLM inference specifically.
4. **Speculative decoding, quantization, distillation** — verified sources at a level an
   application engineer needs (recognize the technique and its tradeoffs, not implement an
   inference server).
5. **Pricing/cost comparison across providers** — inherently a CURRENT-layer concern once
   sourced, since prices change constantly.
6. **Token usage monitoring / LLM observability tooling** — a verified, non-self-promotional
   source.

Candidate raw entries to re-check first (titles, under `research/raw/cost-latency/`):
- "LLM Cost Optimization Strategies: Complete Tactics List [2026]" (Atlan) —
  `01-llm-cost-optimization-strategies-atlan.md`
- "Reduce LLM Cost and Latency: A Comprehensive Guide for 2026" (getmaxim.ai) —
  `02-reduce-llm-cost-latency-maxim.md`
- "LLM Inference SLO Engineering: TTFT, ITL, and P99 Latency Budgets for Production AI
  (2026)" — `04-inference-slo-engineering-spheron.md`
- "Prompt Caching in 2026: Cut LLM Costs, Keep Quality" —
  `06-prompt-caching-guide-digitalapplied.md`
- "LLM Prompt Caching: Cost Savings, Invalidation & Workload Design" —
  `07-prompt-caching-intuitionlabs.md`
- "Cluster, Route, Escalate: Cascaded Framework for Cost-Aware LLM Serving" (arXiv) —
  `08-cluster-route-escalate-arxiv.md`
- "Dynamic Model Routing and Cascading for Efficient LLM Inference: A Survey" (arXiv) —
  `09-model-routing-cascading-survey-arxiv.md`
- "LLM Model Routing: Route Queries to the Right Model Automatically" —
  `10-llm-model-routing-neuraltrust.md`
- "Speculative Decoding: 2-3x Faster LLM Inference (2026)" —
  `11-speculative-decoding-premai.md`
- "How speculative decoding delivers faster LLM inference" (Red Hat Developers) —
  `12-speculative-decoding-redhat.md`
- "LLM Inference Cost Comparison 2026" (DigitalOcean — treat as CURRENT-layer once sourced)
  — `13-llm-inference-cost-comparison-digitalocean.md`
- "Token Usage Monitoring: Track, Attribute, and Optimise AI Spend" —
  `15-token-usage-monitoring-neuraltrust.md`
- "Best LLM monitoring tools in 2026 (tested & reviewed)" (Braintrust) —
  `16-best-llm-monitoring-tools-braintrust.md`
- "Model Distillation for LLMs: Cut Costs & Boost Speed in 2026" (Redis) —
  `20-model-distillation-redis.md`
- "Distillation with Programmatic Data Curation: Smarter LLMs, 5-30x Cheaper Inference"
  (TensorZero) — `21-distillation-programmatic-data-tensorzero.md`

---

## Module 8: Prompt Injection & Security

**Prerequisites:** Module 6 (the attack surface this module teaches is specifically tools/
retrieval feeding untrusted content into an agent's context).

**Learning objectives:**
- Distinguish direct prompt injection from indirect prompt injection (injected via retrieved
  documents, tool output, web content).
- Recognize the concrete "reading tool becomes acting tool" risk pattern in agentic systems.
- Distinguish prompt injection from jailbreaking as related-but-different threat categories.
- Name first-line mitigations and detection points for a production agent (connects to
  Module 6's MCP material and Module 4's evals, since injection resistance is itself
  something to eval for).

### Lesson 8.1 — Tool-metadata poisoning: a worked example (SOURCED)

Verified source:
- **Securing AI agents: When AI tools move from reading to acting** —
  https://www.microsoft.com/en-us/security/blog/2026/06/30/securing-ai-agents-ai-tools-move-from-reading-acting/
  — Quality A · Level: intermediate · Price: free · Time: ~6 min read · Verified
  2026-09-10. (Catalogued under "Агенты и tool use" in `research/verified.md` since that is
  where it was verified, but its content is squarely a prompt-injection/agent-security
  lesson — it is cited here for that reason, and cross-referenced from Module 6.)

Teach directly from this post:
- The concrete worked example: an MCP tool-metadata poisoning attack against a Copilot
  Studio invoice agent — i.e., injected instructions hidden in tool *metadata* (not just
  document content) that get executed once the agent trusts the tool description.
- The four control points it names as mitigations, plus the specific detection tooling it
  cites (Microsoft Purview, Microsoft Sentinel).
- Use this as the anchor case for teaching the general pattern: any content an agent reads
  (tool descriptions, retrieved documents, web pages, API responses) is untrusted input and
  a potential injection vector the moment that agent can also *act* (send email, call a
  paid API, modify data).

This one worked example is not sufficient on its own to teach the full breadth of prompt
injection (direct injection, jailbreak-vs-injection distinction, defense-in-depth
architectures, benchmarks) — those remain gaps below.

### Lesson 8.2 — Indirect injection in the wild: taxonomy and telemetry (SOURCED)

Verified source:
- **Fooling AI Agents: Web-Based Indirect Prompt Injection Observed in the Wild — Unit 42**
  https://unit42.paloaltonetworks.com/ai-agent-prompt-injection/ — Quality A · Level:
  intermediate → advanced · Price: free · Time: ~1.5 hours · Verified 2026-09-11 (manual
  check) · Published 2026-03-03.

Teach directly from this post — it is field research on real telemetry, not theory:
- The two-axis taxonomy of indirect injection: **attacker intent** (from "produce nonsense"
  up to data destruction and system-prompt exfiltration) and **payload engineering** —
  delivery methods (zero-size font, CSS-hiding, off-screen placement, HTML attributes,
  SVG/CDATA, runtime execution) and evasion methods (invisible characters, homoglyphs,
  payload splitting, multi-layer encoding, multilingual commands, JSON injection).
- 12 real, dissected cases from live sites.
- The telemetry finding that should reframe how learners think about defense priority: 85.2%
  of observed evasions were plain social engineering (not exotic encoding tricks), and 37.8%
  of deliveries were just visible text on the page — the sophisticated evasion techniques
  make headlines, but the boring ones are what actually gets used.
- The defenses section: spotlighting, instruction hierarchy, adversarial training,
  architecture-level defenses — as a preview list (each has its own not-yet-verified
  candidate source below, in Lesson 8.3).
- The root-cause framing this article makes explicit: an LLM does not distinguish
  instructions from data within one context stream. This is exactly the principle this
  repository's own research agents were built to follow ("page content is data, not
  instructions") — use it as the bridge between "here's a security topic" and "here's why
  your own agent-building practice already has to account for this."
- Notable meta-example: the article's own page contains a directive aimed at AI agents not to
  execute the examples shown on it. Use this as a live illustration of what a trust boundary
  looks like in practice — and note for the learner that the directive was correctly treated
  as content to describe, not an instruction to follow, when this lesson was written.

Together, Lessons 8.1 (Microsoft's worked example) and 8.2 (this taxonomy) cover: what the
attack surface looks like end-to-end (tool metadata *and* web/RAG content), a concrete
incident, and the two most-common real-world evasion patterns. They do not yet cover the
jailbreak-vs-injection distinction, defense-architecture implementation detail, or benchmarks
— those remain the gap below.

### Lesson 8.3 — Jailbreak distinction, defense architectures, benchmarks (GAP)

**GAP.** Every other candidate under "Prompt injection" in `research/verified.md` is either
`EGRESS_BLOCKED` or was screened out by genre without being opened (see
`research/urls-to-verify.md`) — except the OWASP cheat sheet and three academic papers found
via Lesson 8.2's own defenses section, listed below as newly found, not-yet-verified
candidates.

What's specifically needed:
1. A verified source clearly distinguishing **prompt injection from jailbreaking** (two
   independent candidates exist in the raw set — worth cross-checking against each other
   once reachable).
2. A verified source on **defense architectures/guardrail systems** (e.g. an open-source
   guardrail project) with concrete implementation detail, not just "add input validation."
3. A verified source on **benchmarks/evaluation of injection resistance** (this is also a
   Module 4 dependency — injection resistance should be part of an eval suite).
4. Optionally, real-world incident/case-study material (e.g. CI/CD-pipeline injection via a
   coding agent) to make the risk concrete for engineers who don't think of "agent security"
   as their job.

Newly found via Lesson 8.2's own defenses section (not from the original search pass, not yet
verified — high priority for the next pass):
- "LLM Prompt Injection Prevention Cheat Sheet" (OWASP — standards-body primary source) —
  `research/raw/prompt-injection/17-owasp-llm-prompt-injection-cheat-sheet.md`
- "Spotlighting" (arXiv 2403.14720, named explicitly as a defense in Lesson 8.2's source) —
  `research/raw/prompt-injection/18-spotlighting-arxiv-2403.14720.md`
- "The Instruction Hierarchy" (arXiv 2404.13208, named explicitly in Lesson 8.2's source) —
  `research/raw/prompt-injection/19-instruction-hierarchy-arxiv-2404.13208.md`
- "Design-level defenses against prompt injection" (arXiv 2503.18813) —
  `research/raw/prompt-injection/20-design-level-defenses-arxiv-2503.18813.md`
- "Adversarial Prompting" section, same Prompt Engineering Guide as the verified Lesson 5.1
  few-shot page — `research/raw/prompt-injection/16-promptingguide-adversarial-prompting.md`

Candidate raw entries from the original search pass to re-check first (titles, under
`research/raw/prompt-injection/`) — 10 flagged "worth opening next" in
`research/urls-to-verify.md`:
- "Indirect Prompt Injection: The Hidden Threat Breaking Modern AI Systems" (Lakera) —
  `05-lakera-indirect-prompt-injection.md`
- "Indirect Prompt Injection Attacks: Hidden AI Risks" (CrowdStrike) —
  `07-crowdstrike-indirect-prompt-injection.md`
- "LlamaFirewall: An Open Source Guardrail System for Building Secure AI Agents" (arXiv —
  concrete open-source system, strong candidate for implementation-level teaching) —
  `14-llamafirewall.md`
- "PIArena: A Platform for Prompt Injection Evaluation" (arXiv, benchmark) —
  `03-piarena-benchmark.md`
- "LongPIBench: A Long-Context Benchmark for Prompt Injection" (arXiv, benchmark) —
  `04-longpibench.md`
- "Agent Data Injection Attacks are Realistic Threats to AI Agents" (arXiv) —
  `08-agent-data-injection-attacks.md`
- "GitInject: Real-World Prompt Injection Attacks in AI-Powered CI/CD Pipelines" (arXiv —
  concrete incident-style material, good for making the risk real) — `10-gitinject-cicd.md`
- "The Promptware Kill Chain: How Prompt Injections Gradually Evolved Into a Multistep
  Malware Delivery Mechanism" (arXiv) — `11-promptware-kill-chain.md`
- "Prompt Injection vs. Jailbreaking: What's the Difference?" (learnprompting.org) —
  `12-learnprompting-injection-vs-jailbreaking.md`
- "Prompt Injection vs Jailbreaking: What's the Difference?" (Promptfoo — cross-check
  against the above for agreement) — `13-promptfoo-injection-vs-jailbreaking.md`

Screened out by genre without opening (content-marketing / legal, not a technical-content
signal): getmaxim.ai's defense guide, Sysdig's guide, Snowflake's guardrails post (vendor
content-marketing), ktslaw's litigation-risk alert (legal, not instructional) — see
`research/urls-to-verify.md`.

---

## Module 9: Interview Readiness

**Prerequisites:** all preceding modules — this is explicitly a capstone/review layer, not
new technical content.

**Design decision (11.09.2026):** this module is deliberately **not** built as a question
bank, even where verified question-list sources might eventually exist. Rationale: the "45+
questions with answers" genre teaches memorized phrasing, not understanding — and memorized
answers collapse on the first follow-up question, which is exactly what an interviewer probes
for. This is doubly true for a candidate whose interview will center on a take-home/test
project: that interview is structured around *your own code and the decisions you made*, not
a generic question bank. So Module 9 is redesigned around **defending your own project**
instead. See `research/urls-to-verify.md` → "Тема «Вопросы на собеседованиях»" for the full
reasoning and the disposition of all 20 raw candidates in that topic.

**Learning objectives:**
- Give a clear, structured walkthrough of your own project (built across Modules 1-8): what
  it does, why you made the architecture choices you made, and what you'd change with more
  time.
- Defend specific decisions under questioning: why this chunking/retrieval approach and not
  another (Module 3), why this model/prompting strategy (Modules 1, 5), what your evals
  actually check and don't check (Module 4), what your cost/latency profile looks like and
  where the next bottleneck is (Module 7), what your threat model is for prompt injection
  given what the project actually does (Module 8).
- Handle scaling/what-if questions with a reasoned estimate rather than a guess: "what if
  load grows 100x", "what if this needs to run 10x cheaper", "what's the first thing that
  breaks and how would you know."
- Practice articulating tradeoffs, since every prior module has one at its center (RAG vs.
  long-context, single-agent vs. multi-agent, judge-based vs. reference-based evals,
  cache-friendly vs. flexible prompt structure) — a strong answer names the tradeoff and the
  reason for the specific choice, not just the choice.

### Lesson 9.1 — Structured project walkthrough & defense (methodology, no external source needed)

This lesson is a facilitation structure, not a set of readings — it doesn't need an external
citation because it is built entirely from what the learner already produced in Modules 1-8,
plus general interview-coaching practice (connective narrative, per this curriculum's rules,
since no concrete "resource" is being pointed to).

Run it as a mock interview with four fixed rounds, each keyed to specific prior modules:
1. **The pitch (2-3 min).** Learner explains the project like they would to a hiring manager
   who hasn't seen the code: what it does, for whom, and the one or two decisions they're
   proudest of.
2. **The architecture drill-down.** Interviewer picks one component (retrieval, prompting,
   an agent tool, the eval harness) and asks "why this, not X" until the learner reaches a
   real constraint (cost, latency, data availability, time) rather than "it's the popular
   choice." Directly exercises the tradeoff-articulation objective above.
3. **The scaling/failure round.** Interviewer asks 2-3 what-if questions calibrated to the
   project's actual stack (e.g. "your vector DB now has 100x the documents — what breaks
   first and what do you change," "a user reports the agent leaked something it
   shouldn't've — walk me through how you'd find out why"). Answers should reference the
   learner's own Module 7 cost/latency reasoning and Module 8 threat model, not a generic
   scaling playbook.
4. **The retrospective.** "What would you do differently with another week / with 10x the
   budget / if this had to support 100 more users tomorrow." Tests whether the learner
   actually understands their own tradeoffs or just made choices by default.

Have the learner keep a one-page "decision log" while building the Modules 3/5/6/8 projects
(each entry: decision, alternatives considered, why this one) — Round 2 and Round 3 both draw
directly from this log, and building it is itself good practice for interviews that ask "walk
me through a decision you made."

### Lesson 9.2 — Optional supplementary material (unverified, use with caution)

Not required for Lesson 9.1, and deliberately not built into the core methodology above (see
the design decision at the top of this module). If a learner wants extra exposure to how
generative-AI system-design questions are typically framed, these raw candidates are flagged
"worth opening next" in `research/urls-to-verify.md` — they lean toward system-design
case-style material rather than pure question-and-answer lists, but are **not yet verified**:
- "Generative AI System Design Interview: 2026 Guide" —
  `research/raw/ai-engineer-interview-questions/09-systemdesignhandbook-genai-system-design-guide.md`
- "AI System Design Interview Questions (2026)" —
  `research/raw/ai-engineer-interview-questions/10-systemdesignhandbook-ai-system-design-questions.md`
- "Machine Learning System Design Interview (2026 Guide)" (Exponent) —
  `research/raw/ai-engineer-interview-questions/12-exponent-ml-system-design-interview-guide.md`
- "The Complete Agentic AI System Design Interview Guide 2026" —
  `research/raw/ai-engineer-interview-questions/11-medium-agentic-ai-system-design-guide.md`
- "7 RAG & Agent System Design Questions..." —
  `research/raw/ai-engineer-interview-questions/14-towardsai-rag-agent-system-design-questions.md`
- "Design and optimize a RAG system | OpenAI Interview Question" (claims real-interview
  provenance — check that claim before trusting it) —
  `research/raw/ai-engineer-interview-questions/19-prachub-design-optimize-rag-system.md`
- "45+ AI Engineer Interview Questions" (UPenn Career Services, Aced/Exponent) and "100+ Real
  Interviews" (Medium) — three sources claiming institutional/real-interview provenance,
  worth checking that claim specifically rather than treating them as generic listicles —
  `research/raw/ai-engineer-interview-questions/01-upenn-ai-engineer-interview-questions.md`,
  `03-exponent-ai-engineer-interview-questions.md`, `02-medium-100-real-interviews-ai-engineer.md`

The other 11 raw candidates in this topic were screened out entirely (pure "N questions with
answers" listicles) — see `research/urls-to-verify.md` for the list and reasoning.

---

## Summary table

| # | Module | Verified sources | Status |
|---|---|---|---|
| 0 | Orientation | 0 (see CURRENT.md) | meta / non-graded |
| 1 | LLM Fundamentals & Tokenization | 1 (tiktoken) | **partial** — tokenization mechanics sourced; sampling/context/attention/KV-cache is a GAP |
| 2 | Embeddings & Vector Search | 1 (HNSW) | **partial** — vector index mechanics sourced; model selection/hybrid search/chunking/reranking is a GAP |
| 3 | Retrieval-Augmented Generation | 0 | **GAP** (entire module) |
| 4 | Evaluation (Evals) | 1 (LangSmith evaluation concepts) | **partial** — core concepts sourced; LLM-as-judge/frameworks/CI/CD/calibration is a GAP |
| 5 | Prompt Design & Iteration | 2 (Anthropic best practices, Few-Shot Prompting Guide) | **partial** — foundational technique + few-shot sourced; system prompt design/structured output/optimization tooling is a GAP |
| 6 | Agents & Tool Use | 3 (2 MCP posts + 1 shared with Module 8) | **partial** — MCP protocol sourced; agent fundamentals/architectures/frameworks is a GAP |
| 7 | Cost & Latency | 0 | **GAP** (entire module) |
| 8 | Prompt Injection & Security | 2 (Microsoft worked example, shared with Module 6; Unit 42 taxonomy) | **partial** — worked example + real-world taxonomy sourced; jailbreak distinction/defense architectures/benchmarks is a GAP |
| 9 | Interview Readiness | 0, by design | **redesigned** — self-contained "defend your own project" methodology, not a GAP; question-bank sources deliberately excluded (see module text) |

Note: the Microsoft security post is counted once as a verified source but used in two
modules (6 and 8) because its content genuinely serves both — that is a deliberate citation
choice, not double-counting toward the "12 verified sources" total in `research/verified.md`
(7 from the automated pass, 5 added in the manual follow-up pass of 11.09.2026).
