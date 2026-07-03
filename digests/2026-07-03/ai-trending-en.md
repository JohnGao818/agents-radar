# AI Open Source Trends 2026-07-03

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-07-03 02:35 UTC

---

# AI Open Source Trends Report — 2026-07-03

## 1. Today's Highlights

The open-source AI ecosystem is experiencing an explosion of agentic tooling, with three powerful signals emerging today: **agent performance optimization**, **multi-agent orchestration**, and **agent-skill standardization**. The trending list is dominated by tools that make AI coding agents more efficient—`caveman` (65% token reduction via caveman-speak) and `strix` (AI penetration testing) both saw thousands of stars. Meanwhile, the topic search reveals a maturing agent infrastructure: `affaan-m/ECC` (225K+ stars, agent harness) and `NousResearch/hermes-agent` (208K stars) are rapidly becoming foundational layers. The most notable new direction is the **agent skill specification movement**, with `agentskills` and `obra/superpowers` defining how skills should be packaged and consumed across Claude Code, Codex, CodeGemini, and others.

---

## 2. Top Projects by Category

### 🔧 AI Infrastructure

- **[vllm-project/vllm](https://github.com/vllm-project/vllm)** ⭐85,201 — High-throughput LLM inference engine; essential backbone for production deployments.
- **[ollama/ollama](https://github.com/ollama/ollama)** ⭐175,328 — The easiest way to run local LLMs; now supporting Kimi-K2.6, GLM-5.1, and DeepSeek.
- **[openai/codex-plugin-cc](https://github.com/openai/codex-plugin-cc)** ⭐0 (+352 today) — OpenAI's official bridge for using Codex from Claude Code; signals deeper cross-platform agent integration.
- **[langflow-ai/langflow](https://github.com/langflow-ai/langflow)** ⭐0 (+117 today) — Visual builder for AI agent workflows; competing with Flowise for low-code agent development.
- **[firecrawl/firecrawl](https://github.com/firecrawl/firecrawl)** ⭐143,297 — Web scraping API designed for AI agents; the go-to tool for giving agents web access.

### 🤖 AI Agents / Workflows

- **[msitarzewski/agency-agents](https://github.com/msitarzewski/agency-agents)** ⭐0 (+3032 today) — **Top trending repo** — A complete multi-agent agency: frontend wizards, Reddit ninjas, whimsy injectors. Highly viral due to its playful yet practical agent roles.
- **[JuliusBrussee/caveman](https://github.com/JuliusBrussee/caveman)** ⭐0 (+926 today) — Claude Code skill that reduces 65% of tokens via caveman-style language; taps into the "prompt efficiency" trend.
- **[NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)** ⭐208,089 [topic:ai-agent] — The agent that grows with you; a flagship open-source agent framework with strong community adoption.
- **[hkuds/Vibe-Trading](https://github.com/HKUDS/Vibe-Trading)** ⭐0 (+939 today) — Personal trading agent; specialized AI for financial tasks signals verticalization of agent use cases.
- **[browser-use/browser-use](https://github.com/browser-use/browser-use)** ⭐102,251 [topic:llm] — Makes websites accessible for AI agents; foundational for web automation agents.
- **[affaan-m/ECC](https://github.com/affaan-m/ECC)** ⭐225,230 [topic:llm] — Universal agent harness for Claude Code, Codex, Cursor; performance optimization, skills, memory, and security in one system.
- **[bytedance/deer-flow](https://github.com/bytedance/deer-flow)** ⭐75,939 [topic:llm] — Long-horizon SuperAgent harness; researchers, codes, creates with sandboxes and subagents.

### 📦 AI Applications

- **[usestrix/strix](https://github.com/usestrix/strix)** ⭐0 (+2137 today) — Open-source AI penetration testing tool; finds app vulnerabilities via AI-driven attacks.
- **[santifer/career-ops](https://github.com/santifer/career-ops)** ⭐0 (+372 today) — AI-powered job search with 14 skill modes, PDF generation, batch processing; practical vertical solution.
- **[ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis)** ⭐53,544 [topic:ai-agent] — LLM-powered multi-market stock analysis; real-time data, dashboards, zero-cost scheduling.
- **[hugohe3/ppt-master](https://github.com/hugohe3/ppt-master)** ⭐36,159 [topic:ai-agent] — AI generates editable PowerPoint from any document with native shapes and audio narration.
- **[CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio)** ⭐48,079 [topic:ai-agent] — AI productivity studio with 300+ assistants, smart chat, autonomous agents.

### 🧠 LLMs / Training

- **[pytorch/pytorch](https://github.com/pytorch/pytorch)** ⭐101,250 [topic:ml] — The standard deep learning framework; stable growth at +65 stars today.
- **[huggingface/transformers](https://github.com/huggingface/transformers)** ⭐162,171 [topic:ml] — Model hub and training ecosystem; every new model lands here first.
- **[0xPlaygrounds/rig](https://github.com/0xPlaygrounds/rig)** ⭐7,810 [topic:llm-model] — Build modular LLM apps in Rust; gaining traction for performance-critical agent pipelines.
- **[open-compass/opencompass](https://github.com/open-compass/opencompass)** ⭐7,146 [topic:llm-model] — LLM evaluation platform supporting 100+ datasets; essential for model comparison.

### 🔍 RAG / Knowledge

- **[langgenius/dify](https://github.com/langgenius/dify)** ⭐147,457 [topic:rag] — Production-ready RAG platform for agentic workflows; most starred RAG project today.
- **[infiniflow/ragflow](https://github.com/infiniflow/ragflow)** ⭐84,172 [topic:rag] — Leading open-source RAG engine with agent capabilities.
- **[milvus-io/milvus](https://github.com/milvus-io/milvus)** ⭐45,050 [topic:rag] — High-performance vector database; critical infrastructure for RAG systems.
- **[headroomlabs-ai/headroom](https://github.com/headroomlabs-ai/headroom)** ⭐55,867 [topic:rag] — Compress RAG chunks before LLM; 60-95% fewer tokens, same answers.
- **[StarTrail-org/LEANN](https://github.com/StarTrail-org/LEANN)** ⭐12,628 [topic:vector-db] — 97% storage savings for RAG on personal devices; [MLsys2026] paper implementation.

---

## 3. Trend Signal Analysis

**Explosive growth of agent skill ecosystems.** The two most striking patterns today are the **agent skill standardization** and **prompt efficiency** movements. `JuliusBrussee/caveman` (+926 stars) and `obra/superpowers` (+897 stars) represent a new category: tools that optimize *how agents communicate* rather than what they build. Caveman's 65% token reduction taps directly into the cost-and-latency pain point of agent-heavy workflows. Meanwhile, `agentskills` (new spec project) and `affaan-m/ECC` (225K stars) are converging on a unified skill packaging format—similar to how OpenAPI standardized API consumption. This suggests the agent ecosystem is entering a "plug-and-play" phase where skills become interchangeable across Claude Code, Codex, OpenCode, and Gemini CLI.

**Multi-agent orchestration goes mainstream.** `msitarzewski/agency-agents` (+3032 today) signals that developers are ready for full-blown AI agencies, not just single agents. Its viral growth suggests that the "agent as a service" model—where specialized agents (Reddit ninjas, frontend wizards) coordinate—is now accessible to individual developers. This mirrors the broader shift towards meshing multiple specialized models and tools.

**Vertical AI applications are accelerating.** `HKUDS/Vibe-Trading` (+939) and `santifer/career-ops` (+372) show that AI agents are being rapidly deployed for domain-specific tasks (trading, job search). This aligns with the maturity of LLM APIs and agent frameworks—developers no longer build the infrastructure; they build on top of it.

**RAG is evolving into agent memory.** Projects like `headroomlabs-ai/headroom` (token compression) and `cognee` (knowledge graph memory) are shifting RAG from simple retrieval to persistent, stateful memory layers for agents. This is a natural evolution: as agents run longer sessions, they need structured memory, not just vector search.

**Connection to industry events.** The surge in Claude Code skills (`caveman`, `codex-plugin-cc`, `ECC`) directly reflects Anthropic's recent push to make Claude Code extensible. Meanwhile, the rise of `browser-use/video-use` suggests that agent capabilities are expanding from text/web to multimodal (video editing). This is likely tied to the release of models with stronger video understanding (e.g., Gemini 2.5, GPT-4o video modes).

---

## 4. Community Hot Spots

- **[msitarzewski/agency-agents](https://github.com/msitarzewski/agency-agents)** — Multi-agent orchestration at its most accessible. Worth exploring if you want to understand how specialized agents can coordinate for real-world tasks (3K+ stars in a single day).
- **[JuliusBrussee/caveman](https://github.com/JuliusBrussee/caveman)** — The prompt efficiency movement is real. This Claude Code skill demonstrates that **token optimization** is a first-class engineering problem, not just a cost concern. Watch for similar projects targeting other models.
- **[agentskills/agentskills](https://github.com/agentskills/agentskills)** — A specification project aiming to standardize agent skill packaging. If this gains traction (like OpenAPI did), it will become the backbone of the agent ecosystem. Currently early, but strategically important.
- **[browser-use/video-use](https://github.com/browser-use/video-use)** — Video editing via coding agents. This is an early signal that agent capabilities are expanding beyond text and code into creative multimedia workflows. Could be the next big application category.
- **[headroomlabs-ai/headroom](https://github.com/headroomlabs-ai/headroom)** — RAG token compression (60-95% fewer tokens). As agent sessions grow longer, this becomes critical infrastructure. The "memory compression" approach could be as impactful as vector databases were for first-gen RAG.

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*