# AI Open Source Trends 2026-06-23

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-06-23 02:50 UTC

---

# AI Open Source Trends Report – 2026-06-23

## 1. Today's Highlights

The open-source AI ecosystem today is dominated by **agentic video production**, **context-aware MCP servers**, and **structured skill sharing for coding agents**. Leading the trend is **OpenMontage** (+2,938 stars today) – the first open-source end-to-end agentic video system, alongside **palmier-pro** and **hyperframes**, which collectively signal a strong push to turn LLM agents into video studios. Equally notable is the **explosion of agent skill repositories** (e.g., `mattpocock/skills`, `garrytan/gstack`, `Anthropic-Cybersecurity-Skills`) that package opinionated `.claude` configurations and domain-specific skills – a sign that the community is standardising around Claude Code and similar agent harnesses. Meanwhile, **DeusData/codebase-memory-mcp** (+1,185 today) offers a high-performance MCP server for code intelligence, and **ByteDance/deer-flow** (+738) provides a long-horizon SuperAgent harness, underscoring the maturation of agent infrastructure.

---

## 2. Top Projects by Category

### 🔧 AI Infrastructure
- **[ollama](https://github.com/ollama/ollama)** ⭐174,756 – Local LLM runtime supporting the latest models, the de facto standard for on-device inference.
- **[vllm-project/vllm](https://github.com/vllm-project/vllm)** ⭐83,590 – High-throughput LLM inference engine, now essential for production serving.
- **[firecrawl/firecrawl](https://github.com/firecrawl/firecrawl)** ⭐137,417 (+615 today) – Scalable web scraping API tailored for AI agent data ingestion.
- **[lyogavin/airllm](https://github.com/lyogavin/airllm)** ⭐? (+193 today) – Enables 70B model inference on a single 4GB GPU, widening hardware access.
- **[DeusData/codebase-memory-mcp](https://github.com/DeusData/codebase-memory-mcp)** ⭐? (+1,185 today) – Blazing-fast code intelligence MCP server with persistent knowledge graph (158 languages).

### 🤖 AI Agents / Workflows
- **[bytedance/deer-flow](https://github.com/bytedance/deer-flow)** ⭐73,341 (+738 today) – Long-horizon SuperAgent harness with sandboxes, memory, and subagents; handles tasks from minutes to hours.
- **[Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT)** ⭐185,092 – Pioneering autonomous agent platform, still the most starred agent framework.
- **[OpenHands/OpenHands](https://github.com/OpenHands/OpenHands)** ⭐78,040 – AI-driven development agent, gaining traction for code generation and debugging.
- **[mattpocock/skills](https://github.com/mattpocock/skills)** ⭐? (+2,051 today) – Curated agent skill files straight from the author's `.claude` directory – a new genre of sharable agent configs.
- **[garrytan/gstack](https://github.com/garrytan/gstack)** ⭐? (+573 today) – Claude Code setup with 23 opinionated tools acting as CEO, Designer, Engineer, etc.
- **[CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio)** ⭐47,673 – AI productivity studio with autonomous agents and 300+ assistants, unified LLM access.

### 📦 AI Applications
- **[calesthio/OpenMontage](https://github.com/calesthio/OpenMontage)** ⭐? (+2,938 today) – First open-source agentic video production system: 12 pipelines, 52 tools, 500+ agent skills.
- **[jamiepine/voicebox](https://github.com/jamiepine/voicebox)** ⭐? (+529 today) – Open-source AI voice studio for cloning, dictation, and creation.
- **[heygen-com/hyperframes](https://github.com/heygen-com/hyperframes)** ⭐? (+395 today) – Write HTML, render video – built for AI agents.
- **[ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis)** ⭐45,962 (+1,557 today) – LLM-driven multi-market stock analysis with real-time news and decision dashboards.
- **[hugohe3/ppt-master](https://github.com/hugohe3/ppt-master)** ⭐30,406 – AI generates editable PowerPoint slides from any document, with audio narration.

### 🧠 LLMs / Training
- **[huggingface/transformers](https://github.com/huggingface/transformers)** ⭐161,820 – The standard library for state-of-the-art ML models across modalities.
- **[NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)** ⭐200,033 – Agent that grows with you; combines LLM fine-tuning with agent orchestration.
- **[zjunlp/LightThinker](https://github.com/zjunlp/LightThinker)** ⭐164 – EMNLP 2025 paper on step-by-step compression during reasoning – a novel training paradigm.
- **[galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining)** ⭐266 – Minimal, reliable pretraining library for foundation and world models.

### 🔍 RAG / Knowledge
- **[infiniflow/ragflow](https://github.com/infiniflow/ragflow)** ⭐83,381 – Leading open-source RAG engine with agent capabilities and a superior context layer.
- **[run-llama/llama_index](https://github.com/run-llama/llama_index)** ⭐50,298 – Document agent and OCR platform, cornerstone for production RAG pipelines.
- **[mem0ai/mem0](https://github.com/mem0ai/mem0)** ⭐59,154 – Universal memory layer for AI agents, enabling persistent long-term recall.
- **[milvus-io/milvus](https://github.com/milvus-io/milvus)** ⭐44,899 – Cloud-native vector database for high-scale ANN search.
- **[safishamsi/graphify](https://github.com/safishamsi/graphify)** ⭐70,757 – Turn any codebase, docs, or data into a queryable knowledge graph – agent skill for Claude Code & Co.
- **[headroomlabs-ai/headroom](https://github.com/headroomlabs-ai/headroom)** ⭐47,191 – Compress tool outputs and RAG chunks by 60–95% before LLM ingestion.

---

## 3. Trend Signal Analysis

**Explosive community attention** is concentrated in three areas: **(1) agentic video production** – OpenMontage, hyperframes, and palmier-pro together garnered over 5,800 stars in a single day, reflecting a new appetite for turning LLM agents into full video production pipelines. **(2) Sharable agent skill files** – the meteoric rise of `mattpocock/skills` (+2,051) and `garrytan/gstack` (+573) signals a shift from monolithic agent frameworks to lightweight, composable configuration sets (`.claude` directories, MCP servers) that can be forked and reused across different agent harnesses. **(3) High-performance MCP servers** – DeusData’s `codebase-memory-mcp` (+1,185) and `zilliztech/claude-context` (11,928 total) show that the Model Context Protocol (MCP) is becoming the de facto standard for feeding structured context into agents, with sub-millisecond queries and zero-dependency binaries.

**New tech stacks** emerging today include “agent skill packages” that bundle tools, prompts, and knowledge graphs as drop-in extensions (e.g., `/skills` directories, `Anthropic-Cybersecurity-Skills` mapping six security frameworks). Also notable is the rise of **local-first vertical AI applications** like `daily_stock_analysis` (LLM finance) and `ppt-master` (document-to-presentation), which are easy to self-host and cost-free.

**Connection to industry events**: The surge in agent skill repositories aligns with the continued adoption of **Claude Code** and similar CLI-based agents, where a rich ecosystem of custom skills is a key differentiator. The explosive interest in video generation tools likely correlates with recent improvements in open-weight video models and agentic chaining of vision + audio tools.

---

## 4. Community Hot Spots

- **OpenMontage** – The debut of a full agentic video production suite is the most significant new direction today. Developers should watch how its 52 tools and 500+ agent skills evolve; could become the Blender of AI-driven video.
- **mattpocock/skills** and **Anthropic-Cybersecurity-Skills** – The rise of sharable skill directories points to a new norm: agent configurations as open-source packages. Expect a proliferation of domain-specific skill sets (e.g., legal, medical, DevOps).
- **DeusData/codebase-memory-mcp** – With 158-language support and sub-ms query times, this sets a new bar for code intelligence MCP servers. Its “99% fewer tokens” claim is critical for cost-conscious agent workflows.
- **daily_stock_analysis** – LLM-powered financial analysis is one of the most practical vertical applications. Its zero-cost, scheduled run model makes it a template for other “personal analyst” tools (e.g., weather, sports, portfolio tracking).
- **deer-flow (ByteDance)** – A long-horizon agent harness from a major AI company highlights the industry’s focus on tasks that span minutes to hours. Its sandbox, memory, and subagent architecture is likely to influence other frameworks.

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*