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

**Learning objectives (intended scope, not yet sourced):**
- Explain what an embedding is and why semantic similarity is computed via vector distance.
- Choose an embedding model appropriately (dimensionality, domain fit, cost) for a given
  task.
- Understand approximate nearest-neighbor search at a conceptual level (specifically HNSW,
  the dominant production index type) well enough to reason about recall/latency tradeoffs.
- Understand hybrid search (combining sparse/BM25 with dense vector retrieval) and why pure
  vector search under-performs on exact-match/keyword-heavy queries.
- Understand chunking strategy as a first-order lever on retrieval quality.

### Lesson content: GAP (entire module)

**GAP — no verified sources at all.** `research/verified.md` records zero verified entries
under "Эмбеддинги и векторный поиск"; every candidate is blocked as `EGRESS_BLOCKED`. Per
the hard rules, no lesson content is written here — an unsourced explainer would be
fabrication dressed as a lesson.

What's specifically needed, by sub-topic:
1. **Embedding model selection** — a verified, non-listicle comparison with actual benchmark
   methodology (not just a ranked table) covering open-source and API-based embedding
   models.
2. **Vector index mechanics (HNSW)** — a verified walkthrough with a worked example of how
   HNSW builds/searches a graph, at a level an application engineer (not an ANN researcher)
   needs.
3. **Hybrid search** — a verified source with concrete implementation guidance for combining
   BM25 and dense retrieval (fusion method, e.g. RRF), ideally with a worked example.
4. **Chunking strategy** — a verified source comparing chunking methods with actual code,
   not just named strategies.
5. **Reranking** — a verified source explaining cross-encoder rerankers and when they're
   worth the added latency.

Candidate raw entries to re-check first (titles, under
`research/raw/embeddings-vector-search/`):
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

**Learning objectives (intended scope, not yet sourced):**
- Explain why evals matter for LLM applications specifically (non-determinism, no single
  ground truth, regressions from prompt/model changes).
- Distinguish LLM-as-judge from rule-based/reference-based metrics and know the failure modes
  of each (judge bias, calibration drift).
- Build an offline eval dataset and distinguish online vs. offline evaluation.
- Wire evals into CI/CD as a regression gate for prompt/model changes.
- Apply RAG-specific and agent-specific eval metrics (this sub-topic is a direct dependency
  from Modules 3 and 6).

### Lesson content: GAP (entire module)

**GAP — no verified sources at all.** Zero verified entries under "Evals" in
`research/verified.md`; every candidate blocked as `EGRESS_BLOCKED`.

What's specifically needed, by sub-topic:
1. **LLM-as-judge** — a verified primary source (from a framework vendor actually
   implementing it, e.g. DeepEval/Evidently) with concrete methodology and calibration
   guidance, not just a definitional overview.
2. **Framework comparison** — a verified, non-self-promotional comparison of eval
   frameworks/tools.
3. **Building eval datasets** — a verified, hands-on source (ideally official docs) on
   constructing eval sets for agents/RAG.
4. **CI/CD integration** — a verified source on wiring evals into deployment pipelines as a
   quality gate.
5. **Online vs. offline evals** — a verified source distinguishing the two with concrete
   guidance on when each applies.
6. **Human-eval calibration** — a verified source on calibrating an LLM judge against human
   annotations, since this is the crux of trusting automated evals at all.

Candidate raw entries to re-check first (titles, under `research/raw/evals/`):
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

**Learning objectives (intended scope, not yet sourced):**
- Apply core prompting techniques (zero-shot vs. few-shot, chain-of-thought, structured
  output) and know when each is worth the added tokens/complexity.
- Design system prompts for a specific task/persona with explicit constraints.
- Understand vendor-specific prompting differences (this is inherently a CURRENT-layer
  concern, since it tracks specific model versions).
- Iterate on prompts systematically rather than by ad hoc trial and error (connects forward
  to Module 4's prompt-regression-testing sub-topic).

### Lesson content: GAP (entire module)

**GAP — no verified sources at all.** Zero verified entries under "Проектирование
промптов" in `research/verified.md`; every candidate blocked as `EGRESS_BLOCKED` — including
what would otherwise be an obvious Quality-A pick, Anthropic's own "Prompt engineering best
practices" post, which could not be fetched in this session despite being a first-party
vendor source.

What's specifically needed, by sub-topic:
1. **Foundational technique** — a verified primary source (ideally a model vendor's own
   prompting guide) covering zero-shot/few-shot, chain-of-thought, and structured output.
2. **System prompt design** — a verified source with concrete before/after examples, not
   just a bullet list of tips.
3. **Chain-of-thought specifics** — a verified source explaining when CoT helps vs. hurts
   (latency/cost tradeoff, and modern models where explicit CoT prompting may already be
   less necessary).
4. **Structured output** — a verified source comparing JSON-mode/structured-output
   mechanisms across providers.
5. **Prompt optimization tooling** — a verified, non-listicle source on systematic prompt
   iteration/optimization.

Candidate raw entries to re-check first (titles, under `research/raw/prompt-engineering/`):
- "Prompt engineering best practices for 2026" (Anthropic/Claude — first-party, top
  priority to re-check) — `01-anthropic-claude-prompting-best-practices.md`
- "The 2026 Guide to Prompt Engineering" (IBM) — `02-ibm-2026-guide-prompt-engineering.md`
- "Codex Prompting Guide" (OpenAI developers — first-party) —
  `12-openai-codex-prompting-guide.md`
- "GPT-5.5 prompting guide" (Simon Willison — reputable independent practitioner) —
  `11-simonwillison-gpt55-prompting-guide.md`
- "Gemini 3 developer guide" (Google AI for Developers — first-party) —
  `14-google-gemini3-developer-guide.md`
- "Chain of Thought Prompting in AI: A Comprehensive Guide [2026]" —
  `06-orq-chain-of-thought-comprehensive-guide.md`
- "System Prompt Design Best Practices" — `05-buildmvpfast-system-prompt-design-best-practices.md`
- "AI Structured Output Guide 2026: JSON Mode Across OpenAI, Claude, and Gemini" —
  `08-crazyrouter-structured-output-guide.md`
- "Few-Shot Prompting" (promptingguide.ai) — `15-promptingguide-few-shot.md`
- "Zero-Shot vs Few-Shot prompting: A Guide with Examples" (Vellum) —
  `16-vellum-zero-shot-vs-few-shot.md`
- "Top 10 Prompt Optimization Tools in 2026" — `09-futureagi-top-10-prompt-optimization-tools.md`

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

### Lesson 8.2 — Direct injection, jailbreak distinction, defenses, benchmarks (GAP)

**GAP.** Every other candidate under "Prompt injection" in `research/verified.md` is
`EGRESS_BLOCKED`.

What's specifically needed:
1. A verified source clearly distinguishing **prompt injection from jailbreaking** (two
   independent candidates exist in the raw set — worth cross-checking against each other
   once reachable).
2. A verified source on **indirect prompt injection** specifically (web-based / RAG-context-
   based) beyond the single Microsoft worked example above — ideally from a security vendor
   with its own incident data (Palo Alto Unit 42, CrowdStrike).
3. A verified source on **defense architectures/guardrail systems** (e.g. an open-source
   guardrail project) with concrete implementation detail, not just "add input validation."
4. A verified source on **benchmarks/evaluation of injection resistance** (this is also a
   Module 4 dependency — injection resistance should be part of an eval suite).
5. Optionally, real-world incident/case-study material (e.g. CI/CD-pipeline injection via a
   coding agent) to make the risk concrete for engineers who don't think of "agent security"
   as their job.

Candidate raw entries to re-check first (titles, under `research/raw/prompt-injection/`):
- "Prompt Injection Defense for Production AI Agents: A Complete 2026 Guide" —
  `01-prompt-injection-defense-production-agents.md`
- "The Comprehensive Guide to Prompt Injection Attacks in 2026" (Sysdig) —
  `02-sysdig-comprehensive-guide.md`
- "Indirect Prompt Injection: The Hidden Threat Breaking Modern AI Systems" (Lakera) —
  `05-lakera-indirect-prompt-injection.md`
- "Fooling AI Agents: Web-Based Indirect Prompt Injection Observed in the Wild" (Palo Alto
  Unit 42 — vendor with real incident telemetry, good candidate) —
  `06-unit42-fooling-ai-agents.md`
- "Indirect Prompt Injection Attacks: Hidden AI Risks" (CrowdStrike) —
  `07-crowdstrike-indirect-prompt-injection.md`
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
- "LlamaFirewall: An Open Source Guardrail System for Building Secure AI Agents" (arXiv —
  concrete open-source system, strong candidate for implementation-level teaching) —
  `14-llamafirewall.md`
- "PIArena: A Platform for Prompt Injection Evaluation" (arXiv, benchmark) —
  `03-piarena-benchmark.md`
- "LongPIBench: A Long-Context Benchmark for Prompt Injection" (arXiv, benchmark) —
  `04-longpibench.md`
- "Cortex AI Guardrails: Prompt Injection & Jailbreak Prevention" (Snowflake — vendor
  primary source) — `15-snowflake-cortex-guardrails.md`

---

## Module 9: Interview Readiness

**Prerequisites:** all preceding modules — this is explicitly a capstone/review layer, not
new technical content.

**Learning objectives (intended scope, not yet sourced):**
- Answer conceptual questions across all prior modules fluently (tokenization, RAG, evals,
  agents, cost/latency, security) at a level appropriate for AI Engineer interviews.
- Work through system-design-style prompts (e.g. "design a RAG system", "design an agentic
  customer-support system") with a structured approach.
- Practice articulating tradeoffs (the recurring theme across every module: RAG vs.
  long-context, single-agent vs. multi-agent, judge-based vs. reference-based evals) since
  that is what distinguishes a strong interview answer from a definition-recitation.

### Lesson content: GAP (entire module)

**GAP — no verified sources at all.** Zero verified entries under "Вопросы на
собеседованиях AI Engineer" in `research/verified.md`; every candidate blocked as
`EGRESS_BLOCKED`. This module cannot be built at all right now beyond restating the
objectives above — there is no verified question bank, no verified system-design guide, and
no verified "what do interviewers actually test for" source to draw from.

What's specifically needed:
1. A verified, credible (not SEO-listicle) question bank for AI/LLM engineer interviews,
   ideally from a source with actual hiring-process visibility (a recruiting company, a
   documented set of real interview reports) rather than a generic "Top N questions" blog.
2. A verified system-design guide specific to generative-AI/RAG/agentic system design
   interviews, with worked example answers, not just a question list.
3. Verified, topic-specific question sets for RAG and for prompt engineering specifically,
   so this module can cross-link back into Modules 3 and 5 rather than being a single
   generic list.

Candidate raw entries to re-check first (titles, under
`research/raw/ai-engineer-interview-questions/`):
- "45+ AI Engineer Interview Questions & Answers (2026 Guide)" (UPenn Career Services —
  university career-services source, worth prioritizing for credibility) —
  `01-upenn-ai-engineer-interview-questions.md`
- "Every AI Engineer Interview Question You Need to Know in 2026 (From 100+ Real
  Interviews)" (claims real-interview provenance — worth checking if it substantiates that
  claim) — `02-medium-100-real-interviews-ai-engineer.md`
- "45+ AI Engineer Interview Questions & Answers (2026 Guide)" (Aced/Exponent — an actual
  interview-prep company) — `03-exponent-ai-engineer-interview-questions.md`
- "Generative AI System Design Interview: 2026 Guide" —
  `09-systemdesignhandbook-genai-system-design-guide.md`
- "AI System Design Interview Questions (2026)" —
  `10-systemdesignhandbook-ai-system-design-questions.md`
- "Machine Learning System Design Interview (2026 Guide)" (Exponent) —
  `12-exponent-ml-system-design-interview-guide.md`
- "7 RAG & Agent System Design Questions You Will Face in Every AI Engineer Interview (With
  Answers)" — `14-towardsai-rag-agent-system-design-questions.md`
- "Design and optimize a RAG system | OpenAI Interview Question" (claims to be an actual
  reported interview question — worth checking provenance) —
  `19-prachub-design-optimize-rag-system.md`
- "Top 30 RAG Interview Questions and Answers for 2026" (DataCamp) —
  `13-datacamp-rag-interview-questions.md`
- "RAG Interview: 40 Questions to Go from Beginner to Advanced" (Analytics Vidhya) —
  `15-analyticsvidhya-rag-interview-questions.md`
- "Prompt Engineering Interview Questions That Actually Get Asked" (CodeSignal) —
  `17-codesignal-prompt-engineering-interview-questions.md`
- "Top 32 Prompt Engineering Interview Questions (2026)" —
  `18-datainterview-prompt-engineering-questions.md`

---

## Summary table

| # | Module | Verified sources | Status |
|---|---|---|---|
| 0 | Orientation | 0 (see CURRENT.md) | meta / non-graded |
| 1 | LLM Fundamentals & Tokenization | 1 (tiktoken) | **partial** — tokenization mechanics sourced; sampling/context/attention/KV-cache is a GAP |
| 2 | Embeddings & Vector Search | 0 | **GAP** (entire module) |
| 3 | Retrieval-Augmented Generation | 0 | **GAP** (entire module) |
| 4 | Evaluation (Evals) | 0 | **GAP** (entire module) |
| 5 | Prompt Design & Iteration | 0 | **GAP** (entire module) |
| 6 | Agents & Tool Use | 3 (2 MCP posts + 1 shared with Module 8) | **partial** — MCP protocol sourced; agent fundamentals/architectures/frameworks is a GAP |
| 7 | Cost & Latency | 0 | **GAP** (entire module) |
| 8 | Prompt Injection & Security | 1 (shared with Module 6) | **partial** — one worked example sourced; everything else is a GAP |
| 9 | Interview Readiness | 0 | **GAP** (entire module) |

Note: the Microsoft security post is counted once as a verified source but used in two
modules (6 and 8) because its content genuinely serves both — that is a deliberate citation
choice, not double-counting toward the "7 verified sources" total in `research/verified.md`.
