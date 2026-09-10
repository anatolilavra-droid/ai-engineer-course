# How Anthropic Built a Multi-Agent Research System

- URL: https://blog.bytebytego.com/p/how-anthropic-built-a-multi-agent
- Type: article
- Published: unknown
- Topic: agents-tool-use

Describes Anthropic's orchestrator-worker multi-agent research architecture: a Lead Researcher agent analyzes queries, decides strategy, and spawns specialized subagents that each operate with their own context window, tools, and exploration trajectory for parallel information gathering. Reports the system achieved a 90.2% performance improvement over single-agent systems on internal evaluations but consumes roughly fifteen times more tokens than standard chat, making it best suited to parallelizable research tasks rather than tightly interdependent tasks like coding.
