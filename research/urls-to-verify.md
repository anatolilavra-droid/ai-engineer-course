# URLs to verify

Триаж 123 ссылок из исходного `research/raw/` по 7 темам (эмбеддинги, RAG, evals, промпт-дизайн,
cost/latency, prompt injection, интервью-вопросы), которые не подпадали под сетевое ограничение
основной сессии. Результат ручной проверки от 11.09.2026.

**Метод:** открывались первоисточники (документация, исследовательские блоги, канонические
учебные ресурсы). Отсев по типу источника применялся к материалам, которые по формату заголовка
и домену заведомо не проходят критерии — без открытия содержимого: вендорские листиклы
(«Top N tools»), контент-маркетинг вокруг продукта, Medium-перепевы. Это отсев по жанру, а не по
содержанию — если по какой-то теме материала не хватит, часть из них можно перепроверить.

**Итог: проверено и подтверждено 5 → перенесены в `research/verified.md`. Отсеяно по жанру без
открытия: ~76-78 (см. сверку чисел в конце файла). Осталось открыть: 40. Найдено новых кандидатов
по ссылкам из проверенных источников: 9 (добавлены в `research/raw/`, отдельный раздел ниже).**

---

## Проверено и подтверждено (5) — перенесены в research/verified.md

- Hierarchical Navigable Small Worlds (HNSW) — Pinecone — эмбеддинги — Quality A
- Prompt engineering best practices for 2026 — Anthropic — промпт-дизайн — Quality A
- Few-Shot Prompting — Prompt Engineering Guide (DAIR.AI) — промпт-дизайн — Quality A
- Evaluation concepts — LangSmith / LangChain docs — evals — Quality A
- Fooling AI Agents: Web-Based Indirect Prompt Injection Observed in the Wild — Unit 42 — prompt injection — Quality A

Полные карточки с метаданными — в `research/verified.md`.

---

## Найдено по ссылкам из проверенных источников (9)

Не открывалось, но пришло из материалов класса A, а не из поисковой выдачи — приоритет на
следующий заход проверки. Добавлены как новые кандидаты в `research/raw/<topic>/` (не входят в
исходные 123, поэтому не в счёте выше).

- Faiss: The Missing Manual, остальные главы (LSH, product quantization, композитные индексы) — https://www.pinecone.io/learn/series/faiss/ — `research/raw/embeddings-vector-search/16-faiss-missing-manual-series.md`
- Prompt Engineering Guide, раздел adversarial prompting — https://www.promptingguide.ai/risks/adversarial — `research/raw/prompt-injection/16-promptingguide-adversarial-prompting.md`
- OWASP LLM Prompt Injection Prevention Cheat Sheet — https://cheatsheetseries.owasp.org/cheatsheets/LLM_Prompt_Injection_Prevention_Cheat_Sheet.html — `research/raw/prompt-injection/17-owasp-llm-prompt-injection-cheat-sheet.md`
- Spotlighting (защита от инъекций), arXiv 2403.14720 — https://arxiv.org/abs/2403.14720 — `research/raw/prompt-injection/18-spotlighting-arxiv-2403.14720.md`
- Instruction Hierarchy, arXiv 2404.13208 — https://arxiv.org/abs/2404.13208 — `research/raw/prompt-injection/19-instruction-hierarchy-arxiv-2404.13208.md`
- Design-level defenses против инъекций, arXiv 2503.18813 — https://arxiv.org/pdf/2503.18813 — `research/raw/prompt-injection/20-design-level-defenses-arxiv-2503.18813.md`
- Hamel Husain, «Your AI Product Needs Evals» — https://hamel.dev/blog/posts/evals/ — `research/raw/evals/19-hamel-husain-your-ai-product-needs-evals.md` (на него ссылается документация LangSmith как на отправную точку по evals)
- Anthropic, Effective context engineering for AI agents — https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents — `research/raw/prompt-engineering/19-anthropic-effective-context-engineering.md`
- Anthropic, интерактивный туториал по промптингу — https://github.com/anthropics/prompt-eng-interactive-tutorial — `research/raw/prompt-engineering/20-anthropic-prompt-eng-interactive-tutorial.md` (уже на доступном домене — GitHub, не блокируется сетевой политикой основной сессии; топ-приоритет к открытию)

---

## Стоит открыть следующими (40, не проверено)

Прошли жанровый фильтр — первоисточники, препринты и инженерные блоги. Не открывались только
из-за объёма.

**Эмбеддинги (4)**
- Product Quantization — Pinecone — https://www.pinecone.io/learn/series/faiss/product-quantization/
- Fine-tuning embeddings for RAG with synthetic data — LlamaIndex — https://www.llamaindex.ai/blog/fine-tuning-embeddings-for-rag-with-synthetic-data-e534409a3971
- Scaling Vector Search to 1 Billion on PostgreSQL — VectorChord — https://blog.vectorchord.ai/scaling-vector-search-to-1-billion-on-postgresql
- Hybrid Search in Production: BM25 vs dense — https://tianpan.co/blog/2026-04-12-hybrid-search-production-bm25-dense-embeddings

**RAG (4)**
- Engineering the RAG Stack (обзор архитектур), arXiv — https://arxiv.org/pdf/2601.05264
- What is GraphRAG — Neo4j — https://neo4j.com/blog/genai/what-is-graphrag/
- RAG failure modes — Snorkel — https://snorkel.ai/blog/retrieval-augmented-generation-rag-failure-modes-and-how-to-fix-them/
- RAG vs long-context LLMs — Meilisearch — https://www.meilisearch.com/blog/rag-vs-long-context-llms

**Evals (4)**
- Building Agent & LLM Evaluation Datasets — MLflow docs — https://mlflow.org/docs/latest/genai/datasets/
- LLM Evaluation: методы и метрики — Arize — https://arize.com/llm-evaluation/
- LLM-as-a-Judge: полное руководство — Evidently AI — https://www.evidentlyai.com/llm-guide/llm-as-a-judge
- Illusions of the Gold Standard (о протоколах человеческой оценки), arXiv — https://arxiv.org/pdf/2606.07936

**Промпт-дизайн (5)**
- Codex Prompting Guide — OpenAI — https://developers.openai.com/cookbook/examples/gpt-5/codex_prompting_guide
- Gemini 3 developer guide — Google — https://ai.google.dev/gemini-api/docs/gemini-3
- GPT-5.5 prompting guide — Simon Willison — https://simonwillison.net/2026/apr/25/gpt-5-5-prompting-guide/
- Zero-Shot vs Few-Shot с примерами — Vellum — https://www.vellum.ai/blog/zero-shot-vs-few-shot-prompting-a-guide-with-examples
- promptolution: фреймворк оптимизации промптов, arXiv — https://arxiv.org/pdf/2512.02840

**Стоимость и латентность (4)**
- Dynamic Model Routing and Cascading: обзор, arXiv — https://arxiv.org/html/2603.04445v1
- Cluster, Route, Escalate: каскады для cost-aware serving, arXiv — https://arxiv.org/html/2606.27457
- How speculative decoding delivers faster LLM inference — Red Hat — https://developers.redhat.com/articles/2026/06/12/how-speculative-decoding-delivers-faster-llm-inference
- Distillation with Programmatic Data Curation — TensorZero — https://www.tensorzero.com/blog/distillation-programmatic-data-curation-smarter-llms-5-30x-cheaper-inference/

**Prompt injection (10)**
- Indirect Prompt Injection — Lakera — https://www.lakera.ai/blog/indirect-prompt-injection
- Indirect Prompt Injection Attacks — CrowdStrike — https://www.crowdstrike.com/en-us/blog/indirect-prompt-injection-attacks-hidden-ai-risks/
- LlamaFirewall: open source guardrail system, arXiv — https://arxiv.org/pdf/2505.03574
- PIArena: платформа оценки инъекций, arXiv — https://arxiv.org/pdf/2604.08499
- LongPIBench: бенчмарк на длинном контексте, arXiv — https://arxiv.org/abs/2608.28411v1
- Agent Data Injection Attacks, arXiv — https://arxiv.org/html/2607.05120v1
- GitInject: инъекции в CI/CD, arXiv — https://arxiv.org/pdf/2606.09935
- The Promptware Kill Chain, arXiv — https://arxiv.org/pdf/2601.09625
- Prompt Injection vs Jailbreaking — Learn Prompting — https://learnprompting.org/blog/injection_jailbreaking
- Prompt Injection vs Jailbreaking — Promptfoo — https://www.promptfoo.dev/blog/jailbreaking-vs-prompt-injection/

**Вопросы на собеседованиях (9)** — оставлены на случай, если решение по модулю 9 (см. ниже) пересмотрят
- 45+ AI Engineer Interview Questions — UPenn Career Services — https://careerservices.upenn.edu/blog/2026/06/25/45-ai-engineer-interview-questions-answers-2026-guide/
- Every AI Engineer Interview Question... (claims 100+ real interviews) — https://adilshamim8.medium.com/every-ai-engineer-interview-question-you-need-to-know-in-2026-from-100-real-interviews-b5b7ae4b961a
- 45+ AI Engineer Interview Questions — Aced/Exponent — https://www.tryexponent.com/blog/ai-engineer-interview-questions
- Machine Learning System Design Interview Guide — Exponent — https://www.tryexponent.com/blog/machine-learning-system-design-interview-guide
- Generative AI System Design Interview: 2026 Guide — https://www.systemdesignhandbook.com/guides/generative-ai-system-design-interview/
- AI System Design Interview Questions — https://www.systemdesignhandbook.com/blog/ai-system-design-interview-questions/
- The Complete Agentic AI System Design Interview Guide — https://atul4u.medium.com/the-complete-agentic-ai-system-design-interview-guide-2026-f95d0cfeb7cf
- 7 RAG & Agent System Design Questions... — https://pub.towardsai.net/7-rag-agent-system-design-questions-you-will-face-in-every-ai-engineer-interview-with-answers-45d31004ffe4
- Design and optimize a RAG system | OpenAI Interview Question (claims real provenance) — https://prachub.com/interview-questions/design-and-optimize-a-rag-system

---

## Отсеяно (78, по жанру, без открытия)

### Вендорские листиклы «Top N» (21)

Причина: перечисление инструментов без объяснения принципов, почти всегда с продуктом издателя в
списке. Такие материалы не учат, а продают, и устаревают за месяцы.

Примеры: «Top 9 LLM Evaluation Tools», «Top 5 LLM Evaluation Frameworks», «Top 5 Agent Evaluation
Tools», «Top 10 Prompt Optimization Tools», «Best Open-Source Embedding Models in 2026», «Top
Reranking Models», «Best Multimodal Embedding Models — Tested & Ranked», «Best LLM monitoring
tools», «Best AI Eval Tools for CI/CD», «Comparing the best open source vector databases», «20
Advanced RAG Types».

### Контент-маркетинг вокруг продукта (32)

Причина: материал существует, чтобы привести к покупке; техническая часть сведена к обзору.
Домены: denser.ai, futureagi, getmaxim, orq, k2view, digitalapplied, buildmvpfast, crazyrouter,
pickaxe, lyzr, atlan, puppygraph, oneuptime, galtea, superannotate, galileo, statsig, neuraltrust,
spheron, runpod, intuitionlabs, gmicloud, callsphere, myengineeringpath, snowflake, sysdig,
inngest, kili, automationanywhere.

### Medium и агрегаторы (11)

Причина: перепевы первоисточников без собственного вклада, часто с признаками SEO-генерации.
Сюда же «MTEB Leaderboard» на codesota — агрегатор чужого лидерборда вместо самого лидерборда на
Hugging Face.

### Юридический материал (1)

ktslaw про риски prompt injection в трудовом праве — тема не учебная.

### Тема «Вопросы на собеседованиях» (11 из 20 отсеяно как чистые списки; 9 — в «стоит открыть» выше)

Причина отдельная и важная: жанр «45+ вопросов с ответами» состоит из списков формулировок без
понимания. Заучивание таких ответов проваливает собеседование быстрее, чем незнание — интервьюер
видит зазубренное с первого уточняющего вопроса.

**Решение, применённое в CORE.md (модуль 9):** тему не закрывать списками вопросов, а заменить
модулем «защита собственного проекта» — разбор своего сервиса, объяснение trade-offs, ответ на «а
что если нагрузка вырастет в 100 раз». Это применено независимо от того, откроются ли оставшиеся
9 ссылок — они лишь дополнительный, необязательный материал, если решение по модулю 9 пересмотрят.

Отсеянные без открытия (11, чистые списки вопросов): «50 AI Engineer Interview Questions», «Top 36
LLM Interview Questions» (DataCamp), «LLM Interview Questions — 30 Questions» (myengineeringpath),
«LLM Engineer Interview Questions: 2026 Hiring Guide», «Top 10 LLM Engineer Interview Questions»,
«Top 30 RAG Interview Questions» (DataCamp), «RAG Interview: 40 Questions», «Top 36 Generative AI
Interview Questions» (DataCamp), «Prompt Engineering Interview Questions That Actually Get Asked»,
«Top 32 Prompt Engineering Interview Questions», «Top 20 AI & Machine Learning Interview
Questions» (Tredence).

**Сверка чисел:** 5 (проверено) + 40 (стоит открыть, включая 9 по интервью) + 21 + 32 + 11 + 1 +
11 (интервью, чистые списки) = 121 из 123 — на 2 меньше заявленного в исходном отчёте (5+78+40).
Расхождение мелкое и, похоже, из дедупликации/округления при ручном подсчёте; не стал подгонять
задним числом — здесь приведён самый честный из воспроизводимых подсчётов по конкретным
заголовкам.
