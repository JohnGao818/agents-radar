# AI Open Source Trends 2026-07-20

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-07-20 02:35 UTC

---

# AI Open Source Trends Report – 2026-07-20

## 1. Today’s Highlights
Today’s GitHub trending data reveals an accelerating shift toward **local-first, MCP-native AI tooling** for coding agents. Three distinct themes stand out: (1) **context-aware code intelligence** – projects like `code-review-graph` and `wigolo` that reduce token overhead by giving agents a persistent, compressed view of a codebase or the web; (2) **democratised LLM inference** – `ktransformers` (heterogeneous GPU/CPU inference) and `airllm` (single 4GB GPU 70B inference) continue to lower hardware barriers; and (3) **production-ready agent platforms** – MoonshotAI’s `kimi-cli` CLI agent and Canner's `WrenAI` text‑to‑SQL both entered the top trending list with strong daily star counts. Simultaneously, the broader topic search confirms massive community investment in RAG ecosystems (Dify, RAGFlow), agent memory layers (Mem0, Cognee), and browser‑/computer‑use automation (browser‑use, Cua).

## 2. Top Projects by Category

### 🔧 AI Infrastructure
- **[kvcache-ai/ktransformers](https://github.com/kvcache-ai/ktransformers)** – ⭐360 today. Flexible framework for heterogeneous LLM inference and fine‑tuning, enabling GPU‑CPU hybrid execution.
- **[lyogavin/airllm](https://github.com/lyogavin/airllm)** – ⭐358 today. Run 70B LLMs on a single 4GB GPU through aggressive memory optimisation.
- **[github/copilot-sdk](https://github.com/github/copilot-sdk)** – ⭐39 today. Multi‑platform SDK to integrate Copilot Agent into any service.
- **[MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli)** – ⭐410 today. Terminal‑first CLI agent with built‑in tool use and code generation.
- **[vllm-project/vllm](https://github.com/vllm-project/vllm)** – ⭐86,659 total. High‑throughput LLM inference engine; the de‑facto standard for production serving.
- **[ollama/ollama](https://github.com/ollama/ollama)** – ⭐176,470 total. Local LLM runner supporting dozens of models including DeepSeek, Qwen, and Gemma.

### 🤖 AI Agents / Workflows
- **[NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)** – ⭐217,289 total. Fast‑growing agent harness with skill, memory, and multi‑CLI support.
- **[browser-use/browser-use](https://github.com/browser-use/browser-use)** – ⭐105,593 total. Make websites accessible to AI agents – the dominant browser automation library.
- **[trycua/cua](https://github.com/trycua/cua)** – ⭐64 today. Open‑source computer‑use 2.0 drivers and benchmarks for training/evaluation.
- **[1jehuang/jcode](https://github.com/1jehuang/jcode)** – ⭐235 today. Coding agent harness focused on fast iteration and tool integration.
- **[AstrBotDevs/AstrBot](https://github.com/AstrBotDevs/AstrBot)** – ⭐83 today. Multi‑platform AI agent framework (IM, LLM, plugins).
- **[TauricResearch/TradingAgents](https://github.com/TauricResearch/TradingAgents)** – ⭐93,699 total. Multi‑agent financial trading framework powered by LLMs.
- **[OpenHands/OpenHands](https://github.com/OpenHands/OpenHands)** – ⭐81,330 total. AI‑driven software development agent.

### 📦 AI Applications
- **[jamiepine/voicebox](https://github.com/jamiepine/voicebox)** – ⭐610 today. Open‑source AI voice studio for cloning, dictation, and audio creation.
- **[Canner/WrenAI](https://github.com/Canner/WrenAI)** – ⭐121 today. Generative BI engine – natural‑language to SQL and dashboards across 20+ data sources.
- **[hugohe3/ppt-master](https://github.com/hugohe3/ppt-master)** – ⭐39,969 total. AI‑powered PowerPoint deck generator from documents or topics.
- **[PostHog/posthog](https://github.com/PostHog/posthog)** – ⭐411 today. Product analytics platform adding AI observability and agent debugging via MCP.

### 🧠 LLMs / Training
- **[huggingface/transformers](https://github.com/huggingface/transformers)** – ⭐162,745 total. State‑of‑the‑art model framework for all modalities.
- **[Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT)** – ⭐185,617 total. Pioneering autonomous agent project; now a full platform for agent development.
- **[galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining)** – ⭐290 today. Minimal, reliable library for pretraining foundation and world models.
- **[skyzh/tiny-llm](https://github.com/skyzh/tiny-llm)** – ⭐4,374 total. Educational project teaching LLM inference serving on Apple Silicon.

### 🔍 RAG / Knowledge
- **[langgenius/dify](https://github.com/langgenius/dify)** – ⭐149,374 total. Production‑ready RAG + agentic workflow platform.
- **[infiniflow/ragflow](https://github.com/infiniflow/ragflow)** – ⭐85,412 total. Leading open‑source RAG engine with Agent integration.
- **[mem0ai/mem0](https://github.com/mem0ai/mem0)** – ⭐61,232 total. Universal memory layer for AI agents – persistent context across sessions.
- **[headroomlabs-ai/headroom](https://github.com/headroomlabs-ai/headroom)** – ⭐60,388 total. Token‑compression tool for coding agents (20–95% fewer tokens).
- **[tirth8205/code-review-graph](https://github.com/tirth8205/code-review-graph)** – ⭐663 today. Local‑first code intelligence graph for MCP; reduces context by focusing on relevant code only.
- **[KnockOutEZ/wigolo](https://github.com/KnockOutEZ/wigolo)** – ⭐595 today. Local‑first web search/fetch MCP server – no API keys, $0/query.
- **[milvus-io/milvus](https://github.com/milvus-io/milvus)** – ⭐45,274 total. Cloud‑native vector database for scalable ANN search.

---

## 3. Trend Signal Analysis

Today’s data points to **three explosive trends** reshaping the AI open‑source landscape:

### Agent Context & Memory Dominate
The two highest‑starred trending projects – `code-review-graph` (+663) and `wigolo` (+595) – are both **MCP servers that optimise agent context**. They solve the same core problem: AI coding tools waste tokens on irrelevant information. By building persistent, compressed knowledge graphs (code‑review‑graph) or local‑first web scrapers (wigolo), they cut token usage dramatically. The topic search confirms this: **Mem0** (61k), **Headroom** (60k), **Cognee** (28k), and **Memvid** (16k) all provide memory or compression layers for agents. The community is collectively moving from “give the agent everything” to “give the agent only what it needs.”

### Computer‑Use 2.0 Goes Open Source
**Cua** (trycua/cua) entered trending with a bold promise: “Scale computer‑use 2.0 with open‑source drivers, cross‑OS fleets, and benchmarks.” Alongside **browser‑use** (105k stars), we see a maturing stack for GUI automation – not just web, but full OS‑level interaction. This is a direct response to Anthropic’s Computer Use and OpenAI’s Operator, but fully open and community‑driven.

### Industrial‑Strength Agent Frameworks Reach Critical Mass
Projects like **Hermes Agent** (217k), **AutoGPT** (185k), **OpenHands** (81k), **CopilotKit** (36k), and **AstrBot** (48k today) are no longer prototypes. They offer multi‑platform runtime (CLI, desktop, Slack, phone), built‑in memory, plugin systems, and MCP integration. **Kimi CLI** from MoonshotAI (+410 today) signals that even large labs are releasing CLI‑first agents as open source.

### RAG Becomes Commodity – But with a Twist
Traditional RAG (Dify, RAGFlow, AnythingLLM) continues to grow, but the new angle is **“vectorless RAG”** (PageIndex, LEANN) and **reasoning‑based retrieval** (PaddleOCR + LLM). **WrenAI** (+121) shows that text‑to‑SQL RAG is now production‑ready, while **Graphify‑Labs/graphify** (91k) turns entire codebases into queryable knowledge graphs – merging RAG with agent memory.

**Connection to recent LLM releases:** The trend toward low‑resource inference (4GB GPU for 70B) aligns with the rise of quantised models (e.g., Qwen, GLM‑5.2). MoonshotAI releasing their CLI open source suggests a play to build ecosystem around their API. 

**New direction: “Agent SDKs”** – GitHub’s own **copilot‑sdk** and Google’s **googleworkspace/cli** (with AI agent skills) point to an era where every platform offers an agent SDK, making MCP the universal glue.

---

## 4. Community Hot Spots – Developer Focus Areas

- **[code-review-graph](https://github.com/tirth8205/code-review-graph) & [wigolo](https://github.com/KnockOutEZ/wigolo)** – MCP servers that dramatically reduce token waste. As agent costs rise, projects that filter context will become essential middleware.

- **[mem0ai/mem0](https://github.com/mem0ai/mem0) & [topoteretes/cognee](https://github.com/topoteretes/cognee)** – Persistent agent memory is the missing piece for long‑running, autonomous workflows. Both projects are seeing heavy adoption for production agents.

- **[trycua/cua](https://github.com/trycua/cua)** – If you’re building computer‑use agents (e.g., for testing, data entry, or robotics), this open‑source driver stack could become the standard. Watch for integration with browser‑use and Hermes Agent.

- **[kvcache-ai/ktransformers](https://github.com/kvcache-ai/ktransformers)** – Heterogeneous inference (GPU + CPU + NPU) is the key to running large models on consumer hardware. This framework is more flexible than vLLM for multi‑device setups.

- **[MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli)** – The rise of CLI‑first agents (Claude Code, Gemini CLI, Kimi CLI) means developers should study their SDKs and skill systems. Kimi CLI’s rapid ascent (+410 today) suggests strong market pull for terminal‑based AI tools.

---

*Report generated from GitHub trending (2026-07-20) and AI topic search data. All star counts are as of the report date.*

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*