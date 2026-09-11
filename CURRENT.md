# CURRENT — 2026 Tooling, Roadmaps & Interview Layer

This is the layer of the course expected to age: specific tools, model versions,
frameworks, pricing, roadmaps, and interview trends. It cross-links back to `CORE.md`
modules by name rather than repeating their narrative. As with `CORE.md`, every concrete
resource pointer here traces to an entry verified in `research/verified.md` — nothing is
filled in from training-data memory.

As of 11.09.2026, 7 of 10 topic areas in `research/verified.md` have at least one verified
source (LLM basics/tokenization, embeddings, evals, prompt engineering, agents & tool use,
prompt injection, and AI Engineer roadmaps); only RAG and cost/latency remain fully unsourced,
and interview readiness has zero by deliberate design (see `CORE.md` Module 9). Most of that
new material earned a place in `CORE.md` instead of here, though, because it teaches durable
concepts (how HNSW works, evaluation concepts, prompting fundamentals, injection taxonomy)
rather than something that will look different in six months. This file stays intentionally
short: it's the roadmap references, the current-tooling angle on Module 6, and explicit gap
notes for every other current-layer concern the course will eventually need — not padded out
with unsourced "state of the ecosystem" prose.

---

## Roadmaps & Orientation (supports CORE.md → Module 0)

Three community AI Engineer roadmap repositories are verified as live, active, and
concrete. None of these is official/canonical — they are unofficial community roadmaps of
varying maturity — so present them to the learner as **reference points for scope and
sequencing ideas**, not as an endorsed syllabus. This course's own module list (see
`CORE.md`) is not a copy of any one of these; it derives from `LEARNER.md`'s success-criteria
list and adds ordering rationale of its own.

#### Ultimate AI Engineer Roadmap 2026 (PrinceSinghhub)
- URL: https://github.com/PrinceSinghhub/Ultimate-AI-Engineer-Roadmap-2026
- Quality: B · Level: beginner to advanced · Price: free
- Time: ~1-2 hours to read the full roadmap; full path is multi-month self-paced
- Verified: 2026-09-10
- Why point learners here: the most actively maintained and highest-traction of the three
  (852 stars, 133 forks, last commit 2026-08-01). 17 phases plus a capstone, each phase with
  learning objectives, code examples, and tiered (easy/medium/hard) projects. Best pick if a
  learner wants one comprehensive reference roadmap to skim alongside this course.

#### atryx/ai-engineer-roadmap-2026
- URL: https://github.com/atryx/ai-engineer-roadmap-2026
- Quality: C · Level: beginner to advanced · Price: free
- Time: ~30-45 min read (roadmap doc); full path is multi-month self-paced
- Verified: 2026-09-10
- Why point learners here: a concrete 10-phase path with tool-comparison tables and project
  ideas, structured close to this course's own module order (foundations → LLM fundamentals
  → prompt engineering → RAG → agents → fine-tuning → evaluation → production → multi-modal
  → advanced patterns). Caveat flagged in verification: thin commit history (2 commits, one
  a bot verification commit) — treat as a lightweight secondary overview, not a heavily
  vetted community resource.

#### musamaanjum/ai-engineer-roadmap
- URL: https://github.com/musamaanjum/ai-engineer-roadmap
- Quality: C · Level: intermediate · Price: free
- Time: ~20-30 min read
- Verified: 2026-09-10
- Why point learners here: the most useful of the three for a learner asking "what named
  courses/projects should I actually go do" — 24 named external courses (DeepLearning.AI,
  Stanford, Coursera) and 5 named portfolio projects (RAG, fine-tuning, multi-agent,
  evaluation, production app), plus interview-prep pointers. Caveat: modest traction/vetting
  (15 stars, 1 fork, single commit).

**GAP — no verified source for the "official"/highest-traffic roadmap.** `roadmap.sh`'s own
AI Engineer roadmap (https://roadmap.sh/ai-engineer) — plausibly the most-referenced roadmap
in this space — could not be fetched (`EGRESS_BLOCKED`) and has no verdict. Re-check this
first if network access widens; it would likely become the primary roadmap reference here,
demoting the three above to secondary status. Also unchecked: 16 other roadmap/career-path
articles listed under "Не проверено" in `research/verified.md` (Turing College, Dataquest,
Zero To Mastery, KDnuggets ×2, DataCamp, DeepLearning.AI's "The Batch" skills map, and
others) — see that section of `research/verified.md` for the full list and exact titles.

---

## Agents & Tool Use — current protocol state (supports CORE.md → Module 6)

As of the two verified MCP posts (both dated 2026, see `CORE.md` Module 6 Lesson 6.1 for
full citations and teaching notes):

- **Protocol direction (2026 Roadmap):** MCP's 2026 priorities are transport scalability,
  agent-to-agent communication, governance maturation, and enterprise readiness — this is
  the "why is MCP changing" framing for whatever version of the spec a learner encounters.
- **Concrete spec state (2026-07-28 release):** stateless protocol core, Multi Round-Trip
  Requests, header-based routing (`Mcp-Method`/`Mcp-Name`), cacheable list results, RFC 9207
  authorization hardening. Adoption: TypeScript and Python SDKs each over 1B downloads.
- **Practical implication for this course:** if a learner builds an MCP-based tool
  integration during Module 6, teach it against the stateless-core model described in the
  2026-07-28 spec post, not against an older stateful assumption.

**GAP — no verified source for framework choice.** This course cannot currently recommend
LangGraph vs. CrewAI vs. AutoGen vs. the Claude Agent SDK vs. the OpenAI Agents SDK, because
every comparison source is unverified (`EGRESS_BLOCKED`). See `CORE.md` Module 6 Lesson 6.2
for the full list of candidate raw entries to re-check (titles under
`research/raw/agents-tool-use/`), including two first-party candidates worth prioritizing
once reachable: OpenAI's own "The next evolution of the Agents SDK" and Anthropic's own "When
to use multi-agent systems (and when not to)".

---

## Cost & Latency — pricing (supports CORE.md → Module 7)

**GAP — entirely unsourced.** Model API pricing changes too often to hardcode into a static
course document even if it were sourced, and right now it isn't: zero verified sources exist
for "Стоимость и латентность" in `research/verified.md`. The one raw candidate that would
specifically belong in this CURRENT-layer pricing section, once verified, is:
- "LLM API Pricing Comparison 2026: 30+ Models, Every Provider" —
  `research/raw/cost-latency/14-llm-api-pricing-comparison-inference-net.md`
- "LLM Inference Cost Comparison 2026: DigitalOcean vs. Together AI, Fireworks AI, Modal,
  Nebius, Baseten, and OpenRouter" —
  `research/raw/cost-latency/13-llm-inference-cost-comparison-digitalocean.md`

Do not cite specific per-token prices anywhere in this course from memory — they age within
weeks and neither entry above has been verified. See `CORE.md` Module 7 for the full
technique-level gap list (caching, routing, speculative decoding, etc.), which is a
CORE-layer concern once sourced (the techniques themselves are durable even though specific
prices aren't) — only the live pricing numbers belong in this CURRENT file.

---

## Prompt Design — vendor-specific current guides (supports CORE.md → Module 5)

**Update (11.09.2026):** Anthropic's own guide is now verified and taught in `CORE.md`
Module 5 Lesson 5.1 (it earned a CORE placement rather than staying here, since its
technique content — few-shot, CoT, prefill — is durable, not version-specific; only its
"current as of late 2025" framing is time-sensitive). OpenAI's and Google's equivalents
remain unsourced:
- OpenAI: "Codex Prompting Guide" / "GPT-5.5 prompting guide" (the latter via Simon
  Willison, an independent but reputable practitioner) —
  `research/raw/prompt-engineering/12-openai-codex-prompting-guide.md` and
  `research/raw/prompt-engineering/11-simonwillison-gpt55-prompting-guide.md`
- Google: "Gemini 3 developer guide" —
  `research/raw/prompt-engineering/14-google-gemini3-developer-guide.md`
- Also newly found, not yet verified: Anthropic's "Effective context engineering for AI
  agents" and Anthropic's own interactive prompting tutorial repo (the latter is on GitHub,
  already reachable — top priority) —
  `research/raw/prompt-engineering/19-anthropic-effective-context-engineering.md`,
  `research/raw/prompt-engineering/20-anthropic-prompt-eng-interactive-tutorial.md`

Re-checking the OpenAI/Google guides (and the GitHub-hosted Anthropic tutorial, which needs
no network-policy change at all) should be the next priority — they'd round out this section
with the actual current per-vendor guidance it's meant to hold, alongside Anthropic's.

---

## Interview Readiness — current trends (supports CORE.md → Module 9)

**Update (11.09.2026): no longer a GAP to fill with sources — redesigned instead.** Module 9
was rebuilt around a "defend your own project" methodology that needs no external question
bank (see `CORE.md` Module 9 for the full rationale and structure). Of the 20 raw candidates
for this topic, 11 were screened out entirely as pure question-list listicles; the remaining
9 are kept as strictly optional, unverified supplementary material (`CORE.md` Module 9 Lesson
9.2) — nothing here belongs in the CURRENT layer specifically, since the methodology itself
doesn't age the way a tool/pricing fact would.

---

## Prompt Injection — current threat landscape (supports CORE.md → Module 8)

Beyond the two sourced items already taught in `CORE.md` Module 8 (Lesson 8.1, Microsoft's
MCP tool-metadata poisoning case; Lesson 8.2, Unit 42's indirect-injection taxonomy and
telemetry — both durable enough to live in CORE rather than here), there is no verified
source for active benchmarks or open-source guardrail tooling adoption specifically. See
`CORE.md` Module 8 Lesson 8.3 for the full gap list and candidates — several of the
unverified candidates there (LlamaFirewall, the OWASP cheat sheet, the spotlighting/
instruction-hierarchy/design-level-defenses papers, the CI/CD-focused GitInject paper) are
specifically current-tooling/threat-landscape material that belongs in this file once
verified, rather than in CORE's durable narrative.

---

## Summary

| Section | Verified sources used | Status |
|---|---|---|
| Roadmaps & Orientation | 3 (all three verified roadmap repos) | sourced, with an explicit gap on roadmap.sh itself |
| Agents & Tool Use current state | 2 (both MCP posts, cross-linked from CORE Module 6) | sourced |
| Cost & Latency pricing | 0 | GAP |
| Prompt Design vendor guides | 0 (Anthropic's guide moved to CORE Module 5 — durable technique content) | GAP for OpenAI/Google guides (3 candidates identified incl. 1 already on GitHub, unverified) |
| Interview Readiness trends | 0, by design | redesigned in CORE Module 9, not a sourcing gap — see CORE.md |
| Prompt Injection threat landscape | 0 beyond the 2 CORE-durable examples (Lessons 8.1-8.2) | GAP for benchmarks/guardrail tooling specifically |

Total distinct verified sources referenced across this file: 5 (3 roadmap repos + 2 MCP
posts). The Microsoft security post and the Unit 42 post are referenced by pointer back to
CORE.md rather than recounted here, since their content is CORE-durable (general lesson
patterns) rather than 2026-specific tooling facts.
